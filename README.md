# GLDR APIS
## Protection
#### Create Protection Group
POST /disaster-recovery/v1beta1/virtual-continuous-protection-groups

Body:
```
{
  "name":"PM_DEMO_LIOR10",
  "protectedSite": "{{ProtectedSiteIdentifier}}",
  "recoverySite": "{{RecoverySiteIdentifier}}",
  "hypervisor":{ 
    "host":"{{HostIdentifier}}",
    "cluster":"{{ClusterIdenitifier}}",
    "datastore":"{{DatastoreIdentifier}}",
    "datastoreCluster":"{{DatastoreClusterIdentifier}}",
    "folder":"{{FolderIdentifier}}",
    "network":"{{NetworkIdentifier}}",
    "testNetwork":"{{NetworkIdentifier}}"
    },
  "virtualMachines":[ 
      {         
         "id":"{{VmIdentifier}}"
      }
   ]
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/e977ed03-ece3-4ed0-839b-a993725d4c4c"
}
```
#### Get all protection groups data
GET /disaster-recovery/v1beta1/virtual-continuous-protection-groups

Response:
```
{
    "items": [
        {
            "id": "ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
            "status": "ready",
            "name": "vpg-4b99425",
            "protectedSite": {
                "id": "cfa2cc63-e43b-4f6e-82fb-b6737fce029b",
                "name": "accusamus"
            },
            "recoverySite": {
                "id": "cfa2cc63-e43b-4f6e-82fb-b6737fce029b",
                "name": "accusamus"
            },
            "hypervisor": {
                "host": "5ecdbc67-0bd9-321f-8cc6-03fb2c2da6b7",
                "datastore": "be556441-a07f-3ad0-998f-4288a2f09ec2",
                "cluster": "",
                "datastoreCluster": "",
                "folder": "a4a37624-f274-30a2-b1e0-16e76e758ad9",
                "network": "e3965e6a-9c8f-3c6e-81ae-543bfe8d0e8f",
                "testNetwork": "e3965e6a-9c8f-3c6e-81ae-543bfe8d0e8f"
            },
            "virtualMachines": [
                {
                    "id": "1216926d-410e-5fde-a3e6-1076aafde55e"
                }
            ],
            "type": "virtual-continuous-protection-group",
            "resourceUri": "/api/v1/virtual-continuous-protection-groups/95d4e310-39a1-11ed-8051-56e786f00957",
            "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
            "generation": 2,
            "updatedAt": "2023-03-13T08:11:21.489807Z",
            "createdAt": "2023-03-13T08:11:21.489807Z"
        }
    ],
    "limit": 20000,
    "offset": 0,
    "total": 1
}
```
#### Get data for specific protection group
GET /disaster-recovery/v1beta1/virtual-continuous-protection-groups/{id}

Response:
```
{
    "id": "ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
    "status": "ready",
    "name": "vpg-4b99425",
    "protectedSite": {
        "id": "cfa2cc63-e43b-4f6e-82fb-b6737fce029b",
        "name": "accusamus"
    },
    "recoverySite": {
        "id": "cfa2cc63-e43b-4f6e-82fb-b6737fce029b",
        "name": "accusamus"
    },
    "hypervisor": {
        "host": "5ecdbc67-0bd9-321f-8cc6-03fb2c2da6b7",
        "datastore": "be556441-a07f-3ad0-998f-4288a2f09ec2",
        "cluster": "",
        "datastoreCluster": "",
        "folder": "a4a37624-f274-30a2-b1e0-16e76e758ad9",
        "network": "e3965e6a-9c8f-3c6e-81ae-543bfe8d0e8f",
        "testNetwork": "e3965e6a-9c8f-3c6e-81ae-543bfe8d0e8f"
    },
    "virtualMachines": [
        {
            "id": "1216926d-410e-5fde-a3e6-1076aafde55e"
        }
    ],
    "type": "virtual-continuous-protection-group",
    "resourceUri": "/api/v1/virtual-continuous-protection-groups/95d4e310-39a1-11ed-8051-56e786f00957",
    "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
    "generation": 2,
    "updatedAt": "2023-03-13T08:11:21.489807Z",
    "createdAt": "2023-03-13T08:11:21.489807Z"
}
```
#### Refresh protection group data from ZVM
POST /disaster-recovery/v1beta1/virtual-continuous-protection-groups/refresh/

