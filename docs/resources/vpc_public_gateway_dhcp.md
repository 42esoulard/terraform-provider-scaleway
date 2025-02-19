---
page_title: "Scaleway: scaleway_vpc_public_gateway_dhcp"
description: |-
  Manages Scaleway VPC Public Gateways IP.
---

# scaleway_vpc_public_gateway_dhcp

Creates and manages Scaleway VPC Public Gateway DHCP.
For more information, see [the documentation](https://developers.scaleway.com/en/products/vpc-gw/api/v1/#dhcp-c05544).

## Example

```hcl
resource "scaleway_vpc_public_gateway_dhcp" "main" {
    subnet = "192.168.1.0/24"
}
```

## Arguments Reference

The following arguments are supported:

- `zone` - (Defaults to [provider](../index.md#zone) `zone`) The [zone](../guides/regions_and_zones.md#zones) in which the public gateway DHCP config should be created.
- `project_id` - (Defaults to [provider](../index.md#project_id) `project_id`) The ID of the project the public gateway DHCP config is associated with.
- `subnet` - (Required) The subnet to associate with the public gateway DHCP config.
- `address` - (Optional) The IP address of the public gateway DHCP config.
- `pool_low` - (Optional) Low IP (included) of the dynamic address pool. Defaults to the second address of the subnet.
- `pool_high` - (Optional) High IP (excluded) of the dynamic address pool. Defaults to the last address of the subnet.
- `enable_dynamic` - (Optional) Whether to enable dynamic pooling of IPs. By turning the dynamic pool off, only pre-existing DHCP reservations will be handed out. Defaults to `true`.
- `valid_lifetime` - (Optional) For how long, in seconds, will DHCP entries will be valid. Defaults to 1h (3600s).
- `renew_timer` - (Optional) After how long, in seconds, a renewal will be attempted. Must be 30s lower than `rebind_timer`. Defaults to 50m (3000s).
- `rebind_timer` - (Optional) After how long, in seconds, a DHCP client will query for a new lease if previous renews fail. Must be 30s lower than `valid_lifetime`. Defaults to 51m (3060s).
- `push_default_route` - (Optional) Whether the gateway should push a default route to DHCP clients or only hand out IPs. Defaults to `true`.
- `push_dns_server` - (Optional) Whether the gateway should push custom DNS servers to clients. This allows for instance hostname -> IP resolution. Defaults to `true`.
- `dns_servers_override` - (Optional) Override the DNS server list pushed to DHCP clients, instead of the gateway itself
- `dns_search` - (Optional) Additional DNS search paths
- `dns_local_name` - (Optional) TLD given to hostnames in the Private Network. Allowed characters are `a-z0-9-.`. Defaults to the slugified Private Network name if created along a GatewayNetwork, or else to `priv`.

## Attributes Reference

In addition to all above arguments, the following attributes are exported:

- `id` - The ID of the public gateway DHCP config.
- `organization_id` - The organization ID the public gateway DHCP config is associated with.
- `created_at` - The date and time of the creation of the public gateway DHCP config.
- `updated_at` - The date and time of the last update of the public gateway DHCP config.

## Import

Public gateway DHCP config can be imported using the `{zone}/{id}`, e.g.

```bash
$ terraform import scaleway_vpc_public_gateway_dhcp.main fr-par-1/11111111-1111-1111-1111-111111111111
```
