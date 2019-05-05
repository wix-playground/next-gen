# Provisioning

## Common

Provisioning in our case has two big meanings:

1. Service provisioning
   1. Standard wix services (moving to k8s)
   1. Generic services (dispatchers, zk, etc. Most of them also can be moved to k8s)
1. Infrastructure provisioning
   1. Network part (VPC, subnets, connectivity)
   1. Security (Firewalls/security-groups/ACLs)
   1. Instances and other objects (instances, instance groups, load balancers)
1. @WIgor I think, we need more grannular release process. Test bed should grow to something like blue-green deployment with fast switch between versions. With deploy only to one DC initially. May be A/B DCs - A for stable environment, B - for "possible beta releases".

## Infrastructure

### Blocks

* Infrastructure - it's set of network objects and instances.
* All objects can be joined in blocks.
* Each block has his own cached state in global state storage.
* Each block may be depended from other block or blocks.

### State storage: To discuss

As state storage we can use the current solution with storing data in file object on aws/gce storage. Or we can use different solution (incompatible with terraform) to store cached data and objects idendificators (for aws)

With current solution we allow to everyone with permissions to run provisioning software (terraform) and implement only part of changes. This is bad practice, because we have constantly inreasing gap between real state and configuration. To awoid this we need to forbid all "parsonalized" changes and run provisioning from dedicated servers. This will allow us to build dependency tree and run proviosioning in correct order, probably in parallel between dc.

With correct definition of object we will be abble to define test conditions (healthchec, etc) for each block and before apply everything in prod - run tests on staging.

## DataBases

see [databases document](./Databases.md)

According to BI data we can understand which location is preferred for particular domain and place corresponding databses in this location. Also we shall be able to move that shard to different location.  
(Jony C: I think this could be valuable info when we shard data with R&D)

Probably, with good content cache policy we can awoid this.  
(Jony C: not likely for many reasons)

## WIX-Service

Everything in k8s.

Do k8s PCI compliant?

## Generic service

### DNS

Do we really need internal dns servers to resolve objects between DC's?

Actually, we have al lot of legacy rewriting rules and lot of views only to be able use hostnames for ssh and some addresses. Most of this addresses are already in consul dns or can be added to consul.

### Zookeeper

### Dispatchers
