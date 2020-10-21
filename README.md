# mqttnodered
Node red sublows to deploy STRAND

STRAND is a trilateration app based on Kubernetes for scaling up depending on the receiving data.
Data is exchanged between each component with MQTT.

http://snf-825292.vm.okeanos.grnet.gr/ktserpes/STRAND

Subflows are being built as abstract they can be allowing other apps to deploy use the node red as a deployment platform.
Repository name might change, so please check again if you are plan to use the specific subflows.

Installation
Before you import the subflows node-red-contrib-md5 must be installed.

https://flows.nodered.org/node/node-red-contrib-md5

From there just use the node-red gui to import the two subflows.
The first one is for some global settings and the second a generic app node.
Node red must be able to access your kubernetes installation and to be more specific the kubernetes proxy that must be running.
