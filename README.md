# filecoin-miner-chart

Forked from https://github.com/openworklabs/filecoin-chart

Filecoin Miner chart is a helm chart for hosting Lotus Node clients, miners and workers. [Lotus](https://github.com/filecoin-project/lotus) is an implementation of the [Filecoin spec](https://filecoin-project.github.io/specs/).

## Goals

1. Deploy one or more instances of Lotus client nodes.
2. Expose Lotus node API's through HTTP endpoints.
3. Enable importing chain data for faster syncs.
4. Provide flexible configuration options to suit your needs.
5. Deploy one or more Lotus miner instances
6. Deploy one or more Lotus workers, split by Precommit1 and Precommit1/Commit1/Commit2 phases

For monitoring and graphing, see [filecoin-k8s](https://github.com/openworklabs/filecoin-k8s).
For customizing the Lotus Docker configuration, see [filecoin-docker](https://github.com/openworklabs/filecoin-docker).

## Prerequisites

### Kubernetes cluster (required)

This has only been tested on packet.net using the following machines types
* [g2.large](https://www.packet.com/cloud/servers/g2-large/) (daemon, miner, precommit2/commit1/commit2 worker)
* [c3.medium](https://www.packet.com/cloud/servers/c3-medium/) (precommit1 worker)

Current iteration also assumes rook-ceph installation with RBD and CephFS storageclasses.

### NGINX Ingress Controller (optional)

By default, a Lotus node running inside a Kubernetes cluster is not exposed to the public. The NGINX Ingress Controller is one configuration option that, when enabled, can expose your Lotus node via an HTTP endpoint.

For more details on installation, see [NGINX Installation Guide](https://kubernetes.github.io/ingress-nginx/deploy/).

**Note** - NGINX Ingress Controller is _different_ from [NGINX Kubernetes Ingress Controller](https://www.nginx.com/products/nginx/kubernetes-ingress-controller/) (which we are not using).

### Istio Gateway (optional)

[Istio](https://ihttps://istio.io/docs/setup/getting-started/stio.io/) is an alternative option for exposing your Lotus node to the public (instead of NGINX Ingress Controller). Istio comes with a number of additional features that make authorization, authentication, and managing microservices easier.

For more information on installation and usage, see [getting started with Istio](https://istio.io/docs/setup/getting-started/).

### Certbot (optional)

[Certbot](https://certbot.eff.org/) for handling certs and enabling HTTPS.

## Installation

The chart can be installed (and upgraded) via helm. To install the chart with the with the namespace `filecoin`, run these commands:

Clone this repository:
```shell
git clone https://github.com/openworklabs/filecoin-chart
cd filecoin-chart
```

Create a new `filecoin` namespace:

```shell
kubectl create ns filecoin
```

Deploy a new stateful set `node01` to the `filecoin` namespace:
```shell
helm upgrade --install --namespace filecoin -f values.yaml node01 .
```
The [values file](https://github.com/openworklabs/filecoin-chart/blob/master/values.yaml) contains all the configuration options.

## Configuration options

Coming soon

## License

This project is licensed under the [Apache 2.0](https://github.com/openworklabs/filecoin-chart/blob/master/LICENSE) license.
