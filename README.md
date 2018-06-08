# deploy app
kubectl create -f canvas-ns.yml

kubectl create -f postgres-svc.yml
kubectl create -f postgres-deployment.yml
kubectl create -f canvas-cm.yml
kubectl create -f canvas-svc.yml
kubectl create -f canvas-deployment.yml

kubectl get pods --namespace=canvas

# bootstrap database
kubectl exec -it --namespace=canvas <POD_NAME> -- bash
bundle exec rake db:create db:initial_setup


# delete allthethings
kubectl delete --all pods,deployments,services,configmaps --namespace=canvas
