### Rolling out a new reivsion for a deployment

kubectl create deployment server-deployment --replicas 2 --image grand-server:1.4.6 --dry-run=client -o yaml > server-deployment.yaml
