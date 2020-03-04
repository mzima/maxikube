# Maxikube K8s Lab Environment

## Summary

Maxikube is a Kubernetes lab environment based on Vagrant, Ansible and VirtualBox. The main folder contains Vagrant code to stand up a single Kubernetes master server instance with 2 nodes. The number of nodes is configurable.

A lot of stuff in this repository is based on this blog post:
* https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

## Requirements

The pre-requistes for this are [Ansible](https://github.com/ansible/ansible), [Vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org), installed on the PC you intend to run it on, and 4 GB of RAM.

## Quickstart

### Install
```
$ git clone https://github.com/mzima/maxikube
```

### Start / Halt / Destroy Maxikube
```
$ vagrant up
$ vagrant halt
$ vagrant destroy
```

## Configuration
The main folder contains a `config.yaml` file, which can be used to configure your Maxikube Kubernetes cluster. The following things can be changed:

* K8s nodes count
* master/nodes: number of cpus
* master/nodes: memory allocation

### config.yaml

```
# Maxikube Configuration

master:
  cpus: 2
  memory: 2048

node:
  count: 2
  cpus: 1
  memory: 1024
````

## How to use kubectl with Maxikube

#### On the master node

Ssh into the master node to use kubectl from there:
```
$ vagrant ssh master-1
$ kubectl get all
```

#### On your local system

You need to install kubectl as described here: https://kubernetes.io/docs/tasks/tools/install-kubectl/.

The Vagrant script will automatically save the Kubernetes context config file to `~/.kube/config-maxikube` on your local machine, however you might have to modify your `$KUBECONFIG` environment variable:
```
$ export KUBECONFIG=~/.kube/config-maxikube:$KUBECONFIG
$ kubectl get all
```

