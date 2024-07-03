### Module 7: Volumes

- Each container managed files in a temporay file system. Data written to the file system is lost when the container is restarted

- Ephemeral Volumes exist for the lifespan of a Pod. They are usefuul if you want to share data between multiple containers running in the Pod.

- Persistent Volumes preserve data beyond the lifespan of a Pod. They are a good option for applications that require data to exist longer

- Define the Volume type with spec.volumes[] and the reference it in a container with spec.containers[].volume.volumeMounts


### Volume Types

- emptyDir 

- hostPath

- configMap,secret

- nfs

- persistentVolumeClaim
