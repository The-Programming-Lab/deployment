# The Programming Lab Ingress Configurations

This repository contains Kubernetes Ingress configurations for different components of `theprogramminglab.com` architecture. There are three primary Ingress configurations:

1. **Host Ingress**
2. **Client Ingress**
3. **API Ingress**

## 1. Host Ingress
The host ingress is mainly used to redirect to user's deployed website. The associated domain is `host.theprogramminglab.com`. For example, for user `Braeden6`, the user's deployed website can be accessed via `host.theprogramminglab.com/user/Braeden6`.

The configuration includes a ManagedCertificate for HTTPS traffic, a FrontendConfig for HTTP to HTTPS redirection, and an Ingress rule that routes traffic to the appropriate backend service.

## 2. Client Ingress
The client ingress is used for the frontend Next.js application. The domain associated with this ingress is `theprogramminglab.com`. The configuration is similar to the host ingress but routes traffic to the frontend application instead.

The ingress includes a ManagedCertificate for HTTPS traffic, a FrontendConfig to redirect HTTP to HTTPS, and an Ingress rule to route traffic to the main-client service.

## 3. API Ingress
The API ingress is responsible for all our microservices. The associated domain is `api.theprogramminglab.com`. Different paths correspond to different microservices. For instance, the `/v1/auto-builder` path is handled by the `auto-builder-ms` service, while the `/v1/auth` path is handled by the `auth-ms` service.

Like the other ingresses, it includes a ManagedCertificate for HTTPS, a FrontendConfig for HTTP to HTTPS redirection, and Ingress rules to route the traffic to the respective microservices.

All of the ingress configurations enable both HTTP and HTTPS traffic, but with a preference for HTTPS via redirection from HTTP. The `MOVED_PERMANENTLY_DEFAULT` response code indicates that all HTTP traffic should be permanently redirected to HTTPS.


### Set up 
Add the following DNS records to your domain:
```
gcloud compute addresses create tpl-client --global
gcloud compute addresses create tpl-api --global
gcloud compute addresses create tpl-host --global
```
