# EdgeX Foundry on Kubernetes

A Helm chart to easily deploy the EdgeX IoT project on Kubernetes.
Based on EdgeX [Geneva](https://github.com/edgexfoundry/developer-scripts/tree/master/releases/geneva/compose-files) version.



## Get Start

- Install [Helm](https://v2.helm.sh/docs/)

- **Deploy EdgeX**
```$xslt
$ cd edgex-kubernetes-support
$ helm install --name geneva .
```
- **Undeploy EdgeX**
```$xslt
$ cd edgex-kubernetes-support
$ helm delete geneva --purge
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

- Helm version 2 and version 3 are different. Only version 2 is tested here
- This project is based on [docker-compose-geneva-redis-no-secty.yml](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/geneva/compose-files/docker-compose-geneva-redis-no-secty.yml),
you can implement your customized version based on this.
- Since other edgex services need to rely on consul to obtain configuration or register themselves to consul, other services cannot run normally until consul starts successfully.
- About EdgeX Volume

Unlike the docker-compose files for this release (which use a separate Docker volume container), the manifest files mount host based volumes as follows:

1、edgex-core-consul's /consul/config directory is mapped to the host's /mnt/edgex-consul-config directory.

2、edgex-core-consul's /consul/data directory is mapped to the host's /mnt/edgex-consul-data directory.

3、edgex-mongo's /data/db directory is mapped to the host's /mnt/edgex-mongo directory.

4、edgex-support-logging's /edgex/logs directory is mapped to the host's /mnt/edgex-support-logging directory.

## Some articles about deploying edgex to kubernetes

- VMware China R&D Center
https://mp.weixin.qq.com/s/ECdEkc9QdkVScn4Lvl_JJA

## Feedback

If you find a bug or want to request a new feature, please open a [GitHub Issue](https://github.com/DaveZLB/edgex-kubernetes-support/issues)


