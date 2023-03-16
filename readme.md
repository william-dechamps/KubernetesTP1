#### **Exercice 2**

**a**. Héberger un premier Pod Nginx

```
ApiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Ajout du pod dans le namespace default
```
kubectl apply -f pod-nginx.yaml
```

**b**. A l’aide de la commande kubectl port-forward et d’un navigateur accéder à la page par défaut de votre pod Nginx  
``` 
kubectl port-forward pod/pod-nginx 3000:80 
```