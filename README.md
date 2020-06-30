# EdgeX Foundry on Kubernetes

A Helm chart to easily deploy the EdgeX IoT project on Kubernetes.
Based on EdgeX [fuji](https://github.com/edgexfoundry/developer-scripts/tree/master/releases/fuji/compose-files) version.



## Get Start

- Install [Helm](https://v2.helm.sh/docs/)

- **Deploy EdgeX**

helm2
```bash
$ cd edgex-helm
$ helm install --name fuji .
```
helm3
```bash
cd edgex-helm
helm install fuji .
```

- **Undeploy EdgeX**

helm2
```bash
$ helm delete fuji --purge
```
helm3
```bash
helm uninstall fuji
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

- This project is based on [EdgeX fuji non-secure version](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/fuji/compose-files/docker-compose-fuji-no-secty.yml),
you can implement a secure version based on this.
- Since other edgex services need to rely on consul to obtain configuration or register themselves to consul, other services cannot run normally until consul starts successfully.
- The role of config seed pod is to push the configurations of all services to consul.
- About EdgeX Volume

Unlike the docker-compose files for this release (which use a separate Docker volume container), the manifest files mount host based volumes as follows:

1、edgex-core-consul's /consul/config directory is mapped to the host's /mnt/edgex-consul-config directory.

2、edgex-core-consul's /consul/data directory is mapped to the host's /mnt/edgex-consul-data directory.

3、edgex-mongo's /data/db directory is mapped to the host's /mnt/edgex-mongo directory.

4、edgex-support-logging's /edgex/logs directory is mapped to the host's /mnt/edgex-support-logging directory.

## Feedback

If you find a bug or want to request a new feature, please open a [GitHub Issue](https://github.com/DaveZLB/edgex-helm/issues)


