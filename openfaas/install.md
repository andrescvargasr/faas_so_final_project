#### Step 1: building the docker images

Before deploying any of the components we will be building the docker images needed to deploy jupyter or any of the notebook function containers. To build the images, some basic utility scripts are provided

``` shell
## Build to minikube registry
eval $(minikube docker-env)

## Build base and dev images
./bin/build_serverless_datascience_base.sh
./bin/build_serverless_datascience_dev.sh
```

This step takes a while...

#### Step 2: Deploy cluster components

To run the notebooks and setup the cluster there are a few steps

Setup helm within your cluster

``` shell
echo "Setting up and init ..."
kubectl create serviceaccount -n kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account=tiller --tiller-namespace=kube-system --wait

echo "Securing helm..."
sleep 5 #wait for tiller to deploy
kubectl patch deployment tiller-deploy \
	    --namespace=kube-system \
		--type=json \
		--patch='[{"op": "add", "path": "/spec/template/spec/containers/0/command", "value": ["/tiller", "--listen=localhost:44134"]}]'
```

Then deploy `./yml/jupyter.yml` for our jupyter based interactive development environment from within the cluster

``` shell
echo "Deploying single user notebook server ..."
kubectl apply -f yml/jupyter.yml
```

Now deploy OpenFaas using `helm`

``` shell
echo "Adding openfaas to helm repos ..."
helm repo add openfaas https://openfaas.github.io/faas-netes/

echo "Adding openfaas secret ..."
PASSWORD=$(head -c 12 /dev/urandom | shasum| cut -d' ' -f1)
```

Create openfaas NAMESPACES:

```
kubectl apply -f https://raw.githubusercontent.com/openfaas/faas-netes/master/namespaces.yml
```

```
kubectl -n openfaas create secret generic basic-auth \
	--from-literal=basic-auth-user=admin \
	--from-literal=basic-auth-password=\"$PASSWORD\"

echo "Deploying openfaas ..."
helm repo update && \
helm upgrade openfaas \
	 --install openfaas/openfaas \
	 --namespace openfaas  \
	 --set basic_auth=false \
	 --set functionNamespace=openfaas

echo "Upgrading openfaas image pull policy ..."
helm upgrade openfaas openfaas/openfaas --install --set "faasnetesd.imagePullPolicy=IfNotPresent"
```

You can also deploy all these components using the shell script `./bin/deploy_cluster_components.sh`

#### Step 3: forward ports from jupyter and openfaas

``` shell
sh -c '(kubectl port-forward -n default svc/jupyter 9999:8888 &\
        kubectl port-forward -n openfaas svc/gateway-external 8080:8080)'
```

You can now go to `localhost:9999/lab` in your browser and you should see several language kernels at your disposal.

![Languages in Jupyter](images/language_lab.png)

Now navigate to `mnt/notebooks/deploy_notebook_function.ipynb` for further instructions. 

**Next ->** Go to fisrt [README.md](../README.md)