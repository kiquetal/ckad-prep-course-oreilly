### Question 25

Team Sunny needs to identify some of their Pods in namespace sun. 
They ask you to add a new label protected: true to all Pods with an existing label type: worker or type: runner.
 Also add an annotation protected: do not delete this pod to all Pods having the new label protected: true.

kubectl config set-context --current --namespace sun

kubectl get pods -l "protected=true" 


kubectl label pod -l type=runner protected=true
kubectl label pod -l type=woker protected=true

kubectl annotate pod -l protected=true protected="do no delete this pod"



