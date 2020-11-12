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
In the pipeline name give just a string, in the kubectl proxy field an ip/fqdn plus the port is needed e.g: 192.168.1.2:8080 and in namespace fill the one that you will be using in Kubernetes, default is the default namespace (who would have though it!).\
Global options settings can be an empty object e.g. {} but a default value is present to give a hint how it should be filled.\
From this field you can set settings that you need to pass to all the following deployments/apps.

Next you insert a AppToBeDeployed node anc chain the two.\
Again the three first field must be filled and the app settings is optional.\
The app name should be just a string.\
The deployment template must be a Kubernetes yaml file converted to json.\
Using an online converter like the following should be fine.\

https://onlineyamltools.com/convert-yaml-to-json

After you have your json template just paste it inside.\
You should know what you are doing with this template because each node the only check that makes is if some specific enviromental variables are present. If present it fills them, if not present it adds them.\
On this point I should mention that the enviromental variables that are passed on to the deployments are the app name, its nodeid, the previous node id, the next node id and two base64 encoded variables that contain the global and app settings to be used from the deployed app.\
If you need to use these settings, your app must base64 decode this two enviromental variables.\
Check the mqtttestapp repository if you need an example.\

https://github.com/aknts/mqtttestapp

Also in the BasicDockerContainer repository you can find an example how to build you container to use this enviromental variables with a nodejs app.

https://github.com/aknts/BasicDockerContainer/

In the Git url field you just add the git repository that you want to clone e.g. https://github.com/aknts/mqtttestapp .\
Finally in the app settings, an empty object e.g. {} but a default value is present to give a hint how it should be filled.
From this field you can set specific settings for this deployment/app.

If you need to deploy more apps just add more AppToBeDeployed nodes and just chain them back to back.

If you delete an app node, then also the deployment in the Kubernetes cluster is deleted.

If you edit the template, the changes will be passed on also on the actual deployment.

Rebooting the node-red server will not break the flow but the status of each node will not present.\
Using the inject button will re-populate each node status.

Finally, the nodes are not tested with multiple node chain e.g. two app nodes after a single one so use with caution.
