---
layout: "ibmcloud"
page_title: "IBM Cloud: cs_cluster"
sidebar_current: "docs-ibmcloud-resource-cs-cluster"
description: |-
  Manages IBM Cloud infrastructure cluster.
---

# ibmcloud\_cs_cluster

Create, update, or delete a Kubernetes cluster. An existing subnet can be attached to the cluster by passing the subnet ID. A webhook can be registered to a cluster and you can add multiple worker nodes with the `workers` option.

## Example Usage

In the following example, you can create a Kubernetes cluster:

```hcl
resource "ibmcloud_cs_cluster" "testacc_cluster" {
    name = "test"
    datacenter = "dal10"
    machine_type = "free"
    isolation = "public"
    public_vlan_id = "vlan"
    private_vlan_id = "vlan"
    subnet_id = ["1154643"]
    workers = [{name="worker1",  action="add"},]
    webhook = [{level="Normal",  type="slack", url="https://hooks.slack.com/services/yt7rebjhgh2r4rd44fjk"},]
    org_guid = "test"
    space_guid = "test_space"
    account_guid = "test_acc"
}
```

## Argument Reference

The following arguments are supported:


* `name` - (Required) Name of the cluster.
* `datacenter` - (Required)  The data center of the worker nodes.
* `org_guid` - (Required) The GUID for the Bluemix organization that the cluster is associated with.
* `space_guid` - (Required) The GUID for the Bluemix space that the cluster is associated with.
* `account_guid` - (Required) The GUID for the Bluemix account that the cluster is associated with.
* `workers` - (Required) The worker nodes that needs to be added to the cluster.
* `machinetype` - (Optional) The machine type of the worker nodes.
* `billing` -  (Optional) The billing type for the instance. Accepted values are `hourly` or `monthly`.
* `isolation` - (Optional) Accepted values are `public` or `private`.
* `public_vlan_id`- (Optional) The public VLAN of the worker node.
* `private_vlan_id` - (Optional) The private VLAN of the worker node.
* `subnet_id` - (Optional) The existing subnet ID that you want to add to the cluster.
* `no_subnet` - (Optional) The option if you do not want to automatically create a portable subnet.
* `webhook` - (Optional) The webhook that you want to add to the cluster.
* `wait_time_minutes` - (Optional) The duration, expressed in minutes, to wait for the cluster to become available before declaring it as created. It is also the same amount of time waited for no active transactions before proceeding with an update or deletion. Default value: `90`.



    
## Attributes Reference

The following attributes are exported:

* `id` - ID of the cluster.
* `name` - Name of the cluster.
* `server_url` - The server URL.
* `ingress_hostname` - The ingress hostname.
* `ingress_secret` - The ingress secret.
* `worker_num` - The number of worker nodes for this cluster.
* `workers` - The worker nodes attached to this cluster.
* `subnet_id` - The subnets attached to this cluster.
