### Argo CD
#### Introduction
...


#### Deploy By Container
##### Run by Resource
```bash
# version
ARGO_CD_VERSION=v2.7.9
kubectl create namespace argocd
# non-ha install
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/${ARGO_CD_VERSION}/manifests/install.yaml
# ha install
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/${ARGO_CD_VERSION}/manifests/ha/install.yaml

```

##### Run in Kubernetes
```bash
# add and update repo
helm repo add argo https://argoproj.github.io/argo-helm
helm update

# get charts package
helm fetch argo/argo-cd --untar
cd argo-cd

# configure and run
vim values.yaml
...
helm -n cicd install argocd .
```


#### How To Use
##### postinstallation
```bash
# install argocd cli latest version
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
install -m 555 argocd-linux-amd64 /usr/local/bin/argocd && rm -f argocd-linux-amd64


# access argocd server
# development env
kubectl -n argocd port-forward svc/argocd-server --address=0.0.0.0 8080:443
# production env
kubectl -n argocd apply -f argocd-ingress.yaml


# argocd server infomation
ARGOCD_SERVER=argocd.example.com
ARGOCD_USERNAME=admin
ARGOCD_PASSWORD=`kubectl -n argocd get secrets argocd-initial-admin-secret -ojsonpath='{.data.password}' |base64 -d`


# argocd cli login
argocd login $ARGOCD_SERVER --username $ARGOCD_USERNAME --password $ARGOCD_PASSWORD
```

##### user management
```bash
# create user in configmaps
kubectl -n argocd patch configmaps argocd-cm --type='json' -p='[{"op": "add", "path": "/data", "value": {}},{"op": "add", "path": "/data/accounts.yakir", "value": "apiKey, login"}]'
# create password in secrets
argocd account update-password --account yakir


# delete user in configmaps
kubectl patch -n argocd cm argocd-cm --type='json' -p='[{"op": "remove", "path": "/data/accounts.yakir"}]'
# delete password in secrets
kubectl patch -n argocd secrets argocd-secret --type='json' -p='[{"op": "remove", "path": "/data/accounts.yakir.password"}]'


# get account infomation
argocd account list
argocd account get --account <username>


# generate token
argocd account generate-token --account <username>


# policy
kubectl -n argocd edit configmaps argocd-rbac-cm
...
data:
  policy.csv: |
    # p, account, applications, list, myproject/myapp, allow
    # p, proj:myproj, exec, create, */*, allow
	# p, role:myrole, exec, create, */*, allow
    p, yakir, *, *, *, allow
    
```

##### application
```bash
# create a directory app
argocd app create guestbook \
  --auto-prune
  --dest-name in-cluster \
  --dest-namespace default \
  --dest-server https://kubernetes.default.svc \
  --project default \
  --repo https://github.com/argoproj/argocd-example-apps.git \
  --path guestbook \
  --self-heal \
  --sync-policy automated
# create a helm app from a git repo
argocd app create helm-guestbook \
  --auto-prune
  --dest-name in-cluster \
  --dest-namespace default \
  --dest-server https://kubernetes.default.svc \
  --project default \
  --repo https://github.com/argoproj/argocd-example-apps.git \
  --path helm-guestbook \
  --self-heal \
  --sync-policy automated
# create a Helm app from a Helm repo
argocd app create nginx-ingress \
  --repo https://charts.helm.sh/stable \
  --helm-chart nginx-ingress \
  --revision 1.24.3 \
  --release-name nginx-ingress \
  --dest-namespace default \
  --dest-server https://kubernetes.default.svc


# query all application
argocd app list
#kubectl -n argocd get applications

# sync or deploy application
argocd app sync guestbook
argocd app get guestbook
```


### Argo Workflows
#### Introduction
...


#### Deploy By Container
##### Run by Resource
```bash
# version
ARGO_WORKFLOWS_VERSION=v3.4.9
# install
kubectl create namespace argo
kubectl apply -n argo -f https://github.com/argoproj/argo-workflows/releases/download/${ARGO_WORKFLOWS_VERSION}/install.yaml

# switch authentication mode to server
kubectl patch deployment \
  argo-server \
  --namespace argo \
  --type='json' \
  -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/args", "value": [
  "server",
  "--auth-mode=server"
]}]'
```


##### Run in Kubernetes
```bash
# add and update repo
helm repo add argo https://argoproj.github.io/argo-helm
helm update

# get charts package
helm fetch argo/argo-workflows --untar
cd argo-workflows

# configure and run
vim values.yaml
...
helm -n cicd install argo-workflows .

```

#### How To Use
##### postinstallation
```bash
# install  cli latest version
ARGO_WORKFLOWS_VERSION=v3.4.9
curl -sLO https://github.com/argoproj/argo-workflows/releases/download/${ARGO_WORKFLOWS_VERSION}/argo-linux-amd64.gz
gunzip argo-linux-amd64.gz 
install -m 755 argo-linux-amd64 /usr/local/bin/argo && rm -f argo-linux-amd64

# access argo-server 
kubectl -n argo port-forward deployment/argo-server --address=0.0.0.0  2746:2746
# kubectl -n argo apply -f argo-ingress.yaml

```

##### application
```bash
# example 
argo -n argo submit -w https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml
argo -n argo list
argo -n argo get @latest

# Steps | DAG | Artifacts etc..
```


> Reference:
> 1. [Official Website](https://argoproj.github.io/)
> 2. [Argo Workflows](https://argoproj.github.io/workflows/)
> 3. [Argo CD](https://github.com/argoproj/argo-cd/)
