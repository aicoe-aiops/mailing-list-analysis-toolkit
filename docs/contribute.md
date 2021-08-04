# Contribute to the Mailing List Analysis Toolkit

To get started with familiarizing yourself with the Mailing List analysis project, check how to [Get Started](getting-started.md).

## Add an Analysis

One of the key benefits of this approach is that it allows for the bulk of the development to be done directly in a jupyter notebook as well as making adding new analyses or preprocessing steps as simple adding a new notebook to the repository.

For example, in order to add an additional analysis to the application one just needs to make [submit a PR](https://github.com/aicoe-aiops/mailing-list-analysis-toolkit/pulls) with a new notebook in `notebooks/02_analyses` and a small update to `manifest/wftmpl.yaml` to include the new notebook into the workflow.

You can also reach out to aicoe-aiops@redhat.com for any questions.

## Automation and Workflow Configurations

Please see the README at [manifests/README.md](../manifests/README.md) for complete details on how to define the automation and application workflow via Argo. By following the guide one can automate their application and Jupyter Notebooks using ArgoCD.
