```bash
> kubectl create namespace kubeapps
> kubectl config set-context --current --namespace=kubeapps

> kubectl create secret generic chartmuseum-secret --from-literal="basic-auth-user=curator" --from-literal="basic-auth-pass=mypassword"

> helm install kubeapps .

# wait a while

> kubectl port-forward svc/kubeapps 8080:80

# login with this token
> kubectl create serviceaccount kubeapps-operator
> kubectl create clusterrolebinding kubeapps-operator --clusterrole=cluster-admin --serviceaccount=kubeapps:kubeapps-operator
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: kubeapps-operator-token
  annotations:
    kubernetes.io/service-account.name: kubeapps-operator
type: kubernetes.io/service-account-token
EOF
> kubectl get secret kubeapps-operator-token -o go-template='{{.data.token | base64decode}}'
```
