# run/create/expose の run

## kubectl run
### Pod を oneliner で作成する
```
😀 ❯❯❯ k run nginx --image=nginx --restart=Never
pod/nginx created

😀 ❯❯❯ k get pod
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          40s
```

### Pod に env を指定して作成する
```
😀 ❯❯❯ k run nginx --image=nginx --restart=Never --env=TESTENV=testvalue
pod/nginx created

😀 ❯❯❯ k exec nginx env | grep test
TESTENV=testvalue
```

## Pod と containerPort を指定して作成する
```
😀 ❯❯❯ k run nginx --restart=Never --image=nginx --port=8080
pod/nginx created

😀 ❯❯❯ k get pod -o json | grep Port
                                "containerPort": 8080,
```

## Pod と Resouce制限を加えて作成する
```
😀 ❯❯❯ k run nginx --restart=Never --image=nginx --requests='cpu=100m,memory=50Mi' --limits='cpu=200m,memory=100Mi'
pod/nginx created

😀 ❯❯❯ k get pod -o json | jq -r '.items[].spec.containers[].resources'
{
  "limits": {
    "cpu": "200m",
    "memory": "100Mi"
  },
  "requests": {
    "cpu": "100m",
    "memory": "50Mi"
  }
}
```


## Reference
- [kubectl run/create/expose のススメ](https://qiita.com/sourjp/items/f0c8c8b4a2a494a80908)
