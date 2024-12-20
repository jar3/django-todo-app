DB
kubectl apply -f postgres-pv.yaml
kubectl apply -f postgres-pvc.yaml
kubectl apply -f postgres-configmap.yaml
kubectl apply -f postgres-secret.yaml
kubectl apply -f postgres-deployment.yaml
kubectl apply -f postgres-service.yaml

APP
kubectl apply -f django-configmap.yaml
kubectl apply -f django-secret.yaml
kubectl apply -f django-deployment.yaml
kubectl apply -f django-service.yaml


kubectl get svc django-todo
# Para hacer port-forward (aunque con NodePort no es estrictamente necesario):
kubectl port-forward svc/django-todo 8000:8000

# O puedes acceder directamente usando el nodePort:
# http://node-ip:30000
