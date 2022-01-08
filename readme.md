

Install helm:
choco install kubernetes-helm

Helm add repo:
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

Helm install prometheus:
helm install prometheus-community/prometheus --generate-name --set server.terminationGracePeriodSeconds=360



Result:
PS D:\minikube> kubectl get pods --selector='app=prometheus'
NAME                                                 READY   STATUS              RESTARTS   AGE
prometheus-1641614149-alertmanager-77bd96fb9-r744z   0/2     ContainerCreating   0          30s
prometheus-1641614149-node-exporter-2pnk2            1/1     Running             0          30s
prometheus-1641614149-pushgateway-5b7bf58994-6zf9f   0/1     ContainerCreating   0          30s
prometheus-1641614149-server-56bccffd9f-tvs28        0/2     ContainerCreating   0          30s
PS D:\minikube> kubectl get pods --selector='app=prometheus'
NAME                                                 READY   STATUS    RESTARTS   AGE
prometheus-1641614149-alertmanager-77bd96fb9-r744z   2/2     Running   0          159m
prometheus-1641614149-node-exporter-2pnk2            1/1     Running   0          159m
prometheus-1641614149-pushgateway-5b7bf58994-6zf9f   1/1     Running   0          159m
prometheus-1641614149-server-56bccffd9f-tvs28        2/2     Running   0          159m


Helm: other command
helm uninstall mysql-1641612801
helm list
helm search repo

kubectl: other command
1. kubectl create -f my-first-pod.yaml
2. kubectl describe pods my-pod
3. kubectl port-forward my-pod 8000:3000
4. kubectl expose pod my-pod --type=NodePort --name=my-pod-service
5. kubectl get services
NAME                                       TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-node                                 LoadBalancer   10.98.29.86      <pending>     8080:31566/TCP   17h
kubernetes                                 ClusterIP      10.96.0.1        <none>        443/TCP          17h
my-pod-service                             NodePort       10.105.97.25     <none>        3000:30290/TCP   27s
prometheus-1641614149-alertmanager         ClusterIP      10.96.71.89      <none>        80/TCP           3h33m
prometheus-1641614149-kube-state-metrics   ClusterIP      10.106.37.230    <none>        8080/TCP         3h33m
prometheus-1641614149-node-exporter        ClusterIP      None             <none>        9100/TCP         3h33m
prometheus-1641614149-pushgateway          ClusterIP      10.99.105.167    <none>        9091/TCP         3h33m
prometheus-1641614149-server               ClusterIP      10.107.254.155   <none>        80/TCP           3h33m

可以看到 my-pod-service 將 my-pod 的 port number 30003 與 minikube-vm 上的 port number 30290 做 mapping。接著可以使用 minukube service 的指令快速找到 my-pod-service 的 url
  
6.  minikube service my-pod-service --url

7. kubectl describe nodes minikub

