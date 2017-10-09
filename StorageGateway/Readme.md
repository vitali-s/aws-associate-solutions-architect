# Storage Gateway
AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration. 

Gateways:
* File Gateway - includes software appliance deployed to on-premise environment as Virtual Machine. Provides NFS interfaces to S3 and allows to manage files directly using NFS 3.1/4.0 protocol.
* Volume Gateway - provide cloud storage volumes via ISCSI protocol.
  * Cached Volumes - keeps data in S3, but also keeps frequently accessed data locally. 
  * Stored Volumes - keeps data in S3, could be configured to stora data locally and asynchronously back up point-in-time snapshots.
* Tape Gateway - archive backup data in Amazon Glacier