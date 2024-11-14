---
aliases:
  - K8
---
An open source system for automating, deploying, scaling and managing containerized apps

Clusters - Compute resources which are organized to work as one unit
Control Plane - Manages the cluster. Has different tool
	API server - front end of the control plane
	scheduler - identifies any pods with no assigned node
	etcd - provides highly-available key value
	control manager - cloud specific control logic
	proxy - network proxy that coordinates with real networking.
Nodes - The compute (VM or physical) which acts as a worker.
Kubelets - An agent that runs on the nodes and communicates with the control plane
Job - ad-hoc, creates one or more pods
Pods - Smallest unit of computing. Don't think of them as permanent
ingress - exposes a way into a service
ingress controller - used to provide ingress
persistent storage (PV) - volume whose lifecycle lives beyond any 1 pod that uses it

in AWS we use the service [[Elastic Kubernetes Service]]