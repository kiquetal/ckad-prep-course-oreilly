### Assigning label to a pod imperatevily


kubectl run pod-1 --name=nginx 

kubectl label pod pod-1 frontend=label

kubectl label pods pod-1 pod-2 pod-3 team=artemidis
