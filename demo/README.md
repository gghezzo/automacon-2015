# AutomaCon Demo

## Setup

### Terminal 3

```
kubectl get events --watch-only
```

## Automated Deployments

```
kubectl get pods,rc,svc
```

```
cat rc/nginx.yaml
```

```
kubectl create -f rc/nginx.yaml
```

```
kubectl describe rc nginx
```

```
kubectl get pods
```

Scale out

```
kubectl scale rc nginx --replicas=5
```

```
kubectl get pods --watch-only
```

### Create the nginx service

```
kubectl create -f services/nginx
```

```
kubectl describe svc nginx
```

```
kubectl scale rc nginx --replicas=10
```

```
kubectl describe svc nginx
```

```
kubectl scale rc nginx --replicas=5
```

```
kubectl describe svc nginx
```

#### Working with pods

```
boom -n 10000 -c 10 http://<node-public-ip>:36000
```

```
kubectl logs -f <pod>
```

```
kubectl exec <pod> cat /etc/os-release
kubectl exec <pod> -- uname -a
```

### Rolling update

#### Terminal 1

```
kubectl rolling-update --update-period=500ms --image=nginx:1.9.4 nginx
```

#### Terminal 2

```
while true; do curl -si http://<node-public-ip>:36000 | grep Server; sleep .5; done
```

#### Terminal 3

```
kubectl get pods --watch-only
```

### Clean up

```
kubectl delete rc nginx
```

## Resource utilization

Let the games begin!

- Play with your eyes closed
- Play with eyes open.
- What happens when you try and bolt Kubernetes on existing infrastructure. (B mode)
- What happens when you try and bolt Kubernetes on really bad environments. (B mode)

### Resource quotas

```
cat quotas/prod.yaml
```

```
kubectl create -f quotas/prod.yaml
```

```
kubectl describe quota prod
```

```
cat pods/nginx.yaml
```

```
kubectl create -f pods/nginx.yaml 
```

```
cat pods/nginx-custom.yaml 
```

```
kubectl create -f pods/nginx-custom.yaml
```

```
kubectl describe quota prod
```

```
kubectl delete pods nginx-custom
```

```
kubectl create -f limits/prod.yaml
```

```
kubectl create -f rc/nginx.yaml
```

```
kubectl describe quota prod
```

```
kubectl scale rc nginx --replicas=20
```

```
kubectl create -f rc/nginx-large.yaml
```

```
kubectl scale rc nginx-large --replicas=5
```
