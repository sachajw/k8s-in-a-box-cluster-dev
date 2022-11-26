### Ingredients
- Docker
- Kind
- Helm
- Cluster.Dev
- Backstage

### [VSCode](https://code.visualstudio.com/) IDE
- Download `VSCode IDE` [here](https://code.visualstudio.com/download)
- Security starts in the IDE
- [Terms & Conditions](https://code.visualstudio.com/License/)

#### Helpful Extensions
- Install `Snyk Security | Code & Open Source Dependencies` scanner [here](https://marketplace.visualstudio.com/items?itemName=snyk-security.snyk-vulnerability-scanner)
- Install `Language Support for Java by Red Hat` [here](https://marketplace.visualstudio.com/items?itemName=redhat.java)
- Install `Yaml` support [here](https://marketplace.visualstudio.com/items?itemName=redhat.java)
- Install `Indent Rainbow` [here](https://marketplace.visualstudio.com/items?itemName=redhat.java)
- Install `Change All End of Line Sequence` [here](https://marketplace.visualstudio.com/items?itemName=vs-publisher-1448185.keyoti-changeallendoflinesequence)
- Install `ToDo Tree` [here](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)

### [Docker.com](https://www.docker.com/)
- [Account setup](https://hub.docker.com/signup)
- [Install](https://docs.docker.com/get-docker/)
- Get familiar with the basic commands
- Use [Devdocs](https://devdocs.io/) and the Docker documentation [here](https://docs.docker.com/)
- [Terms & Conditions](https://www.docker.com/legal/docker-terms-service/)

**Docker Security**
- Bake security right in from the word go
- We are going to use Snyk to scan our containers
- Snyk is free and you can set yourself up [here](https://snyk.io/)
- [Terms & Conditions for Snyk](https://snyk.io/policies/terms-of-service/)
- In `Docker Desktop` go to the ` Extensions Marketplace` and install the `Snyk Container Extension`
- On your command line you can now scan your Docker images with `docker scan your-docker-image`
- Disclaimer: Please follow any prompts `Snyk` requires you to fulfill to get up and running

#### .docker/config.json
```
{
	"auths": {
		"<account number>.dkr.ecr.eu-central-1.amazonaws.com": {},
		"https://index.docker.io/v1/": {}
	},
	"credsStore": "desktop",
	"currentContext": "desktop-linux"
}
```

#### List images
```
docker image list
```
#### Pull images to local
```
docker pull quay.io/ortelius/ortelius:latest
```
#### Copy
```
docker cp ~/.docker/config.json woolworths-control-plane:/var/lib/kubelet/config.json
```
#### Exec
```
docker exec -it woolworths-worker bash
```
#### Delete images
```
docker image rm quay.io/ortelius/ortelius
```
#### Octant the GUI perspective of K8s for developers
- Download [here](https://octant.dev/)

#### Kubeshark the API traffic viewer for K8s
- Download [here](https://github.com/kubeshark/kubeshark)

#### [Kind.sigs.k8s.io](https://kind.sigs.k8s.io/)
- Install [here](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)
- Kind node releases [here](https://github.com/kubernetes-sigs/kind/releases)
- Kind allows you to use Docker to run K8s nodes as containers
- Get familiar with the basic commands
- Checkout the Kind documentation [here](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Terms & Conditions](https://www.apache.org/licenses/LICENSE-2.0)

#### Why kind?
- kind supports multi-node (including HA) clusters
- kind supports building Kubernetes release builds from source
- support for make / bash or docker, in addition to pre-published builds
- kind supports Linux, macOS and Windows
- kind is a `CNCF certified conformant Kubernetes installer`

#### Get the list of nodes
```
kind get nodes -n woolworths
```
#### Cluster info
```
kubectl cluster-info --context woolworths
```
#### Logs
```
kind export logs -n woolworths
```
#### Load images onto the container nodes
```
kind load docker-image --name woolworths --nodes woolworths-control-plane,woolworths-worker quay.io/ortelius/ortelius
```

### Helm
- Install Helm [here](https://helm.sh/)
- Also known as the package manager for Kubernetes
#### Helm Dashboard
- GitHub page [here](https://github.com/komodorio/helm-dashboard)
- Binds to all IPs `0.0.0.0:8080`
#### Install
```
helm plugin install https://github.com/komodorio/helm-dashboard.git
```
#### Update
```
helm plugin update dashboard
```
#### Uninstall
```
helm plugin uninstall dashboard
```
#### Add a Helm package
```
helm repo add argo https://argoproj.github.io/argo-helm
```
#### List Helm repos
```
helm repo list
```
#### Update Helm repos
```
helm repo update
```
#### Lint
```
helm lint ./helm-appsofapps
```
#### Debug
```
helm template ./helm-appsofapps --debug
```
#### Dry-run
```
helm install argocd ./helm-appsofapps --dry-run
```
#### Dry-run with Debug
```
helm install argocd ./helm-appsofapps --dry-run --debug
```
