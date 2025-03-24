+++
date = '2025-03-23T20:32:16-05:00'
title = 'Kubernetes Administrator CKA'
+++

## PODs
### Imperativo
`kubectl run myapp-pod --image=nginx --dry-run=client -o yaml > myapp-pod.yaml` 
Construye un archivo yaml que hace referencia a un pod con la imagen descrita
### Declarativo
```bash
apiVersion: v1
kind: Pod
metadata:
    name: myapp-pod
    labels:
        app: myapp
        type: front-end    
spec:
    containers:
        - name: nginx-container
          image: nginx
```

## Deployments
### Imperativo
`kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml`

### Declarativo
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
    name: myapp-deployment
    labels:
        app: myapp
        type: front-end    
spec:
    template:
        metadata:
          name: myapp-pod
          labels:
             app: myapp
             type: front-end    
        spec:
          containers:
          - name: nginx-container
            image: nginx
replicas: 3
selector: 
    matchLabels:
        type: front-end
```

## Services
### Node Port
![](Pasted%20image%2020250323210547.png)
```bash
apiVersion: v1
kind: Service
metadata:
    name: myapp-service
spec:
    type: NodePort
    ports:
        - targetPort: 80
          port: 80
          nodePort: 30008
    selector:
        app: myapp
        type: front-end
```

### Cluster IP
Servicio de Kubernetes que nos permite agrupar los PODs y proporcionar una sola interface de acceso hacia los PODs
![](Pasted%20image%2020250323210857.png)

```bash
apiVersion: v1
kind: Service
metadata:
    name: back-end
spec:
    type: ClusterIP
    ports:
        - targetPort: 80
          port: 80
                    
    selector:
        app: myapp
        type: back-end
```

### LoadBalancer
```bash
apiVersion: v1
kind: Service
metadata:
    name: myapp-service
    
 spec:
     type: LoadBalancer
     ports:
         - targetPort: 80
         port: 80
         nodePort: 30008
```
Soporte en: AWS, Azure, GoogleCloud
