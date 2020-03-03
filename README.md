# Maxikube K8s Lab Environment

## Summary

Maxikube is a Kubernetes lab environment based on Vagrant, Ansible and VirtualBox. The main folder contains Vagrant code to stand up a single Kubernetes master server instance with 2 nodes. The number of nodes is configurable.

A lot of stuff in this repository is based on this blog post:
* https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

## Requirements

The pre-requistes for this are [Ansible](https://github.com/ansible/ansible), [Vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org), installed on the PC you intend to run it on, and 3 GB of RAM.

## Quickstart

### Clone
```
git clone https://github.com/mzima/maxikube
```

### Start / Stop / Destroy Maxikube
```
vagrant up
vagrant stop
vagrant destroy
```

### How to use kubectl with Maxikube

#### kubectl on the master node

Ssh into the master node to use kubectl from there:

```
vagrant ssh master-1
kubectl get all
```

#### kubectl on your local system

You need to install kubectl as described here: https://kubernetes.io/docs/tasks/tools/install-kubectl/.

The Vagrant script will automatically save the Kubernetes context config file to `~/.kube/config-maxikube` on your local machine, however you might have to modify your `$KUBECONFIG` environment variable:

```
export KUBECONFIG=~/.kube/config-maxikube:$KUBECONFIG
kubectl get all
```

## Configuration
The main folder contains a `config.yaml` file, which can be used to configure your Maxikube Kubernetes cluster. The following things can be changed:

* K8s nodes count
* master/nodes: number of cpus
* master/nodes: memory allocation 
