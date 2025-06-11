# Valiton Kubernetes Blueprint

This organisation contains repositories for our Kubernetes blueprint.

## Goal

The goal of the blueprint is to create an automatic setup for Kubernetes clusters for different cloud 
providers. This setup includes the provisioning of commonly used Kubernetes addons. 

## Principles

Each blueprint sets up cloud infrastructure needed for the cluster using terraform or opentofu. Then 
a Kubernetes cluster is deployed and the [GitOps Bridge pattern](https://github.com/gitops-bridge-dev) is used
to deploy the addons

## Tools

### Infrastructure as Code

To deploy the infrastructure as code we use a terraform configuration that can also be applied using opentofu.

### GitOps

We use ArgoCD to deploy the Kubernetes addons

## Cloud providers

The supported cloud providers are AWS and BWS (our in house Openstack cloud, this should work for all Openstack clouds).

## Repositories

The blueprint is split into five repositories:

### charts

In the charts repository we have helm charts for some addons that bring not their own and 
charts to deploy custom resources for some of the addons of the blueprint. These charts are 
referenced in the ArgoCD application sets in the argocd repository.

### argocd

This repository contains the ArgoCD application sets for the addons we chose to deploy 
for the different cloud providers. Besides cloud dependent addons (e.g. cloud controller manager 
and cinder csi plugin for BWS/Openstack) there are additional addons that we found to be
useful, e.g. External Secrets Operator or External DNS.

If you want to use the blueprint, make sure to fork this repository because this defines
the software deployed to your cluster, you have to own this.

You can then also change the configuration, remove addons or add addons you want to use
with your cluster. Note: some of the addons are needed for the blue print to work and should
not be removed.

### terraform

This repository contains terraform modules for each supported cloud provider. The base module 
sets up the infrastructure and the cluster, the bootstrap module deploys ArgoCD and boostraps the 
deployment of the addons defined in the argocd repository. You can simply reference these modules
in your own configuration.

### terraform-helm-gitops-bridge

This repo maintains a fork of the original GitOps-Bridge module. The major addition is a wait period
when you destroy your infrastructure (mainly useful during development and testing).

### examples

The examples repository shows how to use the modules in an actual terraform configuration.
You should clone the repository as a starting point for your own configuration. Using it directly 
is only recommended for testing the blueprint. We also include sample workloads that can be used for 
testing.
