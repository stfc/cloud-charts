JupyterHub Chart
================

This is an opinionated chart for deploying JupyterHub on Kubernetes for STFC Cloud.
Some of the tailored features include:

- Using Longhorn for storage
- Template for pointing to a R/O NFS share for user data
- Examples of using our custom Docker images
- Template IRIS IAM integration
- Template KeyCloak integration

Requirements:
- Longhorn

## Setup
High level overview:

- Add the chart to the ApplicationSet as described in the [app deployment documentation](../../../docs/DEPLOYING_APPS.md)
- Copy the `cluster-template.yaml` from this directory to `clusters/<env>/dest/jupyter-values.yaml`
- Modify the values in the `jupyter-values.yaml` file to tailor the deployment
- Create a secrets file from a template in this directory in the relevant secrets environment
- Commit and push to as per the deployment documentation


## Values

A list of applicable values can be found in the [upstream Zero-to-Jupyter documentation](https://z2jh.jupyter.org/en/latest/jupyterhub/customization.html) and the [values file](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/blob/main/jupyterhub/values.yaml).

We default the following changes:

- Mount shared memory (`/dev/shm`) for tensor-based workloads
- Dynamically provision 10GB volumes by default
- Explicitly use `longhorn` as the storage class for user volumes
- Cap the default CPU and memory limits to 2 CPU and 2GB RAM
- Include two example images for the minimal notebook, and data science notebook
- Cull (shutdown) inactive spaces every 5 days, instead of 1 hour

## Cluster Template

The cluster template additionally provides examples of the following customisations:

- Setting up HTTPS using LetsEncrypt
- Specifying a specific FIP for a dedicated ingress-point
- Mounting an existing NFS share for user data using the `nfs.enabled` and `nfs.ip` values
- Changing the resources and images used by users
- Includes examples of tailoring the resources, and adding a GPU to the user pods

## Secrets

The following secret templates are available to deploy. These should be tailored following the in-line comments in the templates and placed into `secrets` as per the [secrets documentation](../../../docs/secrets.md).
