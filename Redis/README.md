# Redis(R) configuration with HELM
[![CircleCI](https://circleci.com/gh/RedisTimeSeries/prometheus-redistimeseries-adapter/tree/master.svg?style=svg) ](https://circleci.com/gh/RedisTimeSeries/prometheus-redistimeseries-adapter/tree/master)![68747470733a2f2f72656164746865646f63732e6f72672f70726f6a656374732f656c6b2d646f636b65722f62616467652f3f76657273696f6e3d6c6174657374](https://user-images.githubusercontent.com/62883434/214496397-828e853c-512e-405b-b678-4989a36971c7.svg) 

![Logo-redis svg](https://user-images.githubusercontent.com/62883434/214499731-8fd4178c-669b-40ee-841a-69389ab5c243.png)




Redis(R) is an open source, advanced key-value store. It is often referred to as a data structure server since keys can contain strings, hashes, lists, sets and sorted sets.
Disclaimer: Redis is a registered trademark of Redis Ltd. Any rights therein are reserved to Redis Ltd. Any use by Bitnami is for referential purposes only and does not indicate any sponsorship, endorsement, or affiliation between Redis Ltd.

## TL;DR

```console
$ helm repo add my-repo https://charts.bitnami.com/bitnami
$ helm install my-release my-repo/redis
```


## Introduction

This chart bootstraps a [Redis&reg;](https://github.com/bitnami/containers/tree/main/bitnami/redis) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.dev/) for deployment and management of Helm Charts in clusters.

### Choose between Redis&reg; Helm Chart and Redis&reg; Cluster Helm Chart

You can choose any of the two Redis&reg; Helm charts for deploying a Redis&reg; cluster.

1. [Redis&reg; Helm Chart](https://github.com/bitnami/charts/tree/main/bitnami/redis) will deploy a master-replica cluster, with the [option](https://github.com/bitnami/charts/tree/main/bitnami/redis#redis-sentinel-configuration-parameters) of enabling using Redis&reg; Sentinel.
2. [Redis&reg; Cluster Helm Chart](https://github.com/bitnami/charts/tree/main/bitnami/redis-cluster) will deploy a Redis&reg; Cluster topology with sharding.

The main features of each chart are the following:

| Redis&reg;                                     | Redis&reg; Cluster                                             |
|--------------------------------------------------------|------------------------------------------------------------------------|
| Supports multiple databases                            | Supports only one database. Better if you have a big dataset           |
| Single write point (single master)                     | Multiple write points (multiple masters)                               |
| ![redis-topology](https://user-images.githubusercontent.com/62883434/214499477-b9f581ec-74ea-4df7-b78f-1080846986e5.png) | ![redis-cluster-topology](https://user-images.githubusercontent.com/62883434/214499503-877901c5-25ff-41b8-bf4e-d7e7dde350b5.png) |



## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:
you can change `my-release` to any specific name for your project
```console
$ helm repo add my-repo https://charts.bitnami.com/bitnami
$ helm install my-release my-repo/redis
```

The command deploys Redis&reg; on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.
