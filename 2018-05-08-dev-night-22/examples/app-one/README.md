## App One

![](img/mcp.png)

### create pod
```sh
kubect create -f app.yml
```

### access pod
```sh
kubectl exec -ti mc1
```

```sh
tail -f /usr/share/nginx/html/index.html
```
