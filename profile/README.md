# Valiton Kubernetes Blueprint

This organisation contains repository for our Kubernetes blueprint.

## Goal

The goal of the blueprint is to create an automatic setup for Kubernetes clusters for different cloud 
providers. This setup includes the provisioning of commonly used Kuberenetes addons. 

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
