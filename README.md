# Maxikube K8s Lab Environment

## Summary

Maxikube is a Kubernetes lab environment based on Vagrant and Ansible. The vagrant folder contains Vagrant code to stand up a single Kubernetes master server instance with 2 nodes.

A lot of stuff in this repository is based on this blog post:
* https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

## Requirements

The pre-requistes for this are [Ansible](https://github.com/ansible/ansible), [Vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org), installed on the PC you intend to run it on, and 3 GB of RAM.

## Quickstart

### Clone
```
git clone https://github.com/mzima/maxikube
```

### Start / Stop / Destroy
```
vagrant up
vagrant stop
vagrant destroy
```

# Configuration
The vagrant folder contains a `config.yaml` file, which can be used to configure memory usage, cpu count and Kubernetes node count. Maxikube does not support multi master configurations yet.

