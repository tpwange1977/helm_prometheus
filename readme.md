

Install helm:
choco install kubernetes-helm

Helm add repo:
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

Helm install prometheus:
helm install prometheus-community/prometheus --generate-name --set server.terminationGracePeriodSeconds=360


Helm: other command
helm uninstall mysql-1641612801
helm list
helm search repo
