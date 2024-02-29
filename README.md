# Automated K3s HA Cluster Deployment with Ansible
## Overview
This project aims to provide a fully automated solution for deploying a K3s cluster using Ansible playbooks. The deployment process involves two main playbooks: prepare-node.yaml and deploy-cluster.yaml.

prepare-node.yaml: This playbook ensures that nodes are ready for K3s installation. It configures necessary settings, such as disabling the firewall and turning off swap, to create a suitable environment.

deploy-cluster.yaml: This playbook orchestrates the deployment of at least 3 master nodes and an unlimited number of worker nodes. It automates the setup of the first master node to facilitate the seamless joining of additional nodes.

## Prerequisites
Before using the playbooks, ensure the following prerequisites are met:

Ansible is installed on the machine from which you run the playbooks.
Target nodes are accessible via SSH, and Ansible can establish connections to them.
Nodes meet the minimum requirements for running K3s.
## Usage
### 1. Clone the Repository
```
git clone https://github.com/Antares-85/k3s_automate.git
cd k3s_automate
```
### 2. Edit Configuration
I exported a variable in the Ansible server for the IP of kube-VIP master loadbalance
```
export tls_san="IP_LOAD_BALANCER"
```
### 3. Run prepare-node.yaml
This playbook prepares nodes for K3s installation.

```
ansible-playbook -i inventory.ini prepare-node.yaml
```
### 4. Run deploy-cluster.yaml
Deploy the K3s cluster using this playbook.

```
ansible-playbook -i inventory.ini deploy-cluster.yaml
```
## Configuration
### inventory.ini
Edit the inventory file to define your node configuration. Specify master and worker nodes.

```
[master-primary]
master1 ansible_host=your-master-ip ansible_user=your-ssh-user

[master-dependent]
master2 ansible_host=your-master-ip ansible_user=your-ssh-user
master2 ansible_host=your-master-ip ansible_user=your-ssh-user
# Add more master nodes as needed

[workers]
worker1 ansible_host=your-worker-ip ansible_user=your-ssh-user
worker2 ansible_host=your-worker-ip ansible_user=your-ssh-user
# Add more worker nodes as needed
```