Response:
```
{
    "taskUri": "/api/v1/tasks/e977ed03-ece3-4ed0-839b-a993725d4c4c"
}
```
#### Update VPG
PUT /disaster-recovery/v1beta1/virtual-continuous-protection-groups/{vpgId}

Body:
```
{
  "name" : "new vpg name"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/87831e92-b402-4e92-b60f-4be8e995ceac"
}
```

#### Delete a protection group 
DELETE /disaster-recovery/v1beta1/virtual-continuous-protection-groups/{{DSCC_VPG_UDID}}

Response:
```
{
    "taskUri": "/api/v1/tasks/e977ed03-ece3-4ed0-839b-a993725d4c4c"
}
```
## VIRTUALIZATION 
#### Get list of Virtual-machines for a specific Protection site ID 
GET /api/temp/zerto-virtual-machines?siteId={siteId}

Response:
```
[
    {
        "lastUpdatedAt": "2023-05-03T11:52:08Z",
        "id": "0267ee9c-b0a6-5fbd-b910-d307a77ebdd0",
        "name": "TinyLinux-bmeC",
        "type": "virtual-machine",
        "customerId": "cba90f60-8f34-11ec-8c8c-86feca181f9c",
        "internalId": "5addc1dd-f975-45c4-a8f9-d88e3c5f416c.vm-79",
        "siteId": "9276b77e-6197-4f41-8201-3b48d146bf8b",
        "protected": false
    }
]
```
#### Protection site ID as param Refresh virtual machines list 
POST /api/temp/zerto-virtual-machines/refresh

Body:
```
{
    "siteId":"{{ProtectedSiteIdentifier}}"
}
```
Response: 
```
{
    "taskUri": "/api/v1/tasks/01955825-26e1-4130-aae3-2677d465e577"
}
```
#### Get a list of Hypervisor-host
GET /api/temp/zerto-hypervisor-hosts?siteId={siteId}

Response:
```
[
 {
        "id": "de79e9ea-21d5-3f4e-a5f8-379714309bd8",
        "name": "10.171.16.67",
        "type": "hypervisor-host",
        "lastUpdatedAt": "2022-06-14T15:43:48Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.host-10",
        "cluster":{
          "type":"hypervisor-cluster",
          "resourceUri":"<URI>",
          "name":"<string>"
        }
    }
]
```
#### Recovery site ID as param recovery site Refresh Hypervisor-host list 
POST /api/temp/zerto-hypervisor-hosts/refresh

Body:
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/e977ed03-ece3-4ed0-839b-a993725d4c4c"
}
```
#### Get a list of Hypervisor-clusters
GET /api/temp/zerto-hypervisor-clusters?siteId={siteId}

Response:
```
[
    {
        "id": "d8d6b7c3-d726-3ccc-8b8c-117beeb3b7c8",
        "name": "Cluster",
        "type": "hypervisor-cluster",
        "lastUpdatedAt": "2022-06-14T13:12:12Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.domain-c19"
    }
]
```
#### Recovery site ID as param recovery site Refresh Hypervisor-cluster list
 POST /api/temp/zerto-hypervisor-clusters/refresh
 
Body:
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response: 
```
{
    "taskUri": "/api/v1/tasks/e5d2d1f7-f3c6-44cf-92f1-a2854b40dba7"
}
```
#### Get a list of hypervisor-datastores
GET /api/temp/zerto-hypervisor-datastores?siteId={siteId}

```
[
    {
        "id": "f13b8f10-1d32-3624-afbf-731d2d0365f3",
        "name": "inf_QANested0095_DS5",
        "type": "hypervisor-datastore",
        "lastUpdatedAt": "2022-06-14T13:12:18Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.datastore-458"
    }
]
```
#### Recovery site ID as param recovery site Refresh hypervisor-datastores list 
POST /api/temp/zerto-hypervisor-datastores/refresh

Body:
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/3a02bf03-ebf7-42c7-81d6-656d28863730"
}
```
#### Get a list of hypervisor-networks
GET /api/temp/zerto-hypervisor-networks?siteId={siteId}

