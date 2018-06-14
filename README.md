# start minikube
minikube start


# deploy app
kubectl create -f postgres-svc.yml \
  && kubectl create -f postgres-deployment.yml \
  && kubectl create -f canvas-cm.yml \
  && kubectl create -f canvas-svc.yml \
  && kubectl create -f canvas-deployment.yml

kubectl get pods

# bootstrap database
kubectl exec -it <POD_NAME> -- bash
bundle exec rake db:create db:initial_setup

# load up service
minikube service canvas --url


# delete allthethings
kubectl delete --all pods,deployments,services,configmaps
