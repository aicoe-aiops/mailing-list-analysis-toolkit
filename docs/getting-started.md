# Get Started

This project contains examples of how to perform  end-to-end analysis on mailing lists. Check out the [project overview](../README.md) for an overview of this project.

## Run the Notebooks

There are interactive notebooks for this [project](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit) available for anyone to start using on the public [JupyterHub](https://jupyterhub-opf-jupyterhub.apps.zero.massopen.cloud/hub/login) instance on the [Massachusetts Open Cloud](https://massopen.cloud/) (MOC) right now!

1. To get started, access [JupyterHub](https://jupyterhub-opf-jupyterhub.apps.zero.massopen.cloud/), select log in with `moc-sso` and sign in using your Google Account.
2. After signing in, on the spawner page, please select the `Mailing list analysis toolkit` image in the JupyterHub Notebook Image section from the dropdown and select a `Medium` container size and hit `Start` to start your server.
3. Once your server has spawned, you should see a directory titled `mailing-list-analysis-toolkit-<current-timestamp>`.
4. Go to `notebooks/` and to look into the data collection and pre-processing steps explore the notebooks in the `01_collect_data` directory and to explore examples of analyses on mailing lists go through the notebooks in the `02_analyses` directory.
5. Here's a video that that can help familiarize you with the project.

`video: https://www.youtube.com/watch?v=arvpVoTXgZg`

If you need more help navigating the Operate First environment, we have a few [short videos](https://www.youtube.com/playlist?list=PL8VBRDTElCWpneB4dBu4u1kHElZVWfAwW) to help you get started.


## Project Assumptions

This repository assumes that you have an existing Open Data Hub deployed on OpenShift that includes, JupyterHub, Argo, Ceph, Hive, Cloudera Hue and Apache Superset.

* Take a look at [opendatahub.io](https://www.opendatahub.io) for details on the open data hub platform.
* Details of our existing public deployment can be found at [operate-first.cloud](https://www.operate-first.cloud/).

### Dashboard

The primary output and user interface for this application is a [Superset](https://superset.apache.org/) dashboard. This tool allows us to define certain data visualization elements from our analysis that we would like to publish and share with others, while also including enough flexibility and interactivity to allow users to explore the data themselves.

Our application is designed to automatically re-run the analyses on regular basis and ensure that the dashboard and all its plots are current and up to date.

* Current [Superset Dashboard](https://superset.datahub.redhat.com/superset/dashboard/fedora_mail/) can be found here. This is currently accesible internally at Red Hat. However, there are also plans to make the analysis publicly accessible on Operate first (see [issue](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit/issues/67))

![](assets/images/fedora-dashboard.png)

### Automated Argo workflows

If you'd like to automate your Jupyter notebooks using Argo, please follow the steps outlined in this [guide](../manifests/README.md). By following the steps in the document, your application can be fully set and ready to be deployed via Argo CD.
