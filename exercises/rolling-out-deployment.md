### Rolling out a new reivsion for a deployment

kubectl create deployment server-deployment --replicas 2 --image grand-server:1.4.6 --dry-run=client -o yaml > server-deployment.yaml

k rollout history deployment server-deployment 


k set image deployment server-deployment image=nginx


### Create autoscaler

k autoscale deploymnet server-deployment --cpu-percent 54 --min 2 --max 20

k path hpa server-deployment -p '{"spec":{"minReplicas":4}}'
