# redkube
Node red sublows to deploy to a kubernetes cluster.

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

If you want to enable kubeproxy as a service place the kubectlproxy.service in your systemd folder.
For Debian installations that is the /lib/systemd/system/ directory.

Enable, start and check the service by using the following commands

systemctl enable kubectlproxy.service\
systemctl start kubectlproxy.service\
systemctl -l status kubectlproxy.service\

To stop it user the following command

systemctl stop kubectlproxy.service
