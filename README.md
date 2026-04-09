

curl.exe -LO "https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl.exe"

eksctl create cluster --name jhc-cluster --version 1.30 
--region us-east-1 --nodegroup-name ng-1 --node-type t3.medium --nodes 2 --nodes-min 1 --nodes-max 3

aws eks update-kubeconfig --region us-east-1 --name jhc-cluster


kubectl  create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl get pods -n argocd

# if applaicaiton controller fails:
kubectl apply --server-side -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl get crd | findstr applicationsets
# if it appears and deælete if (if does not delete it knows there is 1 remaining thing)
kubectl delete pod -n argocd -l app.kubernetes.io/name=argocd-applicationset-controller

# see if everything is correct
kubectl get pods -n argocd
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server -n argocd 8080:443


# to login, build and push
docker login -u ederoz -p edereder
docker build -t ederoz/test:v1 .
docker push ederoz/test:v1

kubectl get nodes
cd Workspace\gha-eks\k8s>
kubectl apply -f ./ # any yaml file

eksctl delete cluster --name jhc-cluster --region us-east-1


