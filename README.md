```bash
> kubectl create secret generic chartmuseum-secret --from-literal="basic-auth-user=curator" --from-literal="basic-auth-pass=mypassword"

> helm install kubeapps .
```
