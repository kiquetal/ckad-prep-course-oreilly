
In this exercise, you will troubleshoot a misconfigured application stack.

The application stack consists of a web application implemented using Node.js and a MySQL database. The web application connects to the database upon requesting its endpoint. The web application and MySQL database run in a Pod. Both Pods have been exposed by a Service. The Service for the web application Pod is of type NodePort. The Service for the MySQL database is of type ClusterIP.

The following image shows the high-level architecture.

Obtain the host ip

kubectl get pod web-app -n gemini -o json | jq '.status.hostIP' -r
