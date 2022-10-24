# GitOps with FluxCD with Tanzu Packages or Helm Charts

**Because this repository is intended to be used with Tanzu Mission Control, I am referring to certain values configured by Tanzu Mission Control such as the Flux GitRepository object. For the purposes of this example my repo is named 'fluxcd-poc' and is referred-to throughout the kustomization YAMLs.**

**This is also the reason I am currently using the 'master' branch; the ability to change branches via Tanzu Mission Control is in progress** 

**_If you need the GitRepository object automatically created for you, move unused\tanzu-packages-source.yaml into the pre-reqs folder._**

This repo can be used to deploy Tanzu Packages and Helm Charts in a GitOps fashion.

![alt text](https://github.com/coreydinkens/tmc-flux-poc/blob/master/images/overview.png)

#### Please note: Packages in this repository are pre-configured with example values for custom virtual hosts (ingress), storage class, passwords, syslog target, etc… you have to change the configuration according to your environment first! 

The current process to update the values is: 
1. Modify package values as desired under `data-values` folder
2. Encode the entire values file in base64 ie. On linux execute: `cat ./data-values/harbor-data-values.yaml | base64`
3. Copy the output and update the data key in `<packagename>/<packagename>-data-values-secret.yaml`

The [FluxCD Kustomization manifests](https://github.com/coreydinkens/tmc-flux-poc/tree/master/flux-config) have the following dependencies configured:
1. **pre-reqs folder** - Installs service accounts needed to manage Tanzu Carvel packages
2. **flux-config folder** - Installs all Tanzu packages
  a. pre-reqs
    1. cert-manager
    2. fluent-bit
    3. contour  
      a. Harbor
      b. Prometheus
        1. Grafana



Once Flux has been successfully enabled, add kustomizations in the following order, then remove in reverse to avoid package install/removal issues with prune enabled:
1. Add pre-reqs folder Flux kustomization
2. Add flux-config folder Flux kustomization


It is important to note this repo is not what I would consider 'production' ready due to the current package installer service account config. Verifying whether I need to move each SA to it's own namespace to match existing Carvel methodology

Please note: This repository has been tested with TKGs (vSphere with Tanzu – 7U3).

# GitOps with FluxCD and Helm Packages
Use these two directories to test Helm deployments with Flux:
1. kube-prometheus-stack-helm - Self contained Prometheus + Grafana monitoring stack
2. wordpress-helm - Bitnami Wordpress site + MariaDB deployment

Please be aware, that this repository is not officially verified, tested or supported by VMware!
