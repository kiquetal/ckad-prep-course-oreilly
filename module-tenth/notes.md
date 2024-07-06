#### Module tenth

Deployment: contols predefined number of POds with the same configuration, so-called replicas

The number of replicas can be scaled up or down to fulfill load requirements

Updates to the replica configuration 


##### Types of autoscales

- Horizontal Pod Autoscaler: Scale the number of pod based on CPU and memory threshold


- Vertical Pod Autoscaler"base on historic metrics. Supported by a cloud provider as an add-on or needs to be installed manually:


- Both autoscalers use the metrics server.(Every pode should also set resource requests and limits)


#### 

kubectl rollout undo --to-revision=1 deployemnt nginx

kubectl rollout history --to-revision=2 deployments nginx


#### Common deployments strategies

- Ramped: Release a new version on a rolloing update fashion,one after the other.


- Recreate: Terminate the old version and release the new one


- Blue/green: Release a new version alongside the old version then switch traffic


- Canary: Release a new version to a subset of users

spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 0
(SECONDARY replicaset is created with a new version of application(


spec:
  replicas: 3
  strategy:
    type: Recreate

terminate all the running instances


blue/greend canary need 2 deployments


