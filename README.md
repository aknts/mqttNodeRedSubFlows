# redkube
Node red sublows to deploy kubernetes deployments.

Build initially to deploy STRAND but same subflows can now deploy any app having in mind some minimum requirements.

STRAND is a trilateration app based on Kubernetes for scaling up depending on the receiving data.
Data is exchanged between each component with MQTT.

http://snf-825292.vm.okeanos.grnet.gr/ktserpes/STRAND

Installation
Before you import the subflows node-red-contrib-md5 must be installed.

https://flows.nodered.org/node/node-red-contrib-md5

From there just use the node-red gui to import the two subflows.
The first one is for some global settings and the second a generic app node.
Node red must be able to access your kubernetes installation and specifically the kubernetes proxy.


