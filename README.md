#### **Delete old prometheus installation**
```
kubectl delete -f promethus_to_delete.yaml
```
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
kubectl -n cnvrg delete pvc storage-prometheus-cnvrg-prometheus-operator-prometheus-0
```
#kubectl -n cnvrg  delete  pvc prometheus-cnvrg-prometheus-operator-prometheus-db-prometheus-cnvrg-prometheus-operator-prometheus-0
```
#### **Install New prometheus installation**
#### Change nodeaffinity in prometheus-prometheus.yaml file
#### Change hosts to correct domain_name in prometheus-vs.yaml file
```
kubectl apply -f manifests/setup
```
kubectl apply -f manifests/
```
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
```


#### clean resources
```
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
