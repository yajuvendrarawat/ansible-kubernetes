# Provisioning an AKS, EKS, or GKE cluster with Ansible
[![Ansible Lint](https://github.com/nleiva/ansible-kubernetes/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/nleiva/ansible-kubernetes/actions/workflows/ansible-lint.yml)

<p align="center">
<img height="400" src="./pictures/k8s_ansible.png">
</p>

## Requirements

Ansible 2.9+ needs to be [installed](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-with-pip) in your computer to run this. [Python3](https://wiki.python.org/moin/BeginnersGuide/Download) as well.

```bash
python -m pip install --user ansible
```

## Cloud Provider details

Details on the requirements to create a Kubernetes cluster on each cloud provider are described in the following sub-pages:  

- [AKS](aks.md) (Azure)
- [EKS](eks.md) (AWS)
- [GKE](gke.md) (GCP)

**Note**: This is work in progress.

## Creating a new Kubernetes Cluster

Follow these steps to provision a Kubernetes cluster.

1. Clone this repository: `git clone https://github.com/nleiva/ansible-kubernetes.git`

2. Make your cloud provider credentials available as environment variables (`export`). See [AKS](aks.md), [EKS](eks.md), or [GKE](gke.md) for more details.

```bash
export <credential>='...'
```

3. Run the [Playbook](main.yml) and wait a couple of minutes while your Kubernetes cluster is being provisioned. Define the cloud provider via the variable `cloud_provider` (either; `aws`, `azure`, or `gcp`).

```bash
ansible-playbook main.yml -v --extra-vars "cloud_provider=azure"
```

## Integrating with Advanced Cluster Management

See [ACM](acm.md) for details.

```bash
ansible-playbook main.yml -v --extra-vars "acm_import=true cloud_provider=aws"
```

## Destroying a Kubernetes Cluster

Follow these steps to delete a Kubernetes cluster.

1. Run the [Playbook](main.yml) with the variable `delete` set to `true`.Define the cloud provider via the variable `cloud_provider` (either; `aws`, `azure`, or `gcp`).

```bash
ansible-playbook main.yml -v --extra-vars "delete=true cloud_provider=azure"
```

## Run from an Execution Environment

You need [ansible-navigator installed](https://github.com/ansible/ansible-navigator#installing). Here is an example to create an AKS cluster with it.

```bash
ansible-navigator run main.yml -v --extra-vars "cloud_provider=azure"
```

**Note**: I use [podman](https://podman.io/) as my container engine (`container-engine`). You can change to another alternative in the ansible [navigator config file](ansible-navigator.yml).

**Note** For Tower/AAP we need to setup the custom KUBE credentials K8S_AUTH_KUBECONFIG - Ref - https://blog.networktocode.com/post/kubernetes-collection-ansible/