Response:
```
[
    {
        "id": "4f2f4c80-4c49-3b30-95b0-51405023130f",
        "name": "VM Network",
        "type": "hypervisor-network",
        "lastUpdatedAt": "2022-06-14T13:12:25Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.network-11"
    }
]
```
#### Recovery site ID as param recovery siteRefresh hypervisor-networks list 
POST /api/temp/zerto-hypervisor-networks/refresh

Body: 
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/a360908d-c407-45fb-9dee-6818b0d98c88"
}
```
#### Get a list of hypervisor-folders
GET /api/temp/zerto-hypervisor-folders?siteId={siteId}

Response:
```
[
    {
        "id": "b09fef96-058a-32e0-88bb-5167590f5f1b",
        "name": "/",
        "type": "hypervisor-folder",
        "lastUpdatedAt": "2022-06-14T13:12:30Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.group-v3"
    }
]
```
#### Recovery site ID as param recovery siteRefresh hypervisor-folders list 
POST /api/temp/zerto-hypervisor-folders/refresh

Bosy:
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/31f8dd6c-a924-4098-b4cb-a5d668bd51c1"
}
```
#### Get a list of hypervisor-datastore-clusters
GET /api/temp/zerto-hypervisor-datastore-clusters?siteId={siteId}

Response:
```
[
    {
        "id": "ecaa9b14-8943-357a-b264-70191d4287b4",
        "name": "DS4",
        "type": "hypervisor-datastore-cluster",
        "lastUpdatedAt": "2022-06-14T13:12:36Z",
        "customerId": "ac535f94eaec11ecbabefab33ff4092c",
        "siteId": "b0b2468d-914d-477c-86a2-2b8886464ff7",
        "internalId": "02ed58e0-ad7b-4f35-ad5a-9d5fe4ab5017.group-p494"
    }
]
```
#### Recovery site ID as param recovery siteRefresh hypervisor-datastore-clusters list 
POST /api/temp/zerto-hypervisor-datastore-clusters/refresh

