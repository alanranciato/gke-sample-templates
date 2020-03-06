Basic examples of K8 manifests for GKE.

Setup


Create Cluster:
gcloud container clusters create my-demo-cluster --num-nodes=3 --zone=us-central1-a --enable-ip-alias


If using istio, enable istio on the cluster:

gcloud beta container clusters update my-demo-cluster --project [my-project] --zone us-central1-a\
    --update-addons=Istio=ENABLED --istio-config=auth=MTLS_PERMISSIVE


If using nginx, install helm and then install nginx :

Install helm:
curl -o get_helm.sh https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get
chmod +x get_helm.sh
./get_helm.sh

Install helm:
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller

Install nginx controller:
helm install --name nginx-ingress stable/nginx-ingress --set rbac.create=true --set controller.publishService.enabled=true



