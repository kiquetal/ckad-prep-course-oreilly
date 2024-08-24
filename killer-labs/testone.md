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
