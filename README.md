#### **Delete old prometheus installation**
```
kubectl delete -f promethus_to_delete.yaml
kubectl -n cnvrg  get pvc | grep prometheus | awk '{print $1}' | xargs kubectl -n cnvrg delete pvc $1
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
#### **For installation on On premise without NFS support with Istio**
- Change nodeaffinity in prometheus-prometheus.yaml file
- Make sure the local path is correct 
- Change hosts to correct domain_name in prometheus-vs.yaml file
```
rm manifests/prometheus-prometheus_cloud.yml
```
#### **For installation on cloud - Installed with Istio**
- Change hosts to correct domain_name in prometheus-vs.yaml file
```
rm manifests/prometheus-prometheus.yml
```

#### **Install Prometheus**
```
kubectl apply -f manifests/setup
kubectl apply -f manifests/
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
```


#### clean resources
```
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
