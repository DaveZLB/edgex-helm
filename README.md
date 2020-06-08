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
## Tips

- Helm version 2 and version 3 are different. Only version 2 is tested here
- This project is based on [EdgeX fuji non-secure version](https://github.com/edgexfoundry/developer-scripts/blob/master/releases/fuji/compose-files/docker-compose-fuji-no-secty.yml),
you can implement a secure version based on this.

## Feedback

If you find a bug or want to request a new feature, please open a GitHub Issue


