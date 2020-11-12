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
The first one is for some global settings and the second a generic app node with per app settings.
Node red must be able to access your kubernetes installation and specifically the kubernetes proxy.

If you want to enable kubeproxy as a service place the kubectlproxy.service in your systemd folder.
First edit the accepted hosts and the address option to fit your installation.
For Debian installations that is the /lib/systemd/system/ directory.

Enable, start and check the service by using the following commands

systemctl enable kubectlproxy.service\
systemctl start kubectlproxy.service\
systemctl -l status kubectlproxy.service

To stop it user the following command

systemctl stop kubectlproxy.service

Instructions

After you have imported the two subflows, two new nodes will be present at the top of the nodes menu.\
First you add an inject node, we need this to start the deployment flow. Keep everything on default.\
After that you add the global settings node. Pipeline name, Kubectl proxy and Kubernetes namespace are crucial and must be field.\
Global options settings can be an empty object e.g. {} but a default value is present to give a hint how it should be filled.
