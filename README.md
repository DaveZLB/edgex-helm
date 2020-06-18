# EdgeX Foundry on Kubernetes

A [Helm](https://helm.sh/) chart to easily deploy the EdgeX IoT project on Kubernetes.
Based on EdgeX [Geneva](https://github.com/edgexfoundry/developer-scripts/tree/master/releases/geneva/compose-files) version.

## Prerequisites

- Kubernetes cluster 1.10+
- [Helm](https://helm.sh/) 2.8.0+

## Installation

Install the EdgeX helm chart with a release name edgex-geneva

- helm2

```
$ git clone https://github.com/DaveZLB/edgex-kubernetes-support.git
$ helm install --name edgex-geneva edgex-kubernetes-support
```

- helm3

```bash
$ git clone https://github.com/DaveZLB/edgex-kubernetes-support.git
$ helm install edgex-geneva edgex-kubernetes-support
```

## Uninstallation

- helm2

```bash
helm delete edgex-geneva --purge
```

- helm3

```bash
helm uninstall edgex-geneva
```

- **Test EdgeX**

You can test whether the Edgex services start successfully
```$xslt
$ curl http://localhost:48080/api/v1/ping
$ curl http://localhost:48081/api/v1/ping
$ curl http://localhost:48082/api/v1/ping
$ curl http://localhost:48060/api/v1/ping
$ curl http://localhost:48085/api/v1/ping
```

- **Access EdgeX UI**

With a modern browser, navigate to http://localhost:4000
Use details see [EdgeX UI doc](https://github.com/edgexfoundry/edgex-ui-go)

## Tips

- This project is based on [docker-compose-geneva-redis-no-secty.yml](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/geneva/compose-files/docker-compose-geneva-redis-no-secty.yml),
you can implement your customized version based on this.
- Since the EdgeX pods communicates with each other through the kubernetes service name, make sure the kubernetes DNS is enabled.
- Since other edgex services need to rely on consul to obtain configuration or register themselves to consul, other services cannot run normally until consul starts successfully.
- Unlike the docker-compose files for this release (which use a separate Docker volume container), the manifest files mount host based volumes as follows:

1、edgex-core-consul's /consul/config directory is mapped to the host's /mnt/edgex-consul-config directory.

2、edgex-core-consul's /consul/data directory is mapped to the host's /mnt/edgex-consul-data directory.

3、edgex-mongo's /data/db directory is mapped to the host's /mnt/edgex-mongo directory.

4、edgex-support-logging's /edgex/logs directory is mapped to the host's /mnt/edgex-support-logging directory.

## Some articles about deploying edgex to kubernetes

- VMware China R&D Center
https://mp.weixin.qq.com/s/ECdEkc9QdkVScn4Lvl_JJA

## Feedback

If you find a bug or want to request a new feature, please open a [GitHub Issue](https://github.com/DaveZLB/edgex-kubernetes-support/issues)


