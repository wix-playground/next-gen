# Databases (Initial high level draft)

## Scalability
Our main path of growth for scalability in the data layer will be provided by sharding of data stores.
we plan to provide sharding both for data locality and to accomodate growth in a single region.

### Geo-Sharding 
we'll provide Local Writes on all DCs with data replicated to main buckets for backups and cross-DC data movment.
This will require transfer of traffic location between the different layrs of the deployment architecture.  
(This is a requirement probably on both Networking and NASA project.)

## High Availability
Another main focus point for the DB team is around automation of failovers and DR.
while this is rather straight FWD in our "old" 2 main DC architecture this will no longer be the case with geo-location of the data.  
(This will raise requirments for integration with the Networking and probably NASA )

## Provisioning
For DB provisioning we will use 2 methods:
1. k8s - for most dbs 
1. Provisioned servers - until there is enough support to cover all our use-cases.  

(This will require support for DB dedicated nodes - R5 with EBS)

## Self Service
DB services will all be provided by self service portals including (but not limited to)
1. db provisioning
1. dev replica provisioning
1. schema changes

this requires us to be able to dynamically provision all resources.
with k8s this is mostly easy (although underlying nodes layer should be able to grow fast to accomodate needs)

also non-k8s layer (until we will no longer need it) should be dynamically allocated.

## Backup & Restore
Backups & restores will be provided by disk snapshots based system.
This requires us to be able to ship backup data fast enough to storage locations and have enough capacity in place.  
(This is mostly a requirment on networks team)

## Additional databases support 
- PostgreSQL 
- CouchBase ?

(changes are always a possibilty so we can't lock down the solution...)


## MySQL Features
MySQL X Protocol - One of the considerd features requested from R&D is X Protocol support.
This is an http/rest Protocol - It will require http traffic routing and proxy.  
(This should be fitted into artifact http traffic plain)

## Other 
CDC Support - Another highly requested feature is Change-Data-Capture.  
This feature allows application to register to changes in the DB layers.  
It will raise requirments regarding the traffic locality  
 (to propogate changes from shards between DCs)

