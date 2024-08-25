### Killer test attempt one


#### Get list of all namespaces

kubectl get ns  -A > namespaces


#### Create a single pod of image htto:2.4.41-alpine namespace default , the pod should be named pod1 and the container should be named pod1-container

kubectl run pod1 --image httpd:2.4.41-alpine --dry-run=client -o yaml >  pod1-declarative.yaml

kubectl get pod pod1


### Team Neptune needs a Job template located at /opt/course/3/job.yaml. This Job should run image busybox:1.31.0 and execute sleep 2 && echo done. It should be in namespace neptune, run a total of 3 times and should execute 2 runs in parallel.

Start the Job and check its history. Each pod created by the Job should have the label id: awesome-job. The job should be named neb-new-job and the container neb-new-job-container.

kubectl create job neb-new-job -n neptune --image busybox:1.31.0 --dry-run=client -o yaml > job.yaml


### Team Mercury asked you to perform some operations using Helm, all in Namespace mercury:

Delete release internal-issue-report-apiv1
Upgrade release internal-issue-report-apiv2 to any newer version of chart bitnami/nginx available
Install a new release internal-issue-report-apache of chart bitnami/apache. The Deployment should have two replicas, set these via Helm-values during install
There seems to be a broken release, stuck in pending-install state. Find it and delete it


helm list -n mercury

helm search repo bitnami/ng

helm upgrade <release> bitnami/nginx --version 18.1.11

helm install <release> bitnami/apache --set repliceCount=2 -n mercury

### Team Neptune has its own ServiceAccount named neptune-sa-v2 in Namespace neptune. A coworker needs the token from the Secret that belongs to that ServiceAccount. Write the base64 decoded token to file /opt/course/5/token on ckad7326.


Team Neptune has its own ServiceAccount named neptune-sa-v2 in Namespace neptune. A coworker needs the token from the Secret that belongs to that ServiceAccount. Write the base64 decoded token to file /opt/course/5/token on ckad7326.



### Create a single Pod named pod6 in Namespace default of image busybox:1.31.0. The Pod should have a readiness-probe executing cat /tmp/ready. It should initially wait 5 and periodically wait 10 seconds. This will set the container ready only if the file /tmp/ready exists.

The Pod should run the command touch /tmp/ready && sleep 1d, which will create the necessary file to be ready and then idles. Create the Pod and confirm it starts.

kubectl run pod6 --image busybox:1.31.0 --dry-run=client -o yaml -- /bin/sh -c "touch /tmp/ready && sleep 1d" > podq6.yaml


```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: pod6
  name: pod6
spec:
  containers:
  - args:
    - /bin/sh
    - -c 
    - touch /tmp/ready && sleep 1d
    image: busybox:1.31.0
    name: pod6
    readinessProbe:
      exec: 
        command: 
        - /bin/sh
        - -c
        - cat /tmp/ready
      initialDelaySeconds: 5
      periodSeconds: 10
  restartPolicy: Never

```


### Team Pluto needs a new cluster internal Service. Create a ClusterIP Service named project-plt-6cc-svc in Namespace pluto. This Service should expose a single Pod named project-plt-6cc-api of image nginx:1.17.3-alpine, create that Pod as well. The Pod should be identified by label project: plt-6cc-api. The Service should use tcp port redirection of 3333:80.
Finally use for example curl from a temporary nginx:alpine Pod to get the response from the Service. Write the response into /opt/course/10/service_test.html on ckad9043. Also check if the logs of Pod project-plt-6cc-api show the request and write those into /opt/course/10/service_test.log on ckad9043.


kubectl expose pod project- plt-6cc-api  --name project-plt-6cc-svc -n pluto --port 3333 --target-port 80
