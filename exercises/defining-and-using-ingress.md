#### Defining and using an ingress

Creating a Service
Expose a Service named web of type ClusterIP for the Deployment named web in the default namespace. The Service should route network traffic to the Pods controlled by the Deployment.

The Service should define the incoming port 80 and the outgoing port 3000. Explictly assign the IP address of the control plane node to the Service attribute spec.externalIPs.

kubectl expose deploy web --port=80 --target-port=3000 -o yaml --dry-run=client  > service.yaml



Create an Ingress named hello-world-ingress in the namespace default. Define the path type Prefix to the path / from the host hello-world.exposed to the Service from the previous step.

Assign the annotation kubernetes.io/ingress.class: "nginx" to ensure that the Ingress controller picks up on the changes of the Ingress object.
