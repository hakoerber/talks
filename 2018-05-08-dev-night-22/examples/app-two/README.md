## App TWo


### create minikube
```sh
minikube start
```

### create persistent volume
```sh
kubectl create -f k8s/database-pv.yml
```

### create database pod
```sh
kubectl create -f k8s/database.yml
```

### fix database config
```sh
kubectl exec -ti <database-pod-name> /bin/bash

apt-get update && apt-get install nano

nano /var/lib/postgresql/data
```

### create api pod
```sh
kubectl create -f k8s/api.yml
```

### create nginx(frontend) pod
```sh
kubectl create -f k8s/nginx.pod
```

### create required database tables
```sh
kubectl exec -ti <api pod name> alembic upgrade head
```
