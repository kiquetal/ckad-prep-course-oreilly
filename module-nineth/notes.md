#### Labels vs Annotations

- A maxinum number of 63

- Key-value pairs


- Annotations can modify the behaviour on runtime.


kubectl get pods -l tier=frontend, env=dev --show-labels


- Labels are an important, cross-cutting concept in kubernetes. A label is a key-value pair assigned to an object.

- Some primitives like the Deployment, Service and Network Policy use label selection heavily

- Use annotations to provide human-readable metadata to objects. Annotations cannot be used for querying objects


