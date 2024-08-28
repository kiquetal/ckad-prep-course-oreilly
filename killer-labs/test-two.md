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


### Question 19


In Namespace jupiter you'll find an apache Deployment (with one replica) named jupiter-crew-deploy and a ClusterIP Service called jupiter-crew-svc which exposes it. Change this service to a NodePort one to make it available on all nodes on port 30100.

Test the NodePort Service using the internal IP of all available nodes and the port 30100 using curl, 
you can reach the internal node IPs directly from your main terminal. 
On which nodes is the Service reachable? On which node is the Pod running?





### Question 18 

There seems to be an issue in Namespace mars where the ClusterIP service manager-api-svc should make the Pods of Deployment manager-api-deployment available inside the cluster.
You can test this with curl manager-api-svc.mars:4444 from a temporary nginx:alpine Pod. Check for the misconfiguration and apply a fix.

kubectl run temp --restart=Never --image nginx:alpine 


kubectl run tmp --rm -i -restart=Never --image=nginx:alpine -- wget service-srv.mars:4444


### Question 17

Last lunch you told your coworker from department Mars Inc how amazing InitContainers are. Now he would like to see one in action. There is a Deployment yaml at /opt/course/17/test-init-container.yaml. This Deployment spins up a single Pod of image nginx:1.17.3-alpine and serves files from a mounted volume, which is empty right now.

Create an InitContainer named init-con which also mounts that volume and creates a file index.html with content check this out! in the root of the mounted volume. For this test we ignore that it doesn't contain valid html.

The InitContainer should be using image busybox:1.31.0. Test your implementation for example using curl from a temporary nginx:alpine Pod.


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: test-init-container
  namespace: mars
spec:
  replica: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels: 
        id: nginx
      


````
