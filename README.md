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
rm manifests/prometheus-prometheus_cloud.yaml
```
#### **For installation on cloud - Installed with Istio**
- Change hosts to correct domain_name in prometheus-vs.yaml file
```
rm manifests/prometheus-prometheus.yaml
```

#### **Install Prometheus**
```
kubectl apply -f manifests/setup
kubectl apply -f manifests/
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
```
#### **Verify Installation completed successfully**
Run the following, until it finishes:
```
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
```
Go to the grafana.<your domain> and check on the info page (on the buttom of the left pane) version is Grafana v6.6.0 (5c11bbdfb4)

#### **In some clusters there might be a bug based on the provider - to fix the bug run command below**
Fix the url so that if fits your domain with the correct http/https header:
```
url=[http/https]://prometheus.[domain-name].cnvrg.io; if (( $(curl -s  $url/targets | grep -i 'server returned HTTP status 401 Unauthorized' | wc -l) > 0 )); then echo 'applying fix' ; kubectl -n cnvrg get servicemonitor kubelet -o yaml  | grep -v '{"apiVersion":"monitoring.coreos.com/v1"'  | sed 's/https/http/g' | kubectl -n cnvrg apply -f -; fi
```

#### clean resources
```
kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup
```
