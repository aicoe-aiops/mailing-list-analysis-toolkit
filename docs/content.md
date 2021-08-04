# Content

The project repository for mailing list analysis toolkit contains example code for how to develop a custom end-to-end email analytics service using the Open Data Hub on OpenShift.

Here's a [video](https://www.youtube.com/watch?v=arvpVoTXgZg) which goes over the project and demonstrates the automated dashboard.

## Current Lists/ Datasets

* [Fedora Devel](https://lists.fedoraproject.org/archives/list/devel@lists.fedoraproject.org/)
* ? (please [open an issue](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit/issues/new?assignees=&labels=enhancement&template=feature_request.md) if you'd like another mailing list included)

## Application Overview

At a high level, this application can be seen as an [Argo Workflow](https://argoproj.github.io/argo/) which orchestrates a set of Jupyter notebooks to push transformed data to Ceph. Each notebook is responsible for a single task and is used either for collecting raw data from the [Fedora HyperKitty mailing list archive](https://lists.fedoraproject.org/archives/) (our live data set), preprocessing that data, or performing some specific analytics task. In almost all cases, the notebooks both push their outputs to Ceph remote storage (for use in a future run) as well as maintain a local copy within a shared volume among the application's pods for use by other notebook processes. Finally we use external tables in Apache Hive, with Hue, to connect the Ceph data to a SQL database for interactive visualization with Superset.

![](docs/assets/images/app-overview.png)

Here is a [guide](../manifests/README.md) which outlines the steps needed to automate your Jupyter notebooks using Argo. By following the steps in the document, your application can be fully set and ready to be deployed via Argo CD.

## Notebooks

Currently notebooks are divided into two sub-directories `notebooks/01_collect_data` and `notebooks/02_analyses` depending on what stage in the argo workflow they belong to. This should make it explicit where notebooks go in the argo workflow dependency tree when defining it in the `wftmpl.yaml` manifest file. Ideally, the notebooks in `notebooks/01_collect_data` should not be dependent on each other (they could be run in parallel) and notebooks in `notebooks/02_analyses` should be independent of each other and only depend on the output of notebooks in `notebooks/01_collect_date`. That way we keep the workflow and dependency structure clear during development and we believe this architecture can be easily modified to accommodate more complex dependency requirements.


* **01_collect_data**

    * [collect_data](../notebooks/01_collect_data/collect_data.ipynb) - Download new data from source and push to remote storage
    * [download_dataset](../notebooks/01_collect_data/download_datasets.ipynb) - Download existing preprocessed data from remote storage
    * [gz_to_raw](../notebooks/01_collect_data/gz_to_raw.ipynb) - Convert downloaded *.gz files to raw mbox format)
    * [raw_to_meta](../notebooks/01_collect_data/raw_to_meta.ipynb) - Process mbox files into monthly metadata *.csv and push to remote storage
    * [raw_to_text](../notebooks/01_collect_data/raw_to_text.ipynb) - Process mbox files into monthly email body *.csv and push to remote storage
    * ? (please [open an issue](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit/issues/new?assignees=&labels=enhancement&template=feature_request.md) if you would like an additional data collection or pre processing step added)

 * **02_analyses**

    * [contributor_analysis](../notebooks/02_analyses/contributor_analysis.ipynb) (Quantify users monthly activity and push to remote storage)
    * [keyword_analysis](../notebooks/02_analyses/contributor_analysis.ipynb) (Identify top Keywords for each month and push to remote storage)
    * [sentiment analysis](../notebooks/02_analyses/sentiment_analysis.ipynb) (Sentiment Analysis on body of emails)
    * ? (please [open an issue](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit/issues/new?assignees=&labels=enhancement&template=feature_request.md) if you would like an additional analysis added)
