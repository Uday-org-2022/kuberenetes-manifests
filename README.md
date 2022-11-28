# kuberenetes-manifests
# kubectl create ns prod
# kubectl config set-context --current --namespace=prod
# kubectl get pods -n prod

# DASHBOARD

mkdir $HOME/certs

cd certs/

openssl genrsa -out dashboard.key 2048
openssl rsa -in dashboard.key -out dashboard.key
openssl req -sha256 -new -key dashboard.key -out dashboard.csr
openssl x509 -req -sha256 -days 365 -in dashboard.csr -signkey dashboard.key -out dashboard.crt

kubectl create ns kubernetes-dashboard
kubectl -n kubernetes-dashboard create secret generic kubernetes-dashboard-certs --from-file=$HOME/certs

# https://github.com/kubernetes/dashboard
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

kubectl edit svc kubernetes-dashboard -n kubernetes-dashboard

https://15.207.108.57:32305/

apiVersion: v1
kind: ServiceAccount
metadata:
   name: k8s-admin
   namespace: kubernetes-dashboard
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: k8s-admin
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: k8s-admin
    namespace: kubernetes-dashboard
    
 kubectl -n kubernetes-dashboard create token k8s-admin

    

