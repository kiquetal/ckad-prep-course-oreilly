### ConfigMaps and Secrets

kubectl get secret <name-of-secret> -o jsonpath="{.data.password}" | base64 -d


