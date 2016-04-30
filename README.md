# Minikube

Run Kubernetes locally

[![Build Status](https://travis-ci.org/kubernetes/minikube.svg?branch=master)](https://travis-ci.org/kubernetes/minikube)

## Background

Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs
a single-node Kubernetes cluster inside a VM on your laptop for users looking
to try out Kubernetes or develop with it day-to-day.

## Design

Minikube uses [libmachine](https://github.com/docker/machine/tree/master/libmachine) for provisioning VMs, and [localkube](https://github.com/redspread/localkube)
for running the cluster.

For more information about minikube, see the [proposal](https://github.com/kubernetes/kubernetes/blob/master/docs/proposals/local-cluster-ux.md).

## Goals

* Works across multiple OSes - OS X, Linux and Windows primarily.
* Single command setup and teardown UX.
* Unified UX across OSes
* Minimal dependencies on third party software.
* Minimal resource overhead.
* Replace any other alternatives to local cluster deployment.

## Non Goals

* Simplifying kubernetes production deployment experience. Kube-deploy is attempting to tackle this problem.
* Supporting all possible deployment configurations of Kubernetes like various types of storage, networking, etc.


## Build Instructions

    go build -o minikube cli/main.go

## Run Instructions

Start the cluster with:

    ./minikube start
    Starting local Kubernetes cluster...
    2016/04/19 11:41:26 Machine exists!
    2016/04/19 11:41:27 Kubernetes is available at http://192.168.99.100:8080.
    2016/04/19 11:41:27 Run this command to use the cluster: 
    2016/04/19 11:41:27 kubectl config set-cluster minikube --insecure-skip-tls-verify=true --server=http://192.168.99.100:8080

Access the cluster with:

 First run the command from above:

    kubectl config set-cluster minikube --insecure-skip-tls-verify=true --server=http://192.168.99.100:8080

Then use kubectl normally:

    kubectl get pods --cluster=minikube

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for an overview of how to send pull requests.

### Running Tests

#### Unit Tests

Unit tests are run on Travis before code is merged. To run as part of a development cycle:

	go test $(go list ./... | grep -v /vendor/)

#### Integration Tests

Integration tests are currently run manually. To run them, first build the binary:
	
	go build -o minikube cli/main.go

Then test it:

	go test ./integration --tags=integration
