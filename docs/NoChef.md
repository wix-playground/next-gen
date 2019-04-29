# No Chef

Right now we are using chef-server as part of infrastructure and service proviosioning.
We have a lot of legacy code as from wix and from community.

## Disadvantages

* unclear dependencies between cookbooks
* and old bad practice to use community cookbooks with just copy them into wix-cookbooks tree
* no clear splitting between prod/dev environments (because we have multiple environments)
* no (or very tricky) staging procedure and therefore no automation tests
* single point of failure
* speed of deployment (especialy on remote sites)

## Current state and main functions

* user management
* package management (actually, only for initial install and very rare updates)
* wix-service deployment
* system services
  * dns
  * dispatchers/routers
  * zookeeper
  * elasticsearch
  * etc.
* DB management
* PCI env management
* Instance bootstrap/image creation

## Proposed solution

### k8s

* user-management: not required in most cases (no users on nodes). If required - LDAP is better solution (we already have ssh public keys somewhere in self password management)
* package management: not required. All images are pre-built with correct set of packages. If new version is required - new image shall be provided.
* wix-services: all deployment is working
* system services
  * dns: moving to public zones will allow us to not use internal dns with custom rules (just caching). Even more. We don't need our internal dns servers
  * dispatcher/routers: build/test packages with config files for all required dc/type. This will allow us to test and fast roll-back.
  * zookeeper: switch to native etcd in k8s
  * elasticsearch: move inside k8s. Probably, designated cluster
* DB: we also can move DB into k8s with persistent nodes/disks. This will allow us to manage access easily with network policies
* PCI: ~~
* Instance bootstrap/image creation: do not use custom instance bootstrap procedures. Pre-build images for all required cases (with automation) with f.e. ansible
