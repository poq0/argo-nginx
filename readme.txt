install argo
 kubectl create namespace argocd
 kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

see in browser
 kubectl get services -n argocd
 kubectl port-forward service/argocd-server -n argocd 8080:443

username: admin
password: kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
or just argocd admin initial-password -n argocd

password can be changed in browser (User Info > Update password)
delete initial password
 kubectl get secrets -n argocd   or  kubectl get secrets --all-namespaces
 kubectl delete secret argocd-initial-admin-secret -n argocd

argocd login localhost:8080

delopy from git
argocd app create argo-demo ^
  --repo https://github.com/poq0/argo-nginx.git ^
  --path k8s ^
  --dest-server https://kubernetes.default.svc ^
  --dest-namespace argo-demo

argocd app list
argocd app sync argo-demo
argocd app list
kubectl get deployment -n argo-demo


kubectl apply -f k8s
kubectl delete -f k8s

