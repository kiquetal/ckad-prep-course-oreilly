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
    spec:
      volumes:
      - name: web-content
        emptyDir: {}
      initContainers:
      - name: init-cron
        image: busybox:1.31.0
        command: ['/bin/sh','-c','echo "check this out!" > /tmp/web-content/index.html"]
        volumeMounts:
        - name: web-content
          mountPath: "/tmp/web/content"
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - name: web-content
          mountPath: "/usr/share/nginx/html"
        ports:
        - containerPort: 80 


````

### Question 16

The Tech Lead of Mercury2D decided it's time for more logging, to finally fight all these missing data incidents.
 There is an existing container named cleaner-con in Deployment cleaner in Namespace mercury. 
This container mounts a volume and writes logs into a file called cleaner.log.

The yaml for the existing Deployment is available at /opt/course/16/cleaner.yaml. 
Persist your changes at /opt/course/16/cleaner-new.yaml on ckad7326 but also make sure the Deployment is running.

Create a sidecar container named logger-con, image busybox:1.31.0 , 
which mounts the same volume and writes the content of cleaner.log to stdout, you can use the tail -f command for this. 
This way it can be picked up by kubectl logs.

Check if the logs of the new container reveal something about the missing data incidents.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cleaner
  namespace: mercury
spec:
  replicas: 2
  selector:
    matchLabels:
      id: cleaner
  template:
    metadata:
      labels:
        id: cleaner
    spec:
      volumes: 
      - name: logs
        emptyDir: {}
      initContainers:
      - name: init
 	image: bash:5.0.11
        command: ['bash','-c','echo init > /var/log/cleaner/cleaner.log']
	volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      - name: logger-con
        image: busybox:1.31.0
        restartPolicy: Always
        command:['sh','-c',"tail -f /var/log/cleaner/cleaner.log"]
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
      containers:
      - name: cleaner-con
        image: bash:5.0.11
        command: ['bash','-c','while true; do echo `date`: "remove random file " >> /var/log/cleaner/cleaner.log; sleep 1; done']
        volumeMounts:
        - name: logs
          mountPath: /var/log/cleaner
```

### Question 15
Team Moonpie has a nginx server Deployment called web-moon in Namespace moon. 
Someone started configuring it but it was never completed. 
To complete please create a ConfigMap called configmap-web-moon-html containing the content of file /opt/course/15/web-moon.html under the data key-name index.html.

The Deployment web-moon is already configured to work with this ConfigMap and serve its content. 
Test the nginx configuration for example using curl from a temporary nginx:alpine Pod.

kubectl create configmap configmap-web-moon-html --from-file=index.html=/opt/course/15/web-moon.html 

kubectl run temp --image=nginx:alpine --rm -- wget -O- deploy.ment


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-moon
  namespace: moon
  labels:
    id: deployment
````

### Question 14


You need to make changes on an existing Pod in Namespace moon called secret-handler. Create a new Secret secret1 which contains user=test and pass=pwd. The Secret's content should be available in Pod secret-handler as environment variables SECRET1_USER and SECRET1_PASS. The yaml for Pod secret-handler is available at /opt/course/14/secret-handler.yaml.

There is existing yaml for another Secret at /opt/course/14/secret2.yaml, create this Secret and mount it inside the same Pod at /tmp/secret2. Your changes should be saved under /opt/course/14/secret-handler-new.yaml on ckad9043. Both Secrets should only be available in Namespace moon.


### Question 13


Team Moonpie, which has the Namespace moon, needs more storage. Create a new PersistentVolumeClaim named moon-pvc-126 in that namespace. This claim should use a new StorageClass moon-retain with the provisioner set to moon-retainer and the reclaimPolicy set to Retain. The claim should request storage of 3Gi, an accessMode of ReadWriteOnce and should use the new StorageClass.

The provisioner moon-retainer will be created by another team, so it's expected that the PVC will not boot yet. Confirm this by writing the event message from the PVC into file /opt/course/13/pvc-126-reason on ckad9043.


### Question 12




### Question 11



### Question 10

