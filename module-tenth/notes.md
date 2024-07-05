#### Module tenth

Deployment: contols predefined number of POds with the same configuration, so-called replicas

The number of replicas can be scaled up or down to fulfill load requirements

Updates to the replica configuration 


##### Types of autoscales

- Horizontal Pod Autoscaler: Scale the number of pod based on CPU and memory threshold


- Vertical Pod Autoscaler"base on historic metrics. Supported by a cloud provider as an add-on or needs to be installed manually:


- Both autoscalers use the metrics server.(Every pode should also set resource requests and limits)

