#### Create a deployment with kubectl

k create deployment http-deployment --image nginx --replicas 1 -n workspace

k scale deployment http-deployment --replicas 5 -n workspace
