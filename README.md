# EdgeX Foundry on Kubernetes

A [Helm](https://helm.sh/) chart to easily deploy the EdgeX IoT project on Kubernetes.
Based on EdgeX [Geneva](https://github.com/edgexfoundry/developer-scripts/tree/master/releases/geneva/compose-files) version.

## Prerequisites

- Kubernetes cluster 1.10+
- [Helm](https://helm.sh/) 2.8.0+

## Installation

Install the EdgeX helm chart with a release name edgex-geneva

- helm2

```bash
$ git clone https://github.com/DaveZLB/edgex-helm.git
$ helm install --name edgex-geneva edgex-helm
```

- helm3

```bash
$ git clone https://github.com/DaveZLB/edgex-helm.git
$ helm install edgex-geneva edgex-helm
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

## Test EdgeX

EdgeX on kubernetes using NodePort type to expose services by default,You can use ping command to test whether the EdgeX services start successfully.

The ping command format:
```bash
http://{NodeIP}:{NodePort}/api/v1/ping

```
For example, the edgex-core-data ping command format:

```bash
curl http://localhost:30080/api/v1/ping
```


## Access EdgeX UI

With a modern browser, navigate to http://localhost:30400.

Use details see [EdgeX UI doc](https://github.com/edgexfoundry/edgex-ui-go)

## Tips

- This project is based on [docker-compose-geneva-redis-no-secty.yml](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/geneva/compose-files/docker-compose-geneva-redis-no-secty.yml),
you can implement your customized version based on this.
- Since the EdgeX pods communicates with each other through the kubernetes service name, make sure the kubernetes DNS is enabled.
- Since other edgex services need to rely on consul to obtain configuration or register themselves to consul, other services cannot run normally until consul starts successfully.
- Unlike the docker-compose files for this release (which use a separate Docker volume container), the manifest files mount host based volumes as follows:

1、edgex-core-consul's /consul/config directory is mapped to the host's /mnt/edgex-consul-config directory.

2、edgex-core-consul's /consul/data directory is mapped to the host's /mnt/edgex-consul-data directory.

3、edgex-db's /data/db directory is mapped to the host's /mnt/edgex-db directory.

4、edgex-support-logging's /edgex/logs directory is mapped to the host's /mnt/edgex-support-logging directory.

- NodePort is enabled by default. According to default NodePort range(30000～32767), EdgeX NodePort mappings are as follows. 

| EdgeX Service Name          | ContainerPort | NodePort |
| :-------------------------- | ------------- | -------- |
| edgex-core-data             | 48080         | 30080    |
| edgex-core-metadata         | 48081         | 30081    |
| edgex-core-command          | 48082         | 30082    |
| edgex-core-consul           | 8500          | 30850    |
| edgex-support-rulesengine   | 48075         | 30075    |
| edgex-support-notifications | 48060         | 30060    |
| edgex-support-scheduler     | 48085         | 30085    |
| edgex-appservice-rules      | 48100         | 30100    |
| edgex-device-rest           | 49986         | 31986    |
| edgex-device-virtual        | 49990         | 31990    |
| edgex-ui                    | 4000          | 30400    |
| edgex-system                | 48090         | 30090    |
| edgex-redis                 | 6379          | 30079    |

## Some articles about deploying edgex to kubernetes

- VMware China R&D Center
https://mp.weixin.qq.com/s/ECdEkc9QdkVScn4Lvl_JJA

## Feedback

If you find a bug or want to request a new feature, please open a [GitHub Issue](https://github.com/DaveZLB/edgex-helm/issues)


