#### **Exercice 2**

**a**. Héberger un premier Pod Nginx

```yaml
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

#### **Exercice 3**

**a**. A l’image du TP 1 sur Docker (question 7 et 8), héberger un Pod phpmyadmin et mysql, cette fois-ci en utilisant kind
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: phpmyadmin-pod
  labels:
    app: phpmyadmin
spec:
  containers:
    - name: phpmyadmin
      image: phpmyadmin/phpmyadmin:latest
      ports:
        - containerPort: 80
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mysql-pod
  labels:
    app: mysql
spec:
  containers:
    - name: mysql
      image: mysql:5.7
      env:
        - name: root
          value: password
      ports:
        - containerPort: 3306
```

**b**. Créer un service associé au Pod mysql  
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  selector:
    app: mysql
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
  type: ClusterIP
```