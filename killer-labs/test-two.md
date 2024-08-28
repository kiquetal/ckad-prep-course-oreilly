### Question 25

Team Sunny needs to identify some of their Pods in namespace sun. 
They ask you to add a new label protected: true to all Pods with an existing label type: worker or type: runner.
 Also add an annotation protected: do not delete this pod to all Pods having the new label protected: true.

kubectl config set-context --current --namespace sun

kubectl get pods -l "protected=true" 


kubectl label pod -l type=runner protected=true
kubectl label pod -l type=woker protected=true

kubectl annotate pod -l protected=true protected="do no delete this pod"


### Question 21

Team Neptune needs 3 Pods of image httpd:2.4-alpine, 
create a Deployment named neptune-10ab for this. 
The containers should be named neptune-pod-10ab. 
Each container should have a memory request of 20Mi and a memory limit of 50Mi.

Team Neptune has it's own ServiceAccount neptune-sa-v2 
under which the Pods should run. 
The Deployment should be in Namespace neptune.


kubectl create deployment neptune-10ab --replicas 3 --image httpd:2.4.-alpine 


### Question 20

In Namespace venus you'll find two Deployments named api and frontend. 
Both Deployments are exposed inside the cluster using Services. 
Create a NetworkPolicy named np1 which restricts outgoing tcp connections from Deployment frontend and only allows those going to Deployment api. 
Make sure the NetworkPolicy still allows outgoing traffic 
on UDP/TCP ports 53 for DNS resolution.

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: multi-port-egress
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: frontend
  policyTypes:
    - Egress
  egress:
    - to:
        - podSelector:
            matchLabels:
		          app: api 
    - ports:
      - protocol: TCP
        port: 53
			- protocol: UDP
				port 53

```





