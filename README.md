kubectl delete -f promethus_to_delete.yaml
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
kubectl -n cnvrg delete pvc storage-prometheus-cnvrg-prometheus-operator-prometheus-0
#kubectl -n cnvrg  delete  pvc prometheus-cnvrg-prometheus-operator-prometheus-db-prometheus-cnvrg-prometheus-operator-prometheus-0
kubectl apply -f manifests/setup
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
kubectl apply -f manifests/




#clean resources
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
