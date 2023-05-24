---
subcategory: "Fleet"
layout: ""
page_title: "Elasticstack: elasticstack_fleet_agent_policy Resource"
description: |-
  Creates or updates a Fleet Agent Policy.
---

# Resource: elasticstack_fleet_agent_policy

Creates or updates a Fleet Agent Policy. See https://www.elastic.co/guide/en/fleet/current/fleet-api-docs.html#create-agent-policy-api

## Example Usage

```terraform
provider "elasticstack" {
  kibana {}
}

resource "elasticstack_fleet_agent_policy" "test_policy" {
  name            = "Test Policy"
  namespace       = "default"
  description     = "Test Agent Policy"
  sys_monitoring  = true
  monitor_logs    = true
  monitor_metrics = true
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String) The name of the agent policy.
- `namespace` (String) The namespace of the agent policy.

### Optional

- `data_output_id` (String) The identifier for the data output.
- `description` (String) The description of the agent policy.
- `download_source_id` (String) The identifier for the Elastic Agent binary download server.
- `fleet_server_host_id` (String) The identifier for the Fleet server host.
- `monitor_logs` (Boolean) Enable collection of agent logs.
- `monitor_metrics` (Boolean) Enable collection of agent metrics.
- `monitoring_output_id` (String) The identifier for monitoring output.
- `policy_id` (String) Unique identifier of the agent policy.
- `sys_monitoring` (Boolean) Enable collection of system logs and metrics.

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
terraform import elasticstack_kibana_fleet_agent_policy.my_policy <space id>/<policy id>
```