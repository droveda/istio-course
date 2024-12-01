# What is Istio?
Istio is a "Service Mesh"  

## What is a Service Mesh?
A Service Mesh is an extra layer of software you deploy alongside your cluster (eg Kubernetes)  

* Microservice (POD)
  * Container 01
  * Proxy

* Namespace -> istio-system (the Control Plane)
  * istiod (Istio Daemon (used to be called "pilot")) 
  * Kiali UI

Note: **The Proxies are collectively called the "Data Plane" in Istio**    


## Istio Install instructions
* Official site: https://istio.io/latest/docs/setup/getting-started/

### Instructions that I followed for mac m1
* Ensure Docker Desktop is installed and Kubernetes is enabled
  * `kubectl cluster-info`
* Download Istio for ARM64 MAC M1
  * https://github.com/istio/istio/releases/tag/1.24.0
  * https://storage.googleapis.com/istio-release/releases/1.23.3/istioctl-1.23.3-osx-arm64.tar.gz
  * `curl -L https://istio.io/downloadIstio | sh -`
* Add istioctl to Your Path
  * `export PATH=$PWD/bin:$PATH`
* Verify compatibility
  * `istioctl x precheck`
* Install Istio
  * `istioctl install --set profile=demo -y`
* Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later:
  * `kubectl label namespace default istio-injection=enabled`
* Verify the installation
  * `kubectl get pods -n istio-system`

### 1st Hands-on
* cd istio/arm64_v11/warmup-exercise
* kubectl apply -f -> apply all the files
* `kubectl label namespace default istio-injection=enabled`(This will enable istio sidecar injection)
* kubectl get ns default -o yaml
* Re-apply the application yamls
  * `kubectl delete -f 4-application-full-stack.yaml`
  * `kubectl -f 4-application-full-stack.yaml`
* Access the app frontend -> http://localhost:30080
* Access Kiali -> http://localhost:31000
  * Kiali answers the questions:
    * What microservices are part of my Istio service mesh?
    * How are they connected?
    * How are they performing?
* Access JaegerUI -> http://localhost:31001
* Change file warmup-exercise/4-application-full-stack.yaml, line 280 add a timeout of 1 second

## Envoy
envoyproxy.io  
Envoy is an open source edge and service proxy, designed for cloud-native applications  
Istio Simplifies Envoy -> Istio understands Kubernetes  
We can use regular Kubernetes yaml (via CRDs) which get transformed into Envoy configuration automatically...  



