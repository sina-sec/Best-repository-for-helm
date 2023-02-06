# Sentry

![68747470733a2f2f676f7265706f7274636172642e636f6d2f62616467652f6769746875622e636f6d2f68656c6d2f68656c6d](https://user-images.githubusercontent.com/62883434/212608170-ef5e9227-6f58-4659-a4bb-aa6b0ca93610.svg) ![68747470733a2f2f696d672e736869656c64732e696f2f7374617469632f76313f6c6162656c3d676f646f63266d6573736167653d7265666572656e636526636f6c6f723d626c7565](https://user-images.githubusercontent.com/62883434/212608189-8cbd6a04-ea00-40e4-8af5-e82ea974273c.svg)
![68747470733a2f2f636972636c6563692e636f6d2f67682f68656c6d2f68656c6d2e7376673f7374796c653d736869656c64](https://user-images.githubusercontent.com/62883434/212608207-3d521ff6-9e76-4215-8905-6a7a24f4b309.svg)
![68747470733a2f2f626573747072616374696365732e636f7265696e6672617374727563747572652e6f72672f70726f6a656374732f333133312f6261646765](https://user-images.githubusercontent.com/62883434/212608216-8b2c5e08-4ae6-496a-8d73-dfcb66ea5149.svg) [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/bitnami)](https://artifacthub.io/packages/search?repo=bitnami)

![sentry1](https://user-images.githubusercontent.com/62883434/216895869-4b72782c-5f86-4358-be26-53f546ab4213.png)

## Install 

#### First, you should add the repository 


```
helm repo add sentry https://sentry-kubernetes.github.io/charts
```
### After that, you can install sentry with default values or use specific configuration with values ( You can use the values set in this repository, the settings in this repository are standard )


## Without overrides

```
helm install sentry sentry/sentry
```
## With your own values file

```
helm install sentry sentry/sentry -f values.yaml
```
## Configuration

The following table lists the configurable parameters of the Sentry chart and their default values.

Note: this table is incomplete, so have a look at the values.yaml in case you miss something

| Parameter                                     | Description                                                                                                                                                         | Default                        |
| :-------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------- |
| `user.create`                                 | if `true`, creates a default admin user defined from `email` and `password`                                                                                         | `true`                         |
| `user.email`                                  | Admin user email                                                                                                                                                    | `admin@sentry.local`           |
| `user.password`                               | Admin user password                                                                                                                                                 | `aaaa`                         |
| `ingress.enabled`                             | Enabling Ingress                                                                                                                                                    | `false`                        |
| `ingress.regexPathStyle`                      | Allows setting the style the regex paths are rendered in the ingress for the ingress controller in use. Possible values are `nginx`, `aws-alb`, `gke` and `traefik` | `nginx`                        |
| `nginx.enabled`                               | Enabling NGINX                                                                                                                                                      | `true`                         |
| `metrics.enabled`                             | if `true`, enable Prometheus metrics                                                                                                                                | `false`                        |
| `metrics.image.repository`                    | Metrics exporter image repository                                                                                                                                   | `prom/statsd-exporter`         |
| `metrics.image.tag`                           | Metrics exporter image tag                                                                                                                                          | `v0.10.5`                      |
| `metrics.image.PullPolicy`                    | Metrics exporter image pull policy                                                                                                                                  | `IfNotPresent`                 |
| `metrics.nodeSelector`                        | Node labels for metrics pod assignment                                                                                                                              | `{}`                           |
| `metrics.tolerations`                         | Toleration labels for metrics pod assignment                                                                                                                        | `[]`                           |
| `metrics.affinity`                            | Affinity settings for metrics                                                                                                                                       | `{}`                           |
| `metrics.resources`                           | Metrics resource requests/limit                                                                                                                                     | `{}`                           |
| `metrics.service.annotations`                 | annotations for Prometheus metrics service                                                                                                                          | `{}`                           |
| `metrics.service.clusterIP`                   | cluster IP address to assign to service (set to `"-"` to pass an empty value)                                                                                       | `nil`                          |
| `metrics.service.omitClusterIP`               | (Deprecated) To omit the `clusterIP` from the metrics service                                                                                                       | `false`                        |
| `metrics.service.externalIPs`                 | Prometheus metrics service external IP addresses                                                                                                                    | `[]`                           |
| `metrics.service.additionalLabels`            | labels for metrics service                                                                                                                                          | `{}`                           |
| `metrics.service.loadBalancerIP`              | IP address to assign to load balancer (if supported)                                                                                                                | `""`                           |
| `metrics.service.loadBalancerSourceRanges`    | list of IP CIDRs allowed access to load balancer (if supported)                                                                                                     | `[]`                           |
| `metrics.service.servicePort`                 | Prometheus metrics service port                                                                                                                                     | `9913`                         |
| `metrics.service.type`                        | type of Prometheus metrics service to create                                                                                                                        | `ClusterIP`                    |
| `metrics.serviceMonitor.enabled`              | Set this to `true` to create ServiceMonitor for Prometheus operator                                                                                                 | `false`                        |
| `metrics.serviceMonitor.additionalLabels`     | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus                                                                               | `{}`                           |
| `metrics.serviceMonitor.honorLabels`          | honorLabels chooses the metric's labels on collisions with target labels.                                                                                           | `false`                        |
| `metrics.serviceMonitor.namespace`            | namespace where servicemonitor resource should be created                                                                                                           | `the same namespace as sentry` |
| `metrics.serviceMonitor.scrapeInterval`       | interval between Prometheus scraping                                                                                                                                | `30s`                          |
| `serviceAccount.annotations`                  | Additional Service Account annotations.                                                                                                                             | `{}`                           |
| `serviceAccount.enabled`                      | If `true`, a custom Service Account will be used.                                                                                                                   | `false`                        |
| `serviceAccount.name`                         | The base name of the ServiceAccount to use. Will be appended with e.g. `snuba` or `web` for the pods accordingly.                                                   | `"sentry"`                     |
| `serviceAccount.automountServiceAccountToken` | Automount API credentials for a Service Account.                                                                                                                    | `true`                         |
| `sentry.existingSecret`                       | Existing kubernetes secret to be used for secret key for the session cookie ([documentation](https://develop.sentry.dev/config/#general))                                                                     | `nil`                          |
| `sentry.features.vstsLimitedScopes`           | Disables the azdo-integrations with limited scopes that is the cause of so much pain                                                                                | `true`                         |
| `sentry.web.customCA.secretName`              | Allows mounting a custom CA secret                                                                                                                                  | `nil`                          |
| `sentry.web.customCA.item`                    | Key of CA cert object within the secret                                                                                                                             | `ca.crt`                       |
| `symbolicator.api.enabled`                    | Enable Symbolicator                                                                                                                                                 | `false`                        |
| `symbolicator.api.config`                     | Config file for Symbolicator, see [its docs](https://getsentry.github.io/symbolicator/#configuration)                                                               | see values.yaml                |
