#### Set taint and tolerations for a node

kubectl get nodes

kubectl taint nodes <node-name>  dedicated=especial:NoSchedule

k run nginx --image nginx --dry-run=client -o yaml > pod-one.yaml


on pod spec:

   tolerations:
   - key: dedicated
     operator: Equal
     value: especial
     effect: NoSchedule
