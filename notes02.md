# Telemetry

* Will be using:
  * Kiali
  * Jaeger
  * Grafana
  * Files in the folder "1-Telemetry"
  * Will need to restart the kubernetes service in order to clean everything
  * Install istio and Apply the yaml files in order
  * OBS, do not forget to Execute: `kubectl label namespace default istio-injection=enabled`

## Kiali Deeper Dive
Telemetry Requirements:  
* You need a (Envoy Sidecar) Proxy sidecar running in every pod you want to monitor
* The control plane needs to be running (ie istiod and kiali, jaeger, grafana)
* kiali url: `http://localhost:31000`

### Virtual Services and Destination Rules
* kubectl get virtual services
* kubectl get vs
* kubectl get destinationrules
* kubectl get dr
* You can create these using the Kiali UI, right click on a service and using the "Actions" option

### Distributed Tracing
* Opentelemetry - https://opentelemetry.io/
* Distributed tracing lets you observe requests as they propagate through complex, distributed systems. Distributed tracing improves the visibility of your application or system’s health and lets you debug behavior that is difficult to reproduce locally. It is essential for distributed systems, which commonly have nondeterministic problems or are too complicated to reproduce locally.
* Client library for a particular language
* https://opentelemetry.io/docs/concepts/observability-primer/
* With a service mesh all of this down at the proxy level
  * with istio we don't have to use these client libraries at all
* Traces:
  * The path of a request through your application.
  * Traces give us the big picture of what happens when a request is made to an application. 
* Span:
  * A span represents a unit of work or operation. Spans are the building blocks of Traces

#### Metrics with Grafana
* Access the following URL: http://localhost:31002/
* It takes some time to load
* Navigate to home and select one of the already pre-built dashboards
* Some useful dashboards:
  * Istio Sevice Dashboard
  * Istio Workload Dashboard

# Traffic Management

## Canary Releases
* will be using folder "2-Traffic" files

Deploy a new version of a software component (for us, new image)  
But only make that new image "live" for a percentage of the time  
Most of the time, the old (definitely working) version is the one beign used  

### What is a VirtualService?
A VirtualService enables us to configure custom routing rules to the service mesh  

Where does a VirtualService fit in?  
Virtual Services Configure the Proxies!  

* Points to Note:
  * Despite the name, VirtualService and Service are not really related
  * VirtualServices do not replace Services - they do different jobs
  * You only need a VirtualService if you need one!

### What is Destination Rule?