# Istio -- service-mesh

## Istio -- service mesh -- service to service communication in kubernetes

### What is service Mesh ?
#### A Service Mesh is a dedicated infrastructure layer that manages communication between microservices (service to service communication).
#### Without a service mesh, each application/service has to handle things like:
- Service-to-service communication
- Retries
- Timeouts
- TLS/mTLS
- Traffic routing
- Load balancing
- Metrics
- Distributed tracing
- Circuit breaking
#### A service mesh moves much of this communication logic out of the application code and into the infrastructure layer.


## Where does Istio come in? 
#### Istio is a service mesh platform for Kubernetes, Istio uses a sidecar proxy, traditionally Envoy, alongside your application container.

## Istio Architecture
### Modern Istio primarily has two major pieces:
- Control Plane : istiod --> It manages/configures the service mesh.
- Data Plane : Envoy handles the actual traffic.
```
                ISTIO
                  │
        ┌─────────┴─────────┐
        │                   │
     Control Plane       Data Plane
        │                   │
      istiod             Envoy Proxies
```


## Why do we need the Envoy proxy? 
#### Suppose you have:
```
frontend
   ↓
payment-service
```
#### Normally the frontend communicates directly with the payment service.
#### With Istio:
```
Frontend Pod
┌───────────────────────┐
│ Frontend Container    │
│         ↓             │
│ Envoy Sidecar         │
└──────────┬────────────┘
           │
           │ network
           ↓
┌───────────────────────┐
│ Envoy Sidecar         │
│         ↓             │
│ Payment Container     │
└───────────────────────┘
```
#### The application doesn't need to know about most of the advanced networking behavior, The Envoy proxies handle it.


## What can Istio do?
- Traffic management : Useful for Canary deployments.
- Retries
- Timeout
- Circuit breaking
- mTLS : Istio can encrypt service-to-service communication.
- Observability
