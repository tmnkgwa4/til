# Certification Tips!

## Manifest yaml fileの生成
### Pod
```
kubectl run nginx --restart=Never --image=nginx --dry-run -o yaml
```

### Deployment
```
kubectl run nginx --restart=Always --image=nginx --dry-run -o yaml
```

### Replicas 4 の Deployment
```
kubectl run nginx --restart=Always --replicas=4 --images=nginx --dry-run -o yaml
```

