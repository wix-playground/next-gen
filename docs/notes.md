# notes

## from @WIgor

1. Drop Chef - move to immutable servers. Question what to do with ZK, Consul, Vault, Elasticsearch, DBs, etc.
1. ZK, Consul, Etcd - simplify topology DB, ZK too slow for this (question why not MySQL or any other DB with replication), Consul and Etcd intersects by features. Leave Kube with Etcd - everything else move to some appropriate DB, with replicas in all DCs.
1. ~~Magic behind 2 DC for editor (DB staff - replication conflicts, etc) - it smells. Reconsider DB and application logic.~~ This was removed long ago - and not relevant to this anyway... (we have regular replication - and single writeable master...)
1. Kube is ok
1. Current infrastructure is too open. Huge attack surface. Platformization: all API calls must be signed, any app key may be revoked, any developer must have own key, some API should not be called by humans.
1. Different deployment strategies: A/B testing (superset of current test bed), blue-green clusters.
1. Why we have transparent network? Why not to split it to separate isolated domains with API gateways?

## generic

1. Pipeline Standart
1. less stack
1. API with authentication
1. Provisioning with NASA
1. Less proxy/caches
1. Less number of CDN
1. Control plane?
1. Cross Dc connectivity
1. Kube on prem
1. Traffic flow review
1. http2, quick
1. Ddos protectionP
