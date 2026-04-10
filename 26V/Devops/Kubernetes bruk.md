Declarative model.
Describe what you want (desired state) in a manifest.
Kubernetes takes care of how.

```yaml
apiversion: apps/v1
kind: Deployment
metadata:
	name: web-deployment
```
POD:
Minste enheten. Inneholder en eller flere containere. Containere i en pod, deler ressurser.
Deployment:
Håndterer distribusjon av poder i clusteret.
Service:
Gi en fast ip addresse til alle podder i deploymenten.
Fast holdepunkt.

Docker compose. Usually put in a .env file or something.
Why is this hard in kubernetes environment

# .env kubernetes
Kubernetes forventer at det skal ligge i en pod spec.

For individuelle pods kan du sette gjennom
```yml
env: 
- name: KEY
  value: VALUE
```

Can be used for instance to split up permissions. Maybe some people can't set secrets, but just configmaps
### ConfigMaps
- Cluster aware .env
- Stored in the cluster store
- Injected into containers as env variables or mounted as files
### Secrets
- Same as ConfigMaps
- Base64 encoded
- *Not encrypted*

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: hello-cm
data:
  PORT: "8080"
    info.json: |
	  {
	    "containerImageArch":"macos/arm"
	  }

apiVersion: v1
kind: Secret
metadata:
  name: hello-scret
type: Opaque
data:
  MESSAGE: "SGVAWJDAJHWAD=" #base64
```
used with
```yaml
envFrom:
- secretRef:
  name: hello-secret
```
or
```yaml
	volumeMounts: # must be here
	- mountPath:
	  subPath:
volumes:
- name: hello-cm
  configMap:
    name: hello-cm
```

# Storage
PersistentVolume
- Physical piece of storage in infrastructure.
- Managed by th elcuster administrator
- Could be local harddrive, NFS or AWS etc.
PersistentVolumeClaim
- A "request" for storage
- Kubernetes provisions a PersistentVolume through a StorageClass
- The StorageClass is responsible for the physical storage

```yaml
kind: PersistentVoliumeClaim
metadata:
  name: data-pvc
spec:
  resources:
    requests:
      storage: 50Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce # only one has access too
```

In a deployements.
Add in volumes.
And volumeMounts

## Important stuff
Ingress (legacy)
- Simple routing of HTTP HTTPS traffic inside the cluster
- Limited to http routing, not entirely true
- Everything else handled by annnotations (very dependent on implementation)
Gateway API
- Built from the ground up to solve the fialures of Ingress.
- Can natively handle TCP, UDP and gRPC traffic.
- Most features are built into the core API, making it less vendor dependent.

To have more servers on one load balancer.
USE GATEWAY API

Ingress:
```yaml
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
  # Vendor specific magic notes
  nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
```
Potential for conlficts since amdinistrator and devleoper needs to touch it.

Gateway:
HTTPRoute and Gateway kinds
```yaml
kind: Gateway
metadata:
  name: external-web-gateway
```

```yaml
kind: HTTPRoute
metadata:
  name: api-route
  
```
https://gateway-api.sigs.k8s.io

