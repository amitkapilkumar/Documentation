==== NAB DEV0 =======================================
az login --tenant 07854bea-1ad0-4a14-b1e5-c5da8ff45eb7
az account set --subscription nab-dev0
az aks get-credentials -n nab-dev0-aks -g nab-dev0-aks-rg --overwrite
kubectl get po -n nab-dev0 | Select-String -Pattern 'account' -CaseSensitive 

kubectl describe pod integration-fed-service-864689f7f4-j9jgx -n nab-dev0 // get pods / containers details


== for tyl-dev0-aks
az account set --subscription "tyl-dev0"; az aks get-credentials -n tyl-dev0-aks -g tyl-dev0-aks-rg --overwrite
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
az aks browse --resource-group tyl-dev0-aks-rg --name tyl-dev0-aks

kubectl port-forward -n tyl-dev0  integration-maintenance-mock-service-69b96654d9-k9rtn 8080:8443

az login

kubectl -n tyl-dev0 get pods | Select-String -Pattern 'integration-merchant-data' -CaseSensitive // search fo pattern
kubectl get pod -n tyl-dev0 'integration-cufs-service-7cc9d5c9f9-nrt8k' -o=jsonpath='{.spec.containers[].image}' // check for deployed version //  

kubectl logs portal-account-api-6998bd8fdf-gxp5m -n tyl-dev0 // to view logs
kubectl scale --replicas=0 deployment tool-kafkatestconsumer-service -n tyl-uat0 // scale down pod

TYL-UAT
az login
az account set --subscription "tyl-uat";  az aks get-credentials -n tyl-uat0-aks -g tyl-uat0-aks-rg --overwrite
az account set --subscription "tyl-dev0"; az aks get-credentials -n tyl-dev0-aks -g tyl-dev0-aks-rg --overwrite
az account set --subscription "tyl-test0"; az aks get-credentials -n tyl-test0-aks -g tyl-test0-aks-rg --overwrite


az account set --subscription "nab-perf0"; az aks get-credentials -n nab-perf0-aks -g nab-perf0-aks-rg --overwrite

== for pol-test0
az login
az account set --subscription "pollinate-test"; az aks get-credentials -n pol-test0-aks -g pol-test0-aks-rg --overwrite
kubectl -n pol-test0 get pods

kubectl get pod -n pol-test0 'portal-announcement-api-66b957745d-lkmgm' -o=jsonpath='{.spec.containers[].image}' 

kubectl logs integration-reference-data-service-56dd5f8dbc-2h6r7 -n pol-test0

== for cweld01
az login
az aks get-credentials -g tylrootaksrg0 -n pilsharedakslower --subscription “6f4fa17a-25cd-4ce1-bbef-acf14a30c9ad”
--set context
kubectl config use-context pilsharedakslower
--show pod status
kubectl get po -n cweld01
-- conneting to bash terminal in service pod 
kubectl -ncweld01 exec -it integration-fed-service-5b4bfdb8d9-m89jk  -- bash
curl http://localhost:8081/actuator/health

kubectl -npol-dev0 exec -it integration-fed-service-d48fd5949-jvb6h  -- bash
kubectl port-forward portal-transaction-api-66b684989-6t5r7 8080:8081 -n pol-dev0