Body:
```
{
    "siteId":"{{RecoverySiteIdentifier}}"
}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
## RECOVERY

#### Get all recovery groups data
GET /disaster-recovery/v1beta1/virtual-continuous-protection-recovery/

Response:
```
{
    "items": [
        {
            "id": "ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
            "name": "vpg-4b99425",
            "type": "virtual-continuous-protection-recovery",
            "status": "READY",
            "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
            "actions": [
                {
                    "name": "test",
                    "enabled": true,
                    "reason": ""
                },
                {
                    "name": "stop",
                    "enabled": false,
                    "reason": ""
                },
                {
                    "name": "failover",
                    "enabled": true,
                    "reason": ""
                },
                {
                    "name": "move",
                    "enabled": false,
                    "reason": ""
                },
                {
                    "name": "rollback",
                    "enabled": false,
                    "reason": ""
                },
                {
                    "name": "commit",
                    "enabled": false,
                    "reason": ""
                }
            ],
            "resourceUri": "/api/v1/virtual-continuous-protection-recoveries/ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
            "createdAt": "2023-03-13T08:11:40.975818Z",
            "updatedAt": "2023-03-13T08:11:40.975818Z",
            "generation": 1
        }
    ],
    "limit": 20000,
    "offset": 0,
    "total": 1
}
```
#### Get data for specific recovery group
GET /disaster-recovery/v1beta1/virtual-continuous-protection-recovery/{{DSCC_VPG_UDID}}

Response:
```
   {
    "id": "ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
    "name": "vpg-4b99425",
    "type": "virtual-continuous-protection-recovery",
    "status": "READY",
    "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
    "actions": [
        {
            "name": "test",
            "enabled": true,
            "reason": ""
        },
        {
            "name": "stop",
            "enabled": false,
            "reason": ""
        },
        {
            "name": "failover",
            "enabled": true,
            "reason": ""
        },
        {
            "name": "move",
            "enabled": false,
            "reason": ""
        },
        {
            "name": "rollback",
            "enabled": false,
            "reason": ""
        },
        {
            "name": "commit",
            "enabled": false,
            "reason": ""
        }
    ],
    "resourceUri": "/api/v1/virtual-continuous-protection-recoveries/ea8b7d07-10f3-49cf-84a8-7d6f81f940b5",
    "createdAt": "2023-03-13T08:11:40.975818Z",
    "updatedAt": "2023-03-13T08:11:40.975818Z",
    "generation": 1
}  
```
#### Initiate Failover Live Operation 
POST /disaster-recovery/v1beta1/virtual-continuous-protection-recovery/{{DSCC_VPG_UDID}}/Failover

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
#### Initiate Failover Live-Commit  Operation 
POST /disaster-recovery/v1beta1/virtual-continuous-protection-recoveries/:DsccVpgId/FailoverCommit

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
#### Initiate Failover Live-Rollback Operation 
POST /disaster-recovery/v1beta1/virtual-continuous-protection-recoveries/:DsccVpgId/FailoverRollback

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
#### Initiate Failover Test Operation
 POST /disaster-recovery/v1beta1/virtual-continuous-protection-recoveries/{{VpgId}}/FailoverTest

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
#### Initiate Failover Test-Stop Operation 
POST /disaster-recovery/v1beta1/virtual-continuous-protection-recoveries/{{VpgId}}/FailoverTestStop

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
## REPLICATION
#### Get all replication groups data
GET /disaster-recovery/v1beta1/virtual-continuous-protection-replicas/

Response:
```
{
    "items": [
        {
            "id": "a1d7ed4d-8c0d-4876-80cd-dc17ed2569a8",
            "name": "vpg-71bf908",
            "slaStatus": "MEETING_SLA",
            "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
            "healthStatus": "OK",
            "rpo": {
                "configuredSeconds": 300,
                "actualSeconds": 5,
                "status": "OK"
            },
            "history": {
                "configuredMinutes": 1440,
                "actualMinutes": 10
            },
            "type": "virtual-continuous-protection-replica",
            "resourceUri": "/api/v1/virtual-continuous-protection-replicas/a1d7ed4d-8c0d-4876-80cd-dc17ed2569a8",
            "generation": 2,
            "updatedAt": "2023-03-13T07:55:00.69804Z",
            "createdAt": "2023-03-13T07:55:00.413094Z"
        }
    ],
    "limit": 20000,
    "offset": 0,
    "total": 1
}
```
#### Get data for specific replication group
GET /disaster-recovery/v1beta1/virtual-continuous-protection-replicas/{{DSCC_VPG_UDID}}

Response:
```
{
    "id": "a1d7ed4d-8c0d-4876-80cd-dc17ed2569a8",
    "name": "vpg-71bf908",
    "slaStatus": "MEETING_SLA",
    "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
    "healthStatus": "OK",
    "rpo": {
        "configuredSeconds": 300,
        "actualSeconds": 5,
        "status": "OK"
    },
    "history": {
        "configuredMinutes": 1440,
        "actualMinutes": 10
    },
    "type": "virtual-continuous-protection-replica",
    "resourceUri": "/api/v1/virtual-continuous-protection-replicas/a1d7ed4d-8c0d-4876-80cd-dc17ed2569a8",
    "generation": 2,
    "updatedAt": "2023-03-13T07:55:00.69804Z",
    "createdAt": "2023-03-13T07:55:00.413094Z"
}
```
#### Get checkpoints for specific replica VPG
GET /disaster-recovery/v1beta1/virtual-continuous-protection-replicas/:vpgid/checkpoints

Response:
```
{
    "items": [
        {
            "id" : "45d7324d-b880-41e8-8247-fc68efcdb752",
            "tag" : "checkpoint tag"
            "timestamp" : "2022-06-14T14:03:41.764853Z"
        }
    ],
    "limit": 20000,
    "offset": 0,
    "total": 1,
    "createdAt": "2022-06-14T14:07:46.666889Z",
    "updatedAt": "2022-06-14T14:07:46.666889Z",
    "refreshedAt": "2022-06-14T14:07:46.666889Z"
}
```
#### Refresh checkpoint data for specific vpg
POST /disaster-recovery/v1beta1/virtual-continuous-protection-replicas/:vpgid/checkpoints/refresh

Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
#### Refresh replication data from ZVM
POST /disaster-recovery/v1beta1/virtual-continuous-protection-replicas/refresh

Body:
```
{    "recoverySiteId": "8c15b12c-818f-498a-bcb3-573088bc285b"}
```
Response:
```
{
    "taskUri": "/api/v1/tasks/0ea06a97-41d6-4b68-8eec-fc753de4eae7"
}
```
## SITES
#### Gets list of sites connected to DSCC
GET /disaster-recovery/v1beta1/virtual-sites

Response:
```
{
    "items": [
        {
            "id": "9758fdb9-1be2-4b67-b2f0-f7f071124c85",
            "serialNumber": "b5243c5a-cc95-40fc-9323-88b951884e18",
            "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
            "name": "",
            "platformType": "",
            "networkAddress": "",
            "status": "ACTIVATING",
            "connected": false,
            "updatedAt": "2023-03-13T07:47:44.366986Z",
            "type": "virtual-site",
            "resourceUri": "/api/v1/virtual-sites/9758fdb9-1be2-4b67-b2f0-f7f071124c85",
            "generation": 1,
            "refreshedAt": "2023-03-13T07:47:45.547615Z",
            "createdAt": "2023-03-13T07:47:44.233091Z"
        }
    ],
    "limit": 20000,
    "offset": 0,
    "total": 1
}
```
#### Gets specific sites information 
GET {{url}}/disaster-recovery/v1beta1/virtual-sites/{id}

Response:   
```
{
    "id": "9758fdb9-1be2-4b67-b2f0-f7f071124c85",
    "serialNumber": "b5243c5a-cc95-40fc-9323-88b951884e18",
    "customerId": "95d4e310-39a1-11ed-8051-56e786f00957",
    "name": "",
    "platformType": "",
    "networkAddress": "",
    "status": "ACTIVATING",
    "connected": false,
    "updatedAt": "2023-03-13T07:47:44.366986Z",
    "type": "virtual-site",
    "resourceUri": "/api/v1/virtual-sites/9758fdb9-1be2-4b67-b2f0-f7f071124c85",
    "generation": 1,
    "refreshedAt": "2023-03-13T07:47:45.547615Z",
    "createdAt": "2023-03-13T07:47:44.233091Z"
}
```
#### Add Site to DSCC
POST /disaster-recovery/v1beta1/virtual-sites

Body:
```
{
    "serialNumber":"{{serialNumber}}"
}
```
Response:
```
{
    "id": "96acb465-b663-4aba-90c8-0b022ccc3e06"
}
```
#### Refresh site
POST /disaster-recovery/v1beta1/virtual-sites/{id}/refresh

Response:
```
{
    "taskId": "ddd39ad3-a331-400a-9e35-0948433e58ee"
}
```
#### Delete a site from DSCC
DELETE /disaster-recovery/v1beta1/virtual-sites/{id}

Response: 
204 No Content


## REPORTS
#### post 
POST /disaster-recovery/{{}}/virtual-continuous-protection-reports/

Body:
```
{
"siteId":"{{dsccSiteId}}",
"reportType":"recovery",
"startDate":"2022-11-05T11:04:05Z",
"endDate":"2023-09-20T15:04:05Z",
"recoveryOperation":["FailoverTest","Failover"],
"protectionGroup":["{{wrkVPGID}}"],
"state":""
}
```
#### Get
GET /disaster-recovery/{{}}/virtual-continuous-protection-reports

Response:
```

```
#### Get 
GET /disaster-recovery/{{}}//virtual-continuous-protection-reports/:repID

Response:
```

```
