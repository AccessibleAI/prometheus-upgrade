#### **Delete old prometheus installation**
```
kubectl delete -f promethus_to_delete.yaml
kubectl -n cnvrg  get pvc | grep prometheus | awk '{print $1}' | xargs kubectl -n cnvrg delete pvc $1
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
#### **Install New prometheus installation Hostpath Directory Istio**
#### Change nodeaffinity in prometheus-prometheus.yaml filei 
#### Make sure the local path is correct 
#### Change hosts to correct domain_name in prometheus-vs.yaml file
```
rm manifests/prometheus-prometheus_cloud.yml
```
#### **Install New prometheus installation on Cloud instance Istio (using default storage class)**
#### Change hosts to correct domain_name in prometheus-vs.yaml file
```
rm manifests/prometheus-prometheus.yml
```
```
kubectl apply -f manifests/setup
kubectl apply -f manifests/
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
```


#### clean resources
```
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
