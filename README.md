# nginx-ingress-controller-submariner

Problem Summary

The root of the problem lies in the following observations:


	1.	Default NGINX Behavior: When no pods (or endpoints) are available in a Kubernetes service, the upstream configuration in NGINX defaults to 127.0.0.1:8181. This behavior, while standard, causes issues when working with services that rely on DNS manipulations rather than Kubernetes Endpoints.

	2.	Submariner.io Approach: Submariner.io operates differently by relying on DNS manipulations, which conflicts with the Kubernetes-based service discovery mechanism used by the NGINX ingress controller. 
 
	3.	ExternalName Limitation: While using the ExternalName Service type is a valid solution, it is primarily supported by NGINX Plus and may not work as expected with the OSS (open-source) version of the NGINX ingress controller.


The Solution

The provided configuration file (cm-submariner-io-helper.yaml) introduces a declarative approach to resolving the issue. It does this by leveraging a Kubernetes ConfigMap to explicitly define the upstream configurations for Submariner.io services.

This configuration works by:
TBD


Original NGINX ingress controller template file:
https://github.com/nginxinc/kubernetes-ingress/blob/v3.7.2/internal/configs/version1/nginx.ingress.tmpl

Most of the changes are here:
![image](https://github.com/user-attachments/assets/d306a242-e4b0-48ec-bd26-d8373d76ebe8)

