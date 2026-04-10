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

For individuelle pods kan du sette gjennom
```yml
env: 
- name: KEY
  value: VALUE
```