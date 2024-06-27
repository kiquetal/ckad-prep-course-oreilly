### Create a pod named consumer with the image nginx:1.25.3-alpine in the namespaces nextapp
and consume the configmap as volume


	kubectl run consumer --image=nginx1.25.3-alpine --dry-run=client -o yaml  -n nextapp > pod.yaml

	kubectl config get-contexts

 	kubectl config set-context --current --namespaces=nextapp


