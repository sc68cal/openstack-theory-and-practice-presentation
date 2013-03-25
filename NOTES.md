### tl;dr 

* Started as a project at NASA
* Community has standardized on Python
* If you plan on building something and want to release it to the community - no exceptions


## Original Project - Nova

* Nova was released in 2010
* Originally just provided EC2 API compatability 
* Rackspace donated their project that provided the S3 API 

## Components - Essex era

* Swift is the project that originally came from RackSpace
* Keystone is what ties everything together
* Horizon dashboard based upon Django

## OpenStack Architecture
* Uses RabbitMQ for RPC - components can be decentralized

## Compute Example: "Create a VM"

* Many different Hypervisors are supported

## Notes about Folsom Architecture

* Block storage had growing pains 
* Needed to be split into separate project
* Cinder has plugin/backend design - LVM, NetApp, Ceph, etc...
* Quantum - same thing - growing pains - very simple networking

## Networking

* Essex era - fairly simple networking
* Basically L2 broadcast domain, or VLANs

## Nova-Network

* Third network type is dumb - FlatManager
* Admin uses VNC to log into VMs - configure networking manually
* Uses dnsmasq processes to offer DHCP to instances
* Nova-Network injects parameters into the dnsmasq configuration file, then SIGHUP
* Sort of brittle
* Also - what if you don't like dnsmasq? 
* What if you prefer isc-dhcpd or another DHCP server implementation?

## Instance Networking

* Ideally - if you are running batch type jobs - use Fixed IPs 
* Some networking modes (like FlatDHCPManager) mix tenants in same L2 domain

## Technologies used by plugins

* Not a comprehensive list
* Just a couple to give you an idea about how flexible Quantum is

## Quantum Plugins

* Linuxbridge plugin emulates the functionality of Nova-network
* Plugins for some vendors are for physical switching hardware
