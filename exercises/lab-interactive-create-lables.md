#### Assing Label to Pod imperatively

Create three Pods that use the image nginx:1.25.3-alpine in the namespace queryable.

The names of the Pods should be pod-1, pod-2, and pod-3.

Do not assign any labels to the Pods.


kubectl run pod-1 --image=nginx:1.25.3-alpine -n queryable

kubectl label pod pod-1 tier=frontend -n queryable

kubectl label pod pod-2 tier=backend -n queryable

kubectl label pod pod-3 tier=db -n queryable 

kubectl label pod pod-1 team=artemidis -n queryable
kubectl label pod pod-2 team=artemidis -n queryable
kubectl label pod pod-3 team=artemidis -n queryable


