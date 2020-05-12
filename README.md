# grafana-ingress-nginx
Howto use ingress-nginx for expose grafana webui

## Usage

```bash
$ wget https://raw.githubusercontent.com/invaleed/grafana-ingress-nginx/master/grafana-values.yml
$ kubectl create ns monitoring
$ helm install grafana stable/grafana -f grafana-values.yml -n monitoring
```

Make sure you change this part

```yaml
ingress:
  enabled: true
  annotations:
    kubernetes.io/ingress.class: "nginx"
    nginx.ingress.kubernetes.io/rewrite-target: /$1
    nginx.ingress.kubernetes.io/use-regex: "true"

  path: /grafana/?(.*)
  hosts:
    - ""
 ```
 and replace with your ip address or FQDN.
 
 ```yaml
 server:
    root_url: http://10.58.8.240/grafana/
 ```
 
 and this part for set persistent volume
 
 ```yaml
 persistence:
  type: pvc
  enabled: true
  storageClassName: fast
  accessModes:
    - ReadWriteOnce
  size: 10Gi
  finalizers:
    - kubernetes.io/pvc-protection
  ```
  
  Cheers!
