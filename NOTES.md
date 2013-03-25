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
* Floating IPs are the way you connect to an instance from your local machine
* Nova-network uses iptables to drive everything
* Security groups are implemented in iptables on the host running nova-network
* Floating IPs are NAT chain - link floating IP address to instance's fixed IP

## Openstack Quantum

* Nova-network was non-ideal
* Lots of NAT
* Code is kind of a mess - some of the oldest code Nova has
* Dying for a refactor
* Also - the Administrator has to do a lot of the legwork
* No way for tenants to define their own network topologies

# Openstack - Tenant Routers
* [Quantum API extension](http://docs.openstack.org/api/openstack-network/2.0/content/router_ext_concepts.html)
* Creates logical routers on the network

## Technologies used by plugins

* Not a comprehensive list
* Just a couple to give you an idea about how flexible Quantum is

## Quantum Plugins

* Linuxbridge plugin emulates the functionality of Nova-network
* Plugins for some vendors are for physical switching hardware

## Demo

* DevStack - very handy
* Automates all the stuff that you have to do as an admin
* Quickly get up and running
* Vagrant is great! Completely automates the steps that DevStack does not
* Two ways to access Nova
* python-novaclient
* fog library for Ruby
* Horizon
