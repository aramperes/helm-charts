# CTFd Helm Chart

[CTFd](https://github.com/CTFd/CTFd) is a Capture The Flag framework focusing on ease of use and customizability.
It comes with everything you need to run a CTF and it's easy to customize with plugins and themes.

## Chart Details

This chart will install an instance of CTFd, with the possibility of persisting uploads using a PersistentVolumeClaim,
and persisting CTF data through an external SQL database and Redis for cache.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add momoperes https://charts.momoperes.ca
$ helm install --name my-release momoperes/ctfd
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of this chart and their default values

| Parameter                                 | Description                                             | Default                                                    |
| ----------------------------------------- | ------------------------------------------------------- | ---------------------------------------------------------- |
| replicaCount                              | Number of instances                                     | 1                                                          |
| image.repository                          | Repository name                                         | ctfd/ctfd                                                  |
| image.tag                                 | Repository tag                                          | mark-2.1.5                                                 |
| image.pullPolicy                          | Repository pull policy                                  | IfNotPresent                                               |
| persistence.uploads.enabled               | Enable persistence for uploads                          | false                                                      |
| persistence.uploads.accessMode            | Access policy for the PersistentVolumeClaim             | ReadWriteOnce                                                      |
| persistence.uploads.size                  | Size of the PersistentVolumeClaim                       | 1Gi                                                      |
| persistence.uploads.labels                | Additional labels for the PersistentVolumeClaim         | nil                                                      |
| persistence.uploads.name                  | Override the name of the PersistentVolumeClaim          | nil                                                      |
| persistence.uploads.storageClass          | StorageClass of the PersistentVolumeClaim               | nil                                                      |
| persistence.uploads.existingClaim         | Name of an existing PersistentVolumeClaim               | nil                                                        |
| env.open.WORKERS                          | Amount of CTFd workers                                  | 1                                                        |
| env.open.DATABASE_URL                     | URI to an SQL database                                  | nil                                                        |
| env.open.REDIS_URL                        | URI to a Redis database                                 | nil                                                        |
| env.secret.DATABASE_URL                   | URI to an SQL database                                  | nil                                                        |
| env.secret.REDIS_URL                      | URI to a Redis database                                 | nil                                                        |
| env.existingSecret                        | Name of the existing secret to use values from          | nil                                                        |
| env.existingSecretMappings.DATABASE_URL   | Key name in the secret for the SQL database URI         | nil                                                        |
| env.existingSecretMappings.REDIS_URL      | Key name in the secret for the Redis database URI       | nil                                                        |
| service.type                              | Type of service                                         | ClusterIP                                                  |
| service.port                              | Port for the service (http)                             | 80                                                       |
| ingress.enabled                           | Enable ingress controller resource                      | false                                                       |
| ingress.annotations                       | Ingress annotations                                     | {}                                                       |
| ingress.hosts                             | Ingress labels                                          | *See values.yaml*                                                       |
| ingress.tls                               | Ingress TLS settings                                    | []                                                       |
| resources                                 | Pod resources                                           | {}                                                         |
| nodeSelector                              | Pod node selector                                       | {}                                                         |
| tolerations                               | Pod tolerations                                         | []                                                         |
| affinity                                  | Pod affinity                                            | {}                                                         |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml momoperes/ctfd
```
> **Tip**: You can use the default [values.yaml](values.yaml)
