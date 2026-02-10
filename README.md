# minio-ha-design-and-implementation

Design : 
SNSD – single‑node, single drive (dev/test only)

SNMD – single‑node, multi‑drive (still limited)

MNMD – multi‑node multi‑drive — the recommended production mode with erasure coding and HA

In MNMD mode:

Each server has multiple disks (e.g., 4 or more)

Nodes pool storage for erasure coding

The cluster continues serving data if nodes or disks fail

Distributed mode scales horizontally for performance and capacity

Best practice: At least 4 nodes with multiple disks per node behind a load balancer for server‑level HA and redundancy.

MinIO uses erasure coding to distribute data and parity across all drives in the cluster:

Protects against disk/node failures

Allows automatic data healing

Requires a minimum number of drives across the cluster

Reads and writes continue as long as quorum is maintained

Erasure coding is a core requirement in production to ensure:

High durability

Reliability during hardware issues

Reduced risk compared to simple replication

DC1:

Load Balancer A → 4 Nodes (MinIO MNMD cluster)


DC2:

Load Balancer B → 4 Nodes (MinIO MNMD cluster)


Replication:

Active‑Active replication enabled between DC1 ↔ DC2 buckets
Versioning enabled on all replicated buckets
Same IAM & policy configs synced

Deploy MinIO on RedHat Linux: 
https://minio-docs.tf.fo/operations/deployments/baremetal-deploy-minio-on-redhat-linux#deploy-minio-rhel
