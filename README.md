# osp_lbaasv2_install
lbaasv2.sh - shell script for installing lbaav2 on Red Hat OSP 10  
post_config.yaml - resource registry for installing through TripleO class OS::TripleO::Tasks::ControllerPostConfig
lbaasv2.yaml - heat template with bash code from from lbaasv2.sh called by post_config.yaml  

To install through OSP Director modify the 'match' variable to match your controller/network nodes.  
Add this to your deployment:  

openstack overcloud deploy --templates -e \<path to\>/post_config.yaml 

Be sure to check out the lbaasv2 directory of https://github.com/CFields651/osp_tempest-tools to test your lbaasv2 installation with tempest.  

## details
This installaton is based on documentation for Red Hat OpenStack Platform 10 located here:

https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/10/html/networking_guide/sec-lbaas    

The code in this repo should work for:  

$ rpm -qi openstack-neutron-lbaas  
Name        : openstack-neutron-lbaas  
Epoch       : 1  
Version     : 9.1.0  
Release     : 4.el7ost  

This presumes that the haproxy service is installed and running.  

When you start the neutron-server servive it logs this warning in /var/log/neutron/server.log:  
WARNING stevedore.named [-] Could not load neutron_lbaas.drivers.haproxy.plugin_driver.HaproxyOnHostPluginDriver   

When you start the neutron-lbaasv2-agent it logs these warnings in /var/log/neutron/lbaas-agent.log:    
WARNING stevedore.named Could not load neutron.agent.linux.interface.OVSInterfaceDriver  
WARNING stevedore.named Could not load neutron_lbaas.drivers.haproxy.namespace_driver.HaproxyNSDriver  

Despite the warnings, the load balancer seem to work.  Here are good instructions:  
https://docs.openstack.org/ocata/networking-guide/config-lbaas.html  


