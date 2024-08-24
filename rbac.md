### Creating roles

kubectl create role read-only --verb=list,get,watch --resource=pod,deployment,services


### List roles

kubectl get roles

kubectl describe role read-only


### Creating role binding

kubectl create rolebinding read-only-binding --role=read-only --user=bmushcko
