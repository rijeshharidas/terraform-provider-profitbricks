---
layout: "profitbricks"
page_title: "ProfitBricks: profitbricks_k8s_node_pool"
sidebar_current: "docs-profitbricks-resource-k8s-node-pool"
description: |-
  Creates and manages Profitbricks Kubernetes Node Pools.
---

# profitbricks_k8s_node_pool

Manages a Kubernetes Node Pool, part of a managed Kubernetes cluster on ProfitBricks.

## Example Usage

```hcl
resource "profitbricks_k8s_node_pool" "demo" {
  name        = demo
  k8s_version = "1.18.3"
  auto_scaling {
    min_node_count = 1
    max_node_count = 3
  }
  maintenance_window {
    day_of_the_week = "Sunday"
    time            = "10:30:00Z"
  }
  datacenter_id     = "{profitbricks_datacenter_id}"
  k8s_cluster_id    = "{profitbricks_k8s_cluster_id}"
  cpu_family        = "INTEL_XEON"
  availability_zone = "AUTO"
  storage_type      = "SSD"
  node_count        = 1
  cores_count       = 2
  ram_size          = 2048
  storage_size      = 40
}

```

## Argument Reference

The following arguments are supported:

- `name` - (Required)[string] The name of the Kubernetes Cluster.
- `k8s_version` - (Optional)[string] The desired Kubernetes Version. for supported values, please check the API documentation.
- `auto_scaling` - (Optional)[string] Wether the Node Pool should autoscale. For more details, please check the API documentation
- `maintenance_window` - (Optional) See the **maintenance_window** section in the example above
- `datacenter_id` - (Required)[string] A Datacenter's UUID
- `k8s_cluster_id`- (Required)[string] A k8s cluster's UUID
- `cpu_family` - (Required)[string] The desired CPU Family - See the API documentation for more information
- `availability_zone` - (Required)[string] - The desired Compute availability zone - See the API documentation for more information
- `storage_type` -(Required)[string] - The desired storage type - SSD/HDD
- `node_count` -(Required)[int] - The desired number of nodes in the node pool
- `cores_count` -(Required)[int] - The CPU cores count for each node of the node pool
- `ram_size` -(Required)[int] - The desired amount of RAM, in MB
- `storage_size` -(Required)[int] - The desired amount of storage for each node, in GB

## Import

A Kubernetes Node Pool resource can be imported using its Kubernetes cluster's uuid as well as its own UUID, both of which you can retreive from the cloud API: `resource id`, e.g.:

```shell
terraform import profitbricks_k8s_node_pool.demo {k8s_cluster_uuid}/{k8s_nodepool_id}
```

This can be helpful when you want to import kubernetes node pools which you have already created manually or using other means, outside of terraform, towards the goal of managing them via Terraform
