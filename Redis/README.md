# Redis(R) configuration with HELM
[![CircleCI](https://circleci.com/gh/RedisTimeSeries/prometheus-redistimeseries-adapter/tree/master.svg?style=svg) ](https://circleci.com/gh/RedisTimeSeries/prometheus-redistimeseries-adapter/tree/master)![68747470733a2f2f72656164746865646f63732e6f72672f70726f6a656374732f656c6b2d646f636b65722f62616467652f3f76657273696f6e3d6c6174657374](https://user-images.githubusercontent.com/62883434/214496397-828e853c-512e-405b-b678-4989a36971c7.svg) [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/bitnami)](https://artifacthub.io/packages/search?repo=bitnami)

![Logo-redis svg](https://user-images.githubusercontent.com/62883434/214499731-8fd4178c-669b-40ee-841a-69389ab5c243.png)




Redis(R) is an open source, advanced key-value store. It is often referred to as a data structure server since keys can contain strings, hashes, lists, sets and sorted sets.
Disclaimer: Redis is a registered trademark of Redis Ltd. Any rights therein are reserved to Redis Ltd. Any use by Bitnami is for referential purposes only and does not indicate any sponsorship, endorsement, or affiliation between Redis Ltd.

## TL;DR

```console
$ helm repo add my-repo https://charts.bitnami.com/bitnami
$ helm install my-release -f values.yaml my-repo/redis
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

## Parameters

### Global parameters

| Name                      | Description                                            | Value |
| ------------------------- | ------------------------------------------------------ | ----- |
| `global.imageRegistry`    | Global Docker image registry                           | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array        | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)           | `""`  |
| `global.redis.password`   | Global Redis&reg; password (overrides `auth.password`) | `""`  |


### Common parameters

| Name                     | Description                                                                             | Value           |
| ------------------------ | --------------------------------------------------------------------------------------- | --------------- |
| `kubeVersion`            | Override Kubernetes version                                                             | `""`            |
| `nameOverride`           | String to partially override common.names.fullname                                      | `""`            |
| `fullnameOverride`       | String to fully override common.names.fullname                                          | `""`            |
| `commonLabels`           | Labels to add to all deployed objects                                                   | `{}`            |
| `commonAnnotations`      | Annotations to add to all deployed objects                                              | `{}`            |
| `secretAnnotations`      | Annotations to add to secret                                                            | `{}`            |
| `clusterDomain`          | Kubernetes cluster domain name                                                          | `cluster.local` |
| `extraDeploy`            | Array of extra objects to deploy with the release                                       | `[]`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden) | `false`         |
| `diagnosticMode.command` | Command to override all containers in the deployment                                    | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the deployment                                       | `["infinity"]`  |


### Redis&reg; Image parameters

| Name                | Description                                                                                                | Value                |
| ------------------- | ---------------------------------------------------------------------------------------------------------- | -------------------- |
| `image.registry`    | Redis&reg; image registry                                                                                  | `docker.io`          |
| `image.repository`  | Redis&reg; image repository                                                                                | `bitnami/redis`      |
| `image.tag`         | Redis&reg; image tag (immutable tags are recommended)                                                      | `7.0.8-debian-11-r0` |
| `image.digest`      | Redis&reg; image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                 |
| `image.pullPolicy`  | Redis&reg; image pull policy                                                                               | `IfNotPresent`       |
| `image.pullSecrets` | Redis&reg; image pull secrets                                                                              | `[]`                 |
| `image.debug`       | Enable image debug mode                                                                                    | `false`              |


### Redis&reg; common configuration parameters

| Name                             | Description                                                                           | Value         |
| -------------------------------- | ------------------------------------------------------------------------------------- | ------------- |
| `architecture`                   | Redis&reg; architecture. Allowed values: `standalone` or `replication`                | `replication` |
| `auth.enabled`                   | Enable password authentication                                                        | `true`        |
| `auth.sentinel`                  | Enable password authentication on sentinels too                                       | `true`        |
| `auth.password`                  | Redis&reg; password                                                                   | `""`          |
| `auth.existingSecret`            | The name of an existing secret with Redis&reg; credentials                            | `""`          |
| `auth.existingSecretPasswordKey` | Password key to be retrieved from existing secret                                     | `""`          |
| `auth.usePasswordFiles`          | Mount credentials as files instead of using an environment variable                   | `false`       |
| `commonConfiguration`            | Common configuration to be added into the ConfigMap                                   | `""`          |
| `existingConfigmap`              | The name of an existing ConfigMap with your custom configuration for Redis&reg; nodes | `""`          |


### Redis&reg; master configuration parameters

| Name                                                 | Description                                                                                           | Value                    |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------ |
| `master.count`                                       | Number of Redis&reg; master instances to deploy (experimental, requires additional configuration)     | `1`                      |
| `master.configuration`                               | Configuration for Redis&reg; master nodes                                                             | `""`                     |
| `master.disableCommands`                             | Array with Redis&reg; commands to disable on master nodes                                             | `["FLUSHDB","FLUSHALL"]` |
| `master.command`                                     | Override default container command (useful when using custom images)                                  | `[]`                     |
| `master.args`                                        | Override default container args (useful when using custom images)                                     | `[]`                     |
| `master.preExecCmds`                                 | Additional commands to run prior to starting Redis&reg; master                                        | `[]`                     |
| `master.extraFlags`                                  | Array with additional command line flags for Redis&reg; master                                        | `[]`                     |
| `master.extraEnvVars`                                | Array with extra environment variables to add to Redis&reg; master nodes                              | `[]`                     |
| `master.extraEnvVarsCM`                              | Name of existing ConfigMap containing extra env vars for Redis&reg; master nodes                      | `""`                     |
| `master.extraEnvVarsSecret`                          | Name of existing Secret containing extra env vars for Redis&reg; master nodes                         | `""`                     |
| `master.containerPorts.redis`                        | Container port to open on Redis&reg; master nodes                                                     | `6379`                   |
| `master.startupProbe.enabled`                        | Enable startupProbe on Redis&reg; master nodes                                                        | `false`                  |
| `master.startupProbe.initialDelaySeconds`            | Initial delay seconds for startupProbe                                                                | `20`                     |
| `master.startupProbe.periodSeconds`                  | Period seconds for startupProbe                                                                       | `5`                      |
| `master.startupProbe.timeoutSeconds`                 | Timeout seconds for startupProbe                                                                      | `5`                      |
| `master.startupProbe.failureThreshold`               | Failure threshold for startupProbe                                                                    | `5`                      |
| `master.startupProbe.successThreshold`               | Success threshold for startupProbe                                                                    | `1`                      |
| `master.livenessProbe.enabled`                       | Enable livenessProbe on Redis&reg; master nodes                                                       | `true`                   |
| `master.livenessProbe.initialDelaySeconds`           | Initial delay seconds for livenessProbe                                                               | `20`                     |
| `master.livenessProbe.periodSeconds`                 | Period seconds for livenessProbe                                                                      | `5`                      |
| `master.livenessProbe.timeoutSeconds`                | Timeout seconds for livenessProbe                                                                     | `5`                      |
| `master.livenessProbe.failureThreshold`              | Failure threshold for livenessProbe                                                                   | `5`                      |
| `master.livenessProbe.successThreshold`              | Success threshold for livenessProbe                                                                   | `1`                      |
| `master.readinessProbe.enabled`                      | Enable readinessProbe on Redis&reg; master nodes                                                      | `true`                   |
| `master.readinessProbe.initialDelaySeconds`          | Initial delay seconds for readinessProbe                                                              | `20`                     |
| `master.readinessProbe.periodSeconds`                | Period seconds for readinessProbe                                                                     | `5`                      |
| `master.readinessProbe.timeoutSeconds`               | Timeout seconds for readinessProbe                                                                    | `1`                      |
| `master.readinessProbe.failureThreshold`             | Failure threshold for readinessProbe                                                                  | `5`                      |
| `master.readinessProbe.successThreshold`             | Success threshold for readinessProbe                                                                  | `1`                      |
| `master.customStartupProbe`                          | Custom startupProbe that overrides the default one                                                    | `{}`                     |
| `master.customLivenessProbe`                         | Custom livenessProbe that overrides the default one                                                   | `{}`                     |
| `master.customReadinessProbe`                        | Custom readinessProbe that overrides the default one                                                  | `{}`                     |
| `master.resources.limits`                            | The resources limits for the Redis&reg; master containers                                             | `{}`                     |
| `master.resources.requests`                          | The requested resources for the Redis&reg; master containers                                          | `{}`                     |
| `master.podSecurityContext.enabled`                  | Enabled Redis&reg; master pods' Security Context                                                      | `true`                   |
| `master.podSecurityContext.fsGroup`                  | Set Redis&reg; master pod's Security Context fsGroup                                                  | `1001`                   |
| `master.containerSecurityContext.enabled`            | Enabled Redis&reg; master containers' Security Context                                                | `true`                   |
| `master.containerSecurityContext.runAsUser`          | Set Redis&reg; master containers' Security Context runAsUser                                          | `1001`                   |
| `master.kind`                                        | Use either Deployment or StatefulSet (default)                                                        | `StatefulSet`            |
| `master.schedulerName`                               | Alternate scheduler for Redis&reg; master pods                                                        | `""`                     |
| `master.updateStrategy.type`                         | Redis&reg; master statefulset strategy type                                                           | `RollingUpdate`          |
| `master.minReadySeconds`                             | How many seconds a pod needs to be ready before killing the next, during update                       | `0`                      |
| `master.priorityClassName`                           | Redis&reg; master pods' priorityClassName                                                             | `""`                     |
| `master.hostAliases`                                 | Redis&reg; master pods host aliases                                                                   | `[]`                     |
| `master.podLabels`                                   | Extra labels for Redis&reg; master pods                                                               | `{}`                     |
| `master.podAnnotations`                              | Annotations for Redis&reg; master pods                                                                | `{}`                     |
| `master.shareProcessNamespace`                       | Share a single process namespace between all of the containers in Redis&reg; master pods              | `false`                  |
| `master.podAffinityPreset`                           | Pod affinity preset. Ignored if `master.affinity` is set. Allowed values: `soft` or `hard`            | `""`                     |
| `master.podAntiAffinityPreset`                       | Pod anti-affinity preset. Ignored if `master.affinity` is set. Allowed values: `soft` or `hard`       | `soft`                   |
| `master.nodeAffinityPreset.type`                     | Node affinity preset type. Ignored if `master.affinity` is set. Allowed values: `soft` or `hard`      | `""`                     |
| `master.nodeAffinityPreset.key`                      | Node label key to match. Ignored if `master.affinity` is set                                          | `""`                     |
| `master.nodeAffinityPreset.values`                   | Node label values to match. Ignored if `master.affinity` is set                                       | `[]`                     |
| `master.affinity`                                    | Affinity for Redis&reg; master pods assignment                                                        | `{}`                     |
| `master.nodeSelector`                                | Node labels for Redis&reg; master pods assignment                                                     | `{}`                     |
| `master.tolerations`                                 | Tolerations for Redis&reg; master pods assignment                                                     | `[]`                     |
| `master.topologySpreadConstraints`                   | Spread Constraints for Redis&reg; master pod assignment                                               | `[]`                     |
| `master.dnsPolicy`                                   | DNS Policy for Redis&reg; master pod                                                                  | `""`                     |
| `master.dnsConfig`                                   | DNS Configuration for Redis&reg; master pod                                                           | `{}`                     |
| `master.lifecycleHooks`                              | for the Redis&reg; master container(s) to automate configuration before or after startup              | `{}`                     |
| `master.extraVolumes`                                | Optionally specify extra list of additional volumes for the Redis&reg; master pod(s)                  | `[]`                     |
| `master.extraVolumeMounts`                           | Optionally specify extra list of additional volumeMounts for the Redis&reg; master container(s)       | `[]`                     |
| `master.sidecars`                                    | Add additional sidecar containers to the Redis&reg; master pod(s)                                     | `[]`                     |
| `master.initContainers`                              | Add additional init containers to the Redis&reg; master pod(s)                                        | `[]`                     |
| `master.persistence.enabled`                         | Enable persistence on Redis&reg; master nodes using Persistent Volume Claims                          | `true`                   |
| `master.persistence.medium`                          | Provide a medium for `emptyDir` volumes.                                                              | `""`                     |
| `master.persistence.sizeLimit`                       | Set this to enable a size limit for `emptyDir` volumes.                                               | `""`                     |
| `master.persistence.path`                            | The path the volume will be mounted at on Redis&reg; master containers                                | `/data`                  |
| `master.persistence.subPath`                         | The subdirectory of the volume to mount on Redis&reg; master containers                               | `""`                     |
| `master.persistence.subPathExpr`                     | Used to construct the subPath subdirectory of the volume to mount on Redis&reg; master containers     | `""`                     |
| `master.persistence.storageClass`                    | Persistent Volume storage class                                                                       | `""`                     |
| `master.persistence.accessModes`                     | Persistent Volume access modes                                                                        | `["ReadWriteOnce"]`      |
| `master.persistence.size`                            | Persistent Volume size                                                                                | `8Gi`                    |
| `master.persistence.annotations`                     | Additional custom annotations for the PVC                                                             | `{}`                     |
| `master.persistence.selector`                        | Additional labels to match for the PVC                                                                | `{}`                     |
| `master.persistence.dataSource`                      | Custom PVC data source                                                                                | `{}`                     |
| `master.persistence.existingClaim`                   | Use a existing PVC which must be created manually before bound                                        | `""`                     |
| `master.service.type`                                | Redis&reg; master service type                                                                        | `ClusterIP`              |
| `master.service.ports.redis`                         | Redis&reg; master service port                                                                        | `6379`                   |
| `master.service.nodePorts.redis`                     | Node port for Redis&reg; master                                                                       | `""`                     |
| `master.service.externalTrafficPolicy`               | Redis&reg; master service external traffic policy                                                     | `Cluster`                |
| `master.service.extraPorts`                          | Extra ports to expose (normally used with the `sidecar` value)                                        | `[]`                     |
| `master.service.internalTrafficPolicy`               | Redis&reg; master service internal traffic policy (requires Kubernetes v1.22 or greater to be usable) | `Cluster`                |
| `master.service.clusterIP`                           | Redis&reg; master service Cluster IP                                                                  | `""`                     |
| `master.service.loadBalancerIP`                      | Redis&reg; master service Load Balancer IP                                                            | `""`                     |
| `master.service.loadBalancerSourceRanges`            | Redis&reg; master service Load Balancer sources                                                       | `[]`                     |
| `master.service.externalIPs`                         | Redis&reg; master service External IPs                                                                | `[]`                     |
| `master.service.annotations`                         | Additional custom annotations for Redis&reg; master service                                           | `{}`                     |
| `master.service.sessionAffinity`                     | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                  | `None`                   |
| `master.service.sessionAffinityConfig`               | Additional settings for the sessionAffinity                                                           | `{}`                     |
| `master.terminationGracePeriodSeconds`               | Integer setting the termination grace period for the redis-master pods                                | `30`                     |
| `master.serviceAccount.create`                       | Specifies whether a ServiceAccount should be created                                                  | `false`                  |
| `master.serviceAccount.name`                         | The name of the ServiceAccount to use.                                                                | `""`                     |
| `master.serviceAccount.automountServiceAccountToken` | Whether to auto mount the service account token                                                       | `true`                   |
| `master.serviceAccount.annotations`                  | Additional custom annotations for the ServiceAccount                                                  | `{}`                     |


### Redis&reg; replicas configuration parameters

| Name                                                  | Description                                                                                             | Value                    |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------ |
| `replica.replicaCount`                                | Number of Redis&reg; replicas to deploy                                                                 | `3`                      |
| `replica.configuration`                               | Configuration for Redis&reg; replicas nodes                                                             | `""`                     |
| `replica.disableCommands`                             | Array with Redis&reg; commands to disable on replicas nodes                                             | `["FLUSHDB","FLUSHALL"]` |
| `replica.command`                                     | Override default container command (useful when using custom images)                                    | `[]`                     |
| `replica.args`                                        | Override default container args (useful when using custom images)                                       | `[]`                     |
| `replica.preExecCmds`                                 | Additional commands to run prior to starting Redis&reg; replicas                                        | `[]`                     |
| `replica.extraFlags`                                  | Array with additional command line flags for Redis&reg; replicas                                        | `[]`                     |
| `replica.extraEnvVars`                                | Array with extra environment variables to add to Redis&reg; replicas nodes                              | `[]`                     |
| `replica.extraEnvVarsCM`                              | Name of existing ConfigMap containing extra env vars for Redis&reg; replicas nodes                      | `""`                     |
| `replica.extraEnvVarsSecret`                          | Name of existing Secret containing extra env vars for Redis&reg; replicas nodes                         | `""`                     |
| `replica.externalMaster.enabled`                      | Use external master for bootstrapping                                                                   | `false`                  |
| `replica.externalMaster.host`                         | External master host to bootstrap from                                                                  | `""`                     |
| `replica.externalMaster.port`                         | Port for Redis service external master host                                                             | `6379`                   |
| `replica.containerPorts.redis`                        | Container port to open on Redis&reg; replicas nodes                                                     | `6379`                   |
| `replica.startupProbe.enabled`                        | Enable startupProbe on Redis&reg; replicas nodes                                                        | `true`                   |
| `replica.startupProbe.initialDelaySeconds`            | Initial delay seconds for startupProbe                                                                  | `10`                     |
| `replica.startupProbe.periodSeconds`                  | Period seconds for startupProbe                                                                         | `10`                     |
| `replica.startupProbe.timeoutSeconds`                 | Timeout seconds for startupProbe                                                                        | `5`                      |
| `replica.startupProbe.failureThreshold`               | Failure threshold for startupProbe                                                                      | `22`                     |
| `replica.startupProbe.successThreshold`               | Success threshold for startupProbe                                                                      | `1`                      |
| `replica.livenessProbe.enabled`                       | Enable livenessProbe on Redis&reg; replicas nodes                                                       | `true`                   |
| `replica.livenessProbe.initialDelaySeconds`           | Initial delay seconds for livenessProbe                                                                 | `20`                     |
| `replica.livenessProbe.periodSeconds`                 | Period seconds for livenessProbe                                                                        | `5`                      |
| `replica.livenessProbe.timeoutSeconds`                | Timeout seconds for livenessProbe                                                                       | `5`                      |
| `replica.livenessProbe.failureThreshold`              | Failure threshold for livenessProbe                                                                     | `5`                      |
| `replica.livenessProbe.successThreshold`              | Success threshold for livenessProbe                                                                     | `1`                      |
| `replica.readinessProbe.enabled`                      | Enable readinessProbe on Redis&reg; replicas nodes                                                      | `true`                   |
| `replica.readinessProbe.initialDelaySeconds`          | Initial delay seconds for readinessProbe                                                                | `20`                     |
| `replica.readinessProbe.periodSeconds`                | Period seconds for readinessProbe                                                                       | `5`                      |
| `replica.readinessProbe.timeoutSeconds`               | Timeout seconds for readinessProbe                                                                      | `1`                      |
| `replica.readinessProbe.failureThreshold`             | Failure threshold for readinessProbe                                                                    | `5`                      |
| `replica.readinessProbe.successThreshold`             | Success threshold for readinessProbe                                                                    | `1`                      |
| `replica.customStartupProbe`                          | Custom startupProbe that overrides the default one                                                      | `{}`                     |
| `replica.customLivenessProbe`                         | Custom livenessProbe that overrides the default one                                                     | `{}`                     |
| `replica.customReadinessProbe`                        | Custom readinessProbe that overrides the default one                                                    | `{}`                     |
| `replica.resources.limits`                            | The resources limits for the Redis&reg; replicas containers                                             | `{}`                     |
| `replica.resources.requests`                          | The requested resources for the Redis&reg; replicas containers                                          | `{}`                     |
| `replica.podSecurityContext.enabled`                  | Enabled Redis&reg; replicas pods' Security Context                                                      | `true`                   |
| `replica.podSecurityContext.fsGroup`                  | Set Redis&reg; replicas pod's Security Context fsGroup                                                  | `1001`                   |
| `replica.containerSecurityContext.enabled`            | Enabled Redis&reg; replicas containers' Security Context                                                | `true`                   |
| `replica.containerSecurityContext.runAsUser`          | Set Redis&reg; replicas containers' Security Context runAsUser                                          | `1001`                   |
| `replica.schedulerName`                               | Alternate scheduler for Redis&reg; replicas pods                                                        | `""`                     |
| `replica.updateStrategy.type`                         | Redis&reg; replicas statefulset strategy type                                                           | `RollingUpdate`          |
| `replica.minReadySeconds`                             | How many seconds a pod needs to be ready before killing the next, during update                         | `0`                      |
| `replica.priorityClassName`                           | Redis&reg; replicas pods' priorityClassName                                                             | `""`                     |
| `replica.podManagementPolicy`                         | podManagementPolicy to manage scaling operation of %%MAIN_CONTAINER_NAME%% pods                         | `""`                     |
| `replica.hostAliases`                                 | Redis&reg; replicas pods host aliases                                                                   | `[]`                     |
| `replica.podLabels`                                   | Extra labels for Redis&reg; replicas pods                                                               | `{}`                     |
| `replica.podAnnotations`                              | Annotations for Redis&reg; replicas pods                                                                | `{}`                     |
| `replica.shareProcessNamespace`                       | Share a single process namespace between all of the containers in Redis&reg; replicas pods              | `false`                  |
| `replica.podAffinityPreset`                           | Pod affinity preset. Ignored if `replica.affinity` is set. Allowed values: `soft` or `hard`             | `""`                     |
| `replica.podAntiAffinityPreset`                       | Pod anti-affinity preset. Ignored if `replica.affinity` is set. Allowed values: `soft` or `hard`        | `soft`                   |
| `replica.nodeAffinityPreset.type`                     | Node affinity preset type. Ignored if `replica.affinity` is set. Allowed values: `soft` or `hard`       | `""`                     |
| `replica.nodeAffinityPreset.key`                      | Node label key to match. Ignored if `replica.affinity` is set                                           | `""`                     |
| `replica.nodeAffinityPreset.values`                   | Node label values to match. Ignored if `replica.affinity` is set                                        | `[]`                     |
| `replica.affinity`                                    | Affinity for Redis&reg; replicas pods assignment                                                        | `{}`                     |
| `replica.nodeSelector`                                | Node labels for Redis&reg; replicas pods assignment                                                     | `{}`                     |
| `replica.tolerations`                                 | Tolerations for Redis&reg; replicas pods assignment                                                     | `[]`                     |
| `replica.topologySpreadConstraints`                   | Spread Constraints for Redis&reg; replicas pod assignment                                               | `[]`                     |
| `replica.dnsPolicy`                                   | DNS Policy for Redis&reg; replica pods                                                                  | `""`                     |
| `replica.dnsConfig`                                   | DNS Configuration for Redis&reg; replica pods                                                           | `{}`                     |
| `replica.lifecycleHooks`                              | for the Redis&reg; replica container(s) to automate configuration before or after startup               | `{}`                     |
| `replica.extraVolumes`                                | Optionally specify extra list of additional volumes for the Redis&reg; replicas pod(s)                  | `[]`                     |
| `replica.extraVolumeMounts`                           | Optionally specify extra list of additional volumeMounts for the Redis&reg; replicas container(s)       | `[]`                     |
| `replica.sidecars`                                    | Add additional sidecar containers to the Redis&reg; replicas pod(s)                                     | `[]`                     |
| `replica.initContainers`                              | Add additional init containers to the Redis&reg; replicas pod(s)                                        | `[]`                     |
| `replica.persistence.enabled`                         | Enable persistence on Redis&reg; replicas nodes using Persistent Volume Claims                          | `true`                   |
| `replica.persistence.medium`                          | Provide a medium for `emptyDir` volumes.                                                                | `""`                     |
| `replica.persistence.sizeLimit`                       | Set this to enable a size limit for `emptyDir` volumes.                                                 | `""`                     |
| `replica.persistence.path`                            | The path the volume will be mounted at on Redis&reg; replicas containers                                | `/data`                  |
| `replica.persistence.subPath`                         | The subdirectory of the volume to mount on Redis&reg; replicas containers                               | `""`                     |
| `replica.persistence.subPathExpr`                     | Used to construct the subPath subdirectory of the volume to mount on Redis&reg; replicas containers     | `""`                     |
| `replica.persistence.storageClass`                    | Persistent Volume storage class                                                                         | `""`                     |
| `replica.persistence.accessModes`                     | Persistent Volume access modes                                                                          | `["ReadWriteOnce"]`      |
| `replica.persistence.size`                            | Persistent Volume size                                                                                  | `8Gi`                    |
| `replica.persistence.annotations`                     | Additional custom annotations for the PVC                                                               | `{}`                     |
| `replica.persistence.selector`                        | Additional labels to match for the PVC                                                                  | `{}`                     |
| `replica.persistence.dataSource`                      | Custom PVC data source                                                                                  | `{}`                     |
| `replica.persistence.existingClaim`                   | Use a existing PVC which must be created manually before bound                                          | `""`                     |
| `replica.service.type`                                | Redis&reg; replicas service type                                                                        | `ClusterIP`              |
| `replica.service.ports.redis`                         | Redis&reg; replicas service port                                                                        | `6379`                   |
| `replica.service.nodePorts.redis`                     | Node port for Redis&reg; replicas                                                                       | `""`                     |
| `replica.service.externalTrafficPolicy`               | Redis&reg; replicas service external traffic policy                                                     | `Cluster`                |
| `replica.service.internalTrafficPolicy`               | Redis&reg; replicas service internal traffic policy (requires Kubernetes v1.22 or greater to be usable) | `Cluster`                |
| `replica.service.extraPorts`                          | Extra ports to expose (normally used with the `sidecar` value)                                          | `[]`                     |
| `replica.service.clusterIP`                           | Redis&reg; replicas service Cluster IP                                                                  | `""`                     |
| `replica.service.loadBalancerIP`                      | Redis&reg; replicas service Load Balancer IP                                                            | `""`                     |
| `replica.service.loadBalancerSourceRanges`            | Redis&reg; replicas service Load Balancer sources                                                       | `[]`                     |
| `replica.service.annotations`                         | Additional custom annotations for Redis&reg; replicas service                                           | `{}`                     |
| `replica.service.sessionAffinity`                     | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                    | `None`                   |
| `replica.service.sessionAffinityConfig`               | Additional settings for the sessionAffinity                                                             | `{}`                     |
| `replica.terminationGracePeriodSeconds`               | Integer setting the termination grace period for the redis-replicas pods                                | `30`                     |
| `replica.autoscaling.enabled`                         | Enable replica autoscaling settings                                                                     | `false`                  |
| `replica.autoscaling.minReplicas`                     | Minimum replicas for the pod autoscaling                                                                | `1`                      |
| `replica.autoscaling.maxReplicas`                     | Maximum replicas for the pod autoscaling                                                                | `11`                     |
| `replica.autoscaling.targetCPU`                       | Percentage of CPU to consider when autoscaling                                                          | `""`                     |
| `replica.autoscaling.targetMemory`                    | Percentage of Memory to consider when autoscaling                                                       | `""`                     |
| `replica.serviceAccount.create`                       | Specifies whether a ServiceAccount should be created                                                    | `false`                  |
| `replica.serviceAccount.name`                         | The name of the ServiceAccount to use.                                                                  | `""`                     |
| `replica.serviceAccount.automountServiceAccountToken` | Whether to auto mount the service account token                                                         | `true`                   |
| `replica.serviceAccount.annotations`                  | Additional custom annotations for the ServiceAccount                                                    | `{}`                     |


### Redis&reg; Sentinel configuration parameters

| Name                                          | Description                                                                                                                                 | Value                    |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `sentinel.enabled`                            | Use Redis&reg; Sentinel on Redis&reg; pods.                                                                                                 | `false`                  |
| `sentinel.image.registry`                     | Redis&reg; Sentinel image registry                                                                                                          | `docker.io`              |
| `sentinel.image.repository`                   | Redis&reg; Sentinel image repository                                                                                                        | `bitnami/redis-sentinel` |
| `sentinel.image.tag`                          | Redis&reg; Sentinel image tag (immutable tags are recommended)                                                                              | `7.0.7-debian-11-r10`    |
| `sentinel.image.digest`                       | Redis&reg; Sentinel image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag                         | `""`                     |
| `sentinel.image.pullPolicy`                   | Redis&reg; Sentinel image pull policy                                                                                                       | `IfNotPresent`           |
| `sentinel.image.pullSecrets`                  | Redis&reg; Sentinel image pull secrets                                                                                                      | `[]`                     |
| `sentinel.image.debug`                        | Enable image debug mode                                                                                                                     | `false`                  |
| `sentinel.masterSet`                          | Master set name                                                                                                                             | `mymaster`               |
| `sentinel.quorum`                             | Sentinel Quorum                                                                                                                             | `2`                      |
| `sentinel.getMasterTimeout`                   | Amount of time to allow before get_sentinel_master_info() times out.                                                                        | `220`                    |
| `sentinel.automateClusterRecovery`            | Automate cluster recovery in cases where the last replica is not considered a good replica and Sentinel won't automatically failover to it. | `false`                  |
| `sentinel.redisShutdownWaitFailover`          | Whether the Redis&reg; master container waits for the failover at shutdown (in addition to the Redis&reg; Sentinel container).              | `true`                   |
| `sentinel.downAfterMilliseconds`              | Timeout for detecting a Redis&reg; node is down                                                                                             | `60000`                  |
| `sentinel.failoverTimeout`                    | Timeout for performing a election failover                                                                                                  | `180000`                 |
| `sentinel.parallelSyncs`                      | Number of replicas that can be reconfigured in parallel to use the new master after a failover                                              | `1`                      |
| `sentinel.configuration`                      | Configuration for Redis&reg; Sentinel nodes                                                                                                 | `""`                     |
| `sentinel.command`                            | Override default container command (useful when using custom images)                                                                        | `[]`                     |
| `sentinel.args`                               | Override default container args (useful when using custom images)                                                                           | `[]`                     |
| `sentinel.preExecCmds`                        | Additional commands to run prior to starting Redis&reg; Sentinel                                                                            | `[]`                     |
| `sentinel.extraEnvVars`                       | Array with extra environment variables to add to Redis&reg; Sentinel nodes                                                                  | `[]`                     |
| `sentinel.extraEnvVarsCM`                     | Name of existing ConfigMap containing extra env vars for Redis&reg; Sentinel nodes                                                          | `""`                     |
| `sentinel.extraEnvVarsSecret`                 | Name of existing Secret containing extra env vars for Redis&reg; Sentinel nodes                                                             | `""`                     |
| `sentinel.externalMaster.enabled`             | Use external master for bootstrapping                                                                                                       | `false`                  |
| `sentinel.externalMaster.host`                | External master host to bootstrap from                                                                                                      | `""`                     |
| `sentinel.externalMaster.port`                | Port for Redis service external master host                                                                                                 | `6379`                   |
| `sentinel.containerPorts.sentinel`            | Container port to open on Redis&reg; Sentinel nodes                                                                                         | `26379`                  |
| `sentinel.startupProbe.enabled`               | Enable startupProbe on Redis&reg; Sentinel nodes                                                                                            | `true`                   |
| `sentinel.startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                                                                                                      | `10`                     |
| `sentinel.startupProbe.periodSeconds`         | Period seconds for startupProbe                                                                                                             | `10`                     |
| `sentinel.startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                                                                                            | `5`                      |
| `sentinel.startupProbe.failureThreshold`      | Failure threshold for startupProbe                                                                                                          | `22`                     |
| `sentinel.startupProbe.successThreshold`      | Success threshold for startupProbe                                                                                                          | `1`                      |
| `sentinel.livenessProbe.enabled`              | Enable livenessProbe on Redis&reg; Sentinel nodes                                                                                           | `true`                   |
| `sentinel.livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                                                                                     | `20`                     |
| `sentinel.livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                                                                                            | `5`                      |
| `sentinel.livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                                                                                           | `5`                      |
| `sentinel.livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                                                                                         | `5`                      |
| `sentinel.livenessProbe.successThreshold`     | Success threshold for livenessProbe                                                                                                         | `1`                      |
| `sentinel.readinessProbe.enabled`             | Enable readinessProbe on Redis&reg; Sentinel nodes                                                                                          | `true`                   |
| `sentinel.readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                                                                                                    | `20`                     |
| `sentinel.readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                                                                                           | `5`                      |
| `sentinel.readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                                                                                          | `1`                      |
| `sentinel.readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                                                                                        | `5`                      |
| `sentinel.readinessProbe.successThreshold`    | Success threshold for readinessProbe                                                                                                        | `1`                      |
| `sentinel.customStartupProbe`                 | Custom startupProbe that overrides the default one                                                                                          | `{}`                     |
| `sentinel.customLivenessProbe`                | Custom livenessProbe that overrides the default one                                                                                         | `{}`                     |
| `sentinel.customReadinessProbe`               | Custom readinessProbe that overrides the default one                                                                                        | `{}`                     |
| `sentinel.persistence.enabled`                | Enable persistence on Redis&reg; sentinel nodes using Persistent Volume Claims (Experimental)                                               | `false`                  |
| `sentinel.persistence.storageClass`           | Persistent Volume storage class                                                                                                             | `""`                     |
| `sentinel.persistence.accessModes`            | Persistent Volume access modes                                                                                                              | `["ReadWriteOnce"]`      |
| `sentinel.persistence.size`                   | Persistent Volume size                                                                                                                      | `100Mi`                  |
| `sentinel.persistence.annotations`            | Additional custom annotations for the PVC                                                                                                   | `{}`                     |
| `sentinel.persistence.selector`               | Additional labels to match for the PVC                                                                                                      | `{}`                     |
| `sentinel.persistence.dataSource`             | Custom PVC data source                                                                                                                      | `{}`                     |
| `sentinel.persistence.medium`                 | Provide a medium for `emptyDir` volumes.                                                                                                    | `""`                     |
| `sentinel.persistence.sizeLimit`              | Set this to enable a size limit for `emptyDir` volumes.                                                                                     | `""`                     |
| `sentinel.resources.limits`                   | The resources limits for the Redis&reg; Sentinel containers                                                                                 | `{}`                     |
| `sentinel.resources.requests`                 | The requested resources for the Redis&reg; Sentinel containers                                                                              | `{}`                     |
| `sentinel.containerSecurityContext.enabled`   | Enabled Redis&reg; Sentinel containers' Security Context                                                                                    | `true`                   |
| `sentinel.containerSecurityContext.runAsUser` | Set Redis&reg; Sentinel containers' Security Context runAsUser                                                                              | `1001`                   |
| `sentinel.lifecycleHooks`                     | for the Redis&reg; sentinel container(s) to automate configuration before or after startup                                                  | `{}`                     |
| `sentinel.extraVolumes`                       | Optionally specify extra list of additional volumes for the Redis&reg; Sentinel                                                             | `[]`                     |
| `sentinel.extraVolumeMounts`                  | Optionally specify extra list of additional volumeMounts for the Redis&reg; Sentinel container(s)                                           | `[]`                     |
| `sentinel.service.type`                       | Redis&reg; Sentinel service type                                                                                                            | `ClusterIP`              |
| `sentinel.service.ports.redis`                | Redis&reg; service port for Redis&reg;                                                                                                      | `6379`                   |
| `sentinel.service.ports.sentinel`             | Redis&reg; service port for Redis&reg; Sentinel                                                                                             | `26379`                  |
| `sentinel.service.nodePorts.redis`            | Node port for Redis&reg;                                                                                                                    | `""`                     |
| `sentinel.service.nodePorts.sentinel`         | Node port for Sentinel                                                                                                                      | `""`                     |
| `sentinel.service.externalTrafficPolicy`      | Redis&reg; Sentinel service external traffic policy                                                                                         | `Cluster`                |
| `sentinel.service.extraPorts`                 | Extra ports to expose (normally used with the `sidecar` value)                                                                              | `[]`                     |
| `sentinel.service.clusterIP`                  | Redis&reg; Sentinel service Cluster IP                                                                                                      | `""`                     |
| `sentinel.service.loadBalancerIP`             | Redis&reg; Sentinel service Load Balancer IP                                                                                                | `""`                     |
| `sentinel.service.loadBalancerSourceRanges`   | Redis&reg; Sentinel service Load Balancer sources                                                                                           | `[]`                     |
| `sentinel.service.annotations`                | Additional custom annotations for Redis&reg; Sentinel service                                                                               | `{}`                     |
| `sentinel.service.sessionAffinity`            | Session Affinity for Kubernetes service, can be "None" or "ClientIP"                                                                        | `None`                   |
| `sentinel.service.sessionAffinityConfig`      | Additional settings for the sessionAffinity                                                                                                 | `{}`                     |
| `sentinel.terminationGracePeriodSeconds`      | Integer setting the termination grace period for the redis-node pods                                                                        | `30`                     |


### Other Parameters

| Name                                          | Description                                                                                                                                 | Value   |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `networkPolicy.enabled`                       | Enable creation of NetworkPolicy resources                                                                                                  | `false` |
| `networkPolicy.allowExternal`                 | Don't require client label for connections                                                                                                  | `true`  |
| `networkPolicy.extraIngress`                  | Add extra ingress rules to the NetworkPolicy                                                                                                | `[]`    |
| `networkPolicy.extraEgress`                   | Add extra egress rules to the NetworkPolicy                                                                                                 | `[]`    |
| `networkPolicy.ingressNSMatchLabels`          | Labels to match to allow traffic from other namespaces                                                                                      | `{}`    |
| `networkPolicy.ingressNSPodMatchLabels`       | Pod labels to match to allow traffic from other namespaces                                                                                  | `{}`    |
| `podSecurityPolicy.create`                    | Whether to create a PodSecurityPolicy. WARNING: PodSecurityPolicy is deprecated in Kubernetes v1.21 or later, unavailable in v1.25 or later | `false` |
| `podSecurityPolicy.enabled`                   | Enable PodSecurityPolicy's RBAC rules                                                                                                       | `false` |
| `rbac.create`                                 | Specifies whether RBAC resources should be created                                                                                          | `false` |
| `rbac.rules`                                  | Custom RBAC rules to set                                                                                                                    | `[]`    |
| `serviceAccount.create`                       | Specifies whether a ServiceAccount should be created                                                                                        | `true`  |
| `serviceAccount.name`                         | The name of the ServiceAccount to use.                                                                                                      | `""`    |
| `serviceAccount.automountServiceAccountToken` | Whether to auto mount the service account token                                                                                             | `true`  |
| `serviceAccount.annotations`                  | Additional custom annotations for the ServiceAccount                                                                                        | `{}`    |
| `pdb.create`                                  | Specifies whether a PodDisruptionBudget should be created                                                                                   | `false` |
| `pdb.minAvailable`                            | Min number of pods that must still be available after the eviction                                                                          | `1`     |
| `pdb.maxUnavailable`                          | Max number of pods that can be unavailable after the eviction                                                                               | `""`    |
| `tls.enabled`                                 | Enable TLS traffic                                                                                                                          | `false` |
| `tls.authClients`                             | Require clients to authenticate                                                                                                             | `true`  |
| `tls.autoGenerated`                           | Enable autogenerated certificates                                                                                                           | `false` |
| `tls.existingSecret`                          | The name of the existing secret that contains the TLS certificates                                                                          | `""`    |
| `tls.certificatesSecret`                      | DEPRECATED. Use existingSecret instead.                                                                                                     | `""`    |
| `tls.certFilename`                            | Certificate filename                                                                                                                        | `""`    |
| `tls.certKeyFilename`                         | Certificate Key filename                                                                                                                    | `""`    |
| `tls.certCAFilename`                          | CA Certificate filename                                                                                                                     | `""`    |
| `tls.dhParamsFilename`                        | File containing DH params (in order to support DH based ciphers)                                                                            | `""`    |


### Metrics Parameters

| Name                                         | Description                                                                                                         | Value                    |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `metrics.enabled`                            | Start a sidecar prometheus exporter to expose Redis&reg; metrics                                                    | `false`                  |
| `metrics.image.registry`                     | Redis&reg; Exporter image registry                                                                                  | `docker.io`              |
| `metrics.image.repository`                   | Redis&reg; Exporter image repository                                                                                | `bitnami/redis-exporter` |
| `metrics.image.tag`                          | Redis&reg; Exporter image tag (immutable tags are recommended)                                                      | `1.45.0-debian-11-r26`   |
| `metrics.image.digest`                       | Redis&reg; Exporter image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                     |
| `metrics.image.pullPolicy`                   | Redis&reg; Exporter image pull policy                                                                               | `IfNotPresent`           |
| `metrics.image.pullSecrets`                  | Redis&reg; Exporter image pull secrets                                                                              | `[]`                     |
| `metrics.startupProbe.enabled`               | Enable startupProbe on Redis&reg; replicas nodes                                                                    | `false`                  |
| `metrics.startupProbe.initialDelaySeconds`   | Initial delay seconds for startupProbe                                                                              | `10`                     |
| `metrics.startupProbe.periodSeconds`         | Period seconds for startupProbe                                                                                     | `10`                     |
| `metrics.startupProbe.timeoutSeconds`        | Timeout seconds for startupProbe                                                                                    | `5`                      |
| `metrics.startupProbe.failureThreshold`      | Failure threshold for startupProbe                                                                                  | `5`                      |
| `metrics.startupProbe.successThreshold`      | Success threshold for startupProbe                                                                                  | `1`                      |
| `metrics.livenessProbe.enabled`              | Enable livenessProbe on Redis&reg; replicas nodes                                                                   | `true`                   |
| `metrics.livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                                                             | `10`                     |
| `metrics.livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                                                                    | `10`                     |
| `metrics.livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                                                                   | `5`                      |
| `metrics.livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                                                                 | `5`                      |
| `metrics.livenessProbe.successThreshold`     | Success threshold for livenessProbe                                                                                 | `1`                      |
| `metrics.readinessProbe.enabled`             | Enable readinessProbe on Redis&reg; replicas nodes                                                                  | `true`                   |
| `metrics.readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                                                                            | `5`                      |
| `metrics.readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                                                                   | `10`                     |
| `metrics.readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                                                                  | `1`                      |
| `metrics.readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                                                                | `3`                      |
| `metrics.readinessProbe.successThreshold`    | Success threshold for readinessProbe                                                                                | `1`                      |
| `metrics.customStartupProbe`                 | Custom startupProbe that overrides the default one                                                                  | `{}`                     |
| `metrics.customLivenessProbe`                | Custom livenessProbe that overrides the default one                                                                 | `{}`                     |
| `metrics.customReadinessProbe`               | Custom readinessProbe that overrides the default one                                                                | `{}`                     |
| `metrics.command`                            | Override default metrics container init command (useful when using custom images)                                   | `[]`                     |
| `metrics.redisTargetHost`                    | A way to specify an alternative Redis&reg; hostname                                                                 | `localhost`              |
| `metrics.extraArgs`                          | Extra arguments for Redis&reg; exporter, for example:                                                               | `{}`                     |
| `metrics.extraEnvVars`                       | Array with extra environment variables to add to Redis&reg; exporter                                                | `[]`                     |
| `metrics.containerSecurityContext.enabled`   | Enabled Redis&reg; exporter containers' Security Context                                                            | `true`                   |
| `metrics.containerSecurityContext.runAsUser` | Set Redis&reg; exporter containers' Security Context runAsUser                                                      | `1001`                   |
| `metrics.extraVolumes`                       | Optionally specify extra list of additional volumes for the Redis&reg; metrics sidecar                              | `[]`                     |
| `metrics.extraVolumeMounts`                  | Optionally specify extra list of additional volumeMounts for the Redis&reg; metrics sidecar                         | `[]`                     |
| `metrics.resources.limits`                   | The resources limits for the Redis&reg; exporter container                                                          | `{}`                     |
| `metrics.resources.requests`                 | The requested resources for the Redis&reg; exporter container                                                       | `{}`                     |
| `metrics.podLabels`                          | Extra labels for Redis&reg; exporter pods                                                                           | `{}`                     |
| `metrics.podAnnotations`                     | Annotations for Redis&reg; exporter pods                                                                            | `{}`                     |
| `metrics.service.type`                       | Redis&reg; exporter service type                                                                                    | `ClusterIP`              |
| `metrics.service.port`                       | Redis&reg; exporter service port                                                                                    | `9121`                   |
| `metrics.service.externalTrafficPolicy`      | Redis&reg; exporter service external traffic policy                                                                 | `Cluster`                |
| `metrics.service.extraPorts`                 | Extra ports to expose (normally used with the `sidecar` value)                                                      | `[]`                     |
| `metrics.service.loadBalancerIP`             | Redis&reg; exporter service Load Balancer IP                                                                        | `""`                     |
| `metrics.service.loadBalancerSourceRanges`   | Redis&reg; exporter service Load Balancer sources                                                                   | `[]`                     |
| `metrics.service.annotations`                | Additional custom annotations for Redis&reg; exporter service                                                       | `{}`                     |
| `metrics.serviceMonitor.enabled`             | Create ServiceMonitor resource(s) for scraping metrics using PrometheusOperator                                     | `false`                  |
| `metrics.serviceMonitor.namespace`           | The namespace in which the ServiceMonitor will be created                                                           | `""`                     |
| `metrics.serviceMonitor.interval`            | The interval at which metrics should be scraped                                                                     | `30s`                    |
| `metrics.serviceMonitor.scrapeTimeout`       | The timeout after which the scrape is ended                                                                         | `""`                     |
| `metrics.serviceMonitor.relabellings`        | Metrics RelabelConfigs to apply to samples before scraping.                                                         | `[]`                     |
| `metrics.serviceMonitor.metricRelabelings`   | Metrics RelabelConfigs to apply to samples before ingestion.                                                        | `[]`                     |
| `metrics.serviceMonitor.honorLabels`         | Specify honorLabels parameter to add the scrape endpoint                                                            | `false`                  |
| `metrics.serviceMonitor.additionalLabels`    | Additional labels that can be used so ServiceMonitor resource(s) can be discovered by Prometheus                    | `{}`                     |
| `metrics.serviceMonitor.podTargetLabels`     | Labels from the Kubernetes pod to be transferred to the created metrics                                             | `[]`                     |
| `metrics.prometheusRule.enabled`             | Create a custom prometheusRule Resource for scraping metrics using PrometheusOperator                               | `false`                  |
| `metrics.prometheusRule.namespace`           | The namespace in which the prometheusRule will be created                                                           | `""`                     |
| `metrics.prometheusRule.additionalLabels`    | Additional labels for the prometheusRule                                                                            | `{}`                     |
| `metrics.prometheusRule.rules`               | Custom Prometheus rules                                                                                             | `[]`                     |


### Init Container Parameters

| Name                                                   | Description                                                                                                   | Value                   |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- | ----------------------- |
| `volumePermissions.enabled`                            | Enable init container that changes the owner/group of the PV mount point to `runAsUser:fsGroup`               | `false`                 |
| `volumePermissions.image.registry`                     | Bitnami Shell image registry                                                                                  | `docker.io`             |
| `volumePermissions.image.repository`                   | Bitnami Shell image repository                                                                                | `bitnami/bitnami-shell` |
| `volumePermissions.image.tag`                          | Bitnami Shell image tag (immutable tags are recommended)                                                      | `11-debian-11-r72`      |
| `volumePermissions.image.digest`                       | Bitnami Shell image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                    |
| `volumePermissions.image.pullPolicy`                   | Bitnami Shell image pull policy                                                                               | `IfNotPresent`          |
| `volumePermissions.image.pullSecrets`                  | Bitnami Shell image pull secrets                                                                              | `[]`                    |
| `volumePermissions.resources.limits`                   | The resources limits for the init container                                                                   | `{}`                    |
| `volumePermissions.resources.requests`                 | The requested resources for the init container                                                                | `{}`                    |
| `volumePermissions.containerSecurityContext.runAsUser` | Set init container's Security Context runAsUser                                                               | `0`                     |
| `sysctl.enabled`                                       | Enable init container to modify Kernel settings                                                               | `false`                 |
| `sysctl.image.registry`                                | Bitnami Shell image registry                                                                                  | `docker.io`             |
| `sysctl.image.repository`                              | Bitnami Shell image repository                                                                                | `bitnami/bitnami-shell` |
| `sysctl.image.tag`                                     | Bitnami Shell image tag (immutable tags are recommended)                                                      | `11-debian-11-r72`      |
| `sysctl.image.digest`                                  | Bitnami Shell image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag | `""`                    |
| `sysctl.image.pullPolicy`                              | Bitnami Shell image pull policy                                                                               | `IfNotPresent`          |
| `sysctl.image.pullSecrets`                             | Bitnami Shell image pull secrets                                                                              | `[]`                    |
| `sysctl.command`                                       | Override default init-sysctl container command (useful when using custom images)                              | `[]`                    |
| `sysctl.mountHostSys`                                  | Mount the host `/sys` folder to `/host-sys`                                                                   | `false`                 |
| `sysctl.resources.limits`                              | The resources limits for the init container                                                                   | `{}`                    |
| `sysctl.resources.requests`                            | The requested resources for the init container                                                                | `{}`                    |


### useExternalDNS Parameters

| Name                                   | Description                                                                                                                              | Value                               |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `useExternalDNS.enabled`               | Enable various syntax that would enable external-dns to work.  Note this requires a working installation of `external-dns` to be usable. | `false`                             |
| `useExternalDNS.additionalAnnotations` | Extra annotations to be utilized when `external-dns` is enabled.                                                                         | `{}`                                |
| `useExternalDNS.annotationKey`         | The annotation key utilized when `external-dns` is enabled. Setting this to `false` will disable annotations.                            | `external-dns.alpha.kubernetes.io/` |
| `useExternalDNS.suffix`                | The DNS suffix utilized when `external-dns` is enabled.  Note that we prepend the suffix with the full name of the release.              | `""`                                |


