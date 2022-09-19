# GitOps with FluxCD and Tanzu Packages

This repo can be used to deploy Tanzu Packages in a GitOps fashion. Read the following blog post for instructions on how to use the repo and its content:

https://beyondelastic.com/2022/06/08/gitops-with-fluxcd-and-tanzu-packages/

![alt text](https://github.com/beyondelastic/gitops-tanzu-packages/blob/main/images/overview.png)

Please note: Packages in this repository are pre-configured with example values for custom virtual hosts (ingress), storage class, passwords, syslog target, etc… you have to change the configuration according to your environment first! 

The [FluxCD Kustomization manifests](https://github.com/beyondelastic/gitops-tanzu-packages/tree/main/flux-config) have the following dependencies configured:
![alt text](https://github.com/beyondelastic/gitops-tanzu-packages/blob/main/images/dependencies.jpg)

Please note: This repository has been tested with TKGs (vSphere with Tanzu – 7U3). If you are using a TKGm cluster or your TKGs cluster has been attached to TMC, it will have the kapp-controller installed already and the package repository configured. In that case, modify or remove some of the [pre-reqs](https://github.com/beyondelastic/gitops-tanzu-packages/tree/main/pre-reqs) content on a fork of the repository. 

Please be aware, that this repository is not officially verified, tested or supported by VMware!