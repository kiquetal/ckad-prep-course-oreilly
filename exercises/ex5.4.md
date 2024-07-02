### Exercise

1 - Create namespace ckad-prep
2 - In the namespace ckad-prep create a new Pod named mypod with the image nginx:2.3.5. Expose the port 80
3 - Identify the issue with creating the container. Write down the root cause of issue in a file named pod-error.txt
4 - Change the image of the Pod nginx:1.15.12
5 - List the pod and ensure that the container is running.
6 - Log into the container and run the ls command. Write down the output. Log out the container.
7 - Retrieve the IP address of the Pod mypod
8 - Run a temporary Pod in the namesapce ckad-prerp using th eimage busybox. shell into it and run a wget command
agains the nginx Pod using port 80
9 - Render the logs of Pod mypod
10 - Delete the Pod and the namespace 
