# EdgeX Foundry on Kubernetes

A Helm chart to easily deploy the EdgeX IoT project on Kubernetes.
Based on EdgeX [fuji](https://github.com/edgexfoundry/developer-scripts/tree/master/releases/fuji/compose-files) version.



## Get Start

- Install [Helm](https://v2.helm.sh/docs/)

- **Deploy EdgeX**
```$xslt
$ cd edgex-kubernetes-support
$ helm install --name fuji .
```
- **Undeploy EdgeX**
```$xslt
$ cd edgex-kubernetes-support
$ helm delete fuji --purge
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
- This project is based on [EdgeX fuji non-secure version](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/fuji/compose-files/docker-compose-fuji-no-secty.yml),
you can implement a secure version based on this.
- Since other edgex services need to rely on consul to obtain configuration or register themselves to consul, other services cannot run normally until consul starts successfully.
- The role of config seed pod is to push the configurations of all services to consul.

## Feedback

If you find a bug or want to request a new feature, please open a [GitHub Issue](https://github.com/DaveZLB/edgex-kubernetes-support/issues)


