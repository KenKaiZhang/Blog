# HTTP Load Balancing with Ingress

**_Kubernetes's HTTP-based load balancing system. A collection of routing rules that govern how external users access services running in a Kubernetes cluster._**

Follows the **virtual hosting** pattern used by many HTTP sites

- a reverse proxy receives incoming HTTP/HTTPS connection and redirects the connection to the proper folder based on the incoming URL and Host header
- allows for multiple names on the same IP
  - www.test.com and www.teaser.com can have the same IP but will show contents from test and teaser respectively
  - allows for different permissions because contents are in folders

Ingress configuration must be handled by user

## Ingress Spec VS Controllers

Users must install an Ingress controller

- up to the user to install and manage an outside controller

## Using Ingress

```yaml
// simple-ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: simple-ingress
spec:
  defaultBackend:
    service:
      name: alpaca
      port:
        number: 8080
```

Run `kubectl apply -f simple-ingress.yaml` to create this Ingress that blindly passes eevrything to the upstream (alpaca) service

```yaml
// host-ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: host-ingress
spec:
    defaultBackend:
        service:
            name: be-default
            port:
                number: 8080
        rules:
            - host: alpaca.example.com
              http:
                paths:
                    - pathType: prefix
                      path: /
                      backend:
                        service:
                            name: alpaca
                            port:
                                number: 8080
```

`host-ingress.yaml` sets up a rule that only requests with host header `alpaca.example.com` will be allowed redirection to the `alpaca` service, otherwise it will be sent to `be-default` (both on port 8080)

- for `path`, it is possible to set it to something like `/test` so only requests with `alpaca.example.com/test` will be redirected to the `alpaca` service

## Serving TLS

**_Adding a Transport Layer Security allows for more secure websites_**

Users must specify a Secret with their TLS certificat and keys that must be uploaded to be refrenced in an Ingress object

_Making a Secret_

```yaml
apiVersion: v1
kind: Secret
metadata:
  creationTimestamp: null
  name: tls-secret-name
type: kubernetes.io/tls
data:
  tls.crt: <base64 encoded certificate>
  tls.key: <base64 encoded private key>
```

_Ingress object specifying a list of certificates and hostnames that the cerificates are used for_

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: tls-ingress
spec:
    tls:
        - hosts:
            - alpaca.example.com
          secretName: tls-secret-name
        rules:
            - host: alpaca.example.com
              http:
                paths:
                    - backend:
                        serviceName: alpaca
                        servicePort: 8080
```

**_Read more on TLS_**
