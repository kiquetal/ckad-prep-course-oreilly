#### Probes

| Method | Option | Description |
| ------ | ------ | ----------- |
| Custom command | exec.command | Execute command inside of the container |
| HTTP GET request | httpGet | sends a http get to and endpoint exposed by application |
| TCP Connection | tcpSocket | Tries to open a TCP connection to a port.|
| gRPC | grpc | The application implements the GRPC Health Checking protocol | 


| Attributes | Default Values | Description|
| ---------- | -------------- | ---------- |
| initialDelaySeconds | 0 | Delay in seconds until firsth check is executed |
| periodSeconds | 10 | Interval for executing a check | 
| timoutSeconds | 1 | maxinum number of seconds until the check opration times out | 
| successThreshold | 1 | Number of successful check attemps until probe is considered successful after a failure | 
| failureThreshold | 3 | Number of failures for check attempts before probe is marked failed and takes action | 
| terminationGracePeriodSeconds | 30 | grace period before forcing a container stop upon failure | 
