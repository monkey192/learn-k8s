### Configmap & how to use it
- declare configmap
- use configmap in pod by `volume`
- use configmap in pod by `env variables`

### apply 
`kubectl apply -f .`

```sh
sh-3.2$ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5dcd64d74-8l26t   1/1     Running   0          4m39s
nginx-5dcd64d74-dzwcx   1/1     Running   0          4m35s
```

### Go into pod
`kubectl exec -it nginx-5dcd64d74-8l26t -- /bin/sh`

```sh
sh-3.2$ kubectl exec -it nginx-5dcd64d74-8l26t -- /bin/sh
# printenv
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT=tcp://10.96.0.1:443
HOSTNAME=nginx-5dcd64d74-8l26t
HOME=/root
PKG_RELEASE=1~bullseye
TERM=xterm
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
NGINX_VERSION=1.21.6
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_PORT=443
NJS_VERSION=0.7.2
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_SERVICE_HOST=10.96.0.1
PWD=/
DB_HOST=fuga   <- ConfigMap value is passed by ENV
```
  
### Confirm mount volumes
```sh
# cd /mount
# ls -l
total 0
lrwxrwxrwx 1 root root 14 Feb 24 08:14 DB_HOST -> ..data/DB_HOST
lrwxrwxrwx 1 root root 14 Feb 24 08:14 DB_NAME -> ..data/DB_NAME
lrwxrwxrwx 1 root root 10 Feb 24 08:14 ENV -> ..data/ENV
# cat DB_HOST
fuga# 
```