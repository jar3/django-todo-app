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

# DEBUGUEAR
# Entrar al pod
kubectl exec -it $(kubectl get pod -l app=django-todo -o name) -c django-todo -- bash

# Dentro del pod, verificar que el servicio responde
curl -v localhost:8000

# Entrar al shell de Django
kubectl exec -it $(kubectl get pod -l app=django-todo -o name) -c django-todo -- python manage.py shell

# Dentro del shell de Python
from django.conf import settings
print(settings.CSRF_TRUSTED_ORIGINS)
print(settings.CSRF_COOKIE_SECURE)
print(settings.ALLOWED_HOSTS)
