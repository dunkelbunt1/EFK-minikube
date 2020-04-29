# EFK-minikube
Non production setup of the EFK stack on minikube

1. **Create the namespace** 
```
kubectl create -f kube-logging.yaml
```
2. **Create the elastic search service** 
```
kubectl create -f elasticsearch_svc.yaml
```
3. **Create elastic search as a Stateful Set** 
```
kubectl create -f elasticsearch_statefulset.yaml
```
4. **Creating the Kibana Deployment and Service** 
```
kubectl create -f kibana.yaml
```
5. **Creating the Fluentd DaemonSet** 
```
kubectl create -f fuentd.yaml
```
6. **Accessing the UI** 

Oberserve the name of your Kibana pod:

```
kubectl get pods --namespace=kube-logging
NAME                      READY   STATUS    RESTARTS   AGE
es-cluster-0              1/1     Running   0          63m
es-cluster-1              1/1     Running   0          62m
es-cluster-2              1/1     Running   0          62m
fluentd-v6jgn             1/1     Running   0          23m
kibana-5749b5778b-vwn47   1/1     Running   0          51m
```
and configure port forwarding.
```
kubectl port-forward kibana-5749b5778b-vwn47  5601:5601 --namespace=kube-logging
```
visit the following web URL:
```
http://localhost:5601
```

7. **Testing the logging** 

```
kubectl create -f counter.yaml
```




**Version:** 

kubectl version: 1.18.x, minikube version: v1.9.x
