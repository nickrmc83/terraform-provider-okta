---
layout: 'okta'
page_title: 'Okta: okta_network_zone'
sidebar_current: 'docs-okta-resource-network-zone'
description: |-
  Creates an Okta Network Zone.
---

# okta_network_zone

Creates an Okta Network Zone.

This resource allows you to create and configure an Okta Network Zone.

## Example Usage

```hcl
resource "okta_network_zone" "example" {
  name     = "example"
  type     = "IP"
  gateways = ["1.2.3.4/24", "2.3.4.5-2.3.4.15"]
  proxies  = ["2.2.3.4/24", "3.3.4.5-3.3.4.15"]
}
```

## Example Usage - Dynamic Tor Blocker

```hcl
resource "okta_network_zone" "example" {
  name               = "TOR Blocker"
  type               = "DYNAMIC"
  usage              = "BLOCKLIST"
  dynamic_proxy_type = "TorAnonymizer"
}
```

## Argument Reference

The following arguments are supported:

- `name` - (Required) Name of the Network Zone Resource.

- `type` - (Required) Type of the Network Zone - can either be `"IP"` or `"DYNAMIC"` only.

- `dynamic_locations` - (Optional) Array of locations [ISO-3166-1](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
  and [ISO-3166-2](https://en.wikipedia.org/wiki/ISO_3166-2). Format code: countryCode OR countryCode-regionCode.

- `dynamic_proxy_type` - (Optional) Type of proxy being controlled by this dynamic network zone - can be one of `Any`, `TorAnonymizer` or `NotTorAnonymizer`.

- `gateways` - (Optional) Array of values in CIDR/range form.

- `proxies` - (Optional) Array of values in CIDR/range form. Can not be set if `usage` is set to `"BLOCKLIST"`.

- `usage` - (Optional) Usage of the Network Zone - can be either `"POLICY"` or `"BLOCKLIST"`. By default, it is `"POLICY"`.

- `asns` - (Optional) Array of Autonomous System Numbers (each element is a string representation of an ASN numeric value).

## Attributes Reference

- `id` - Network Zone ID.

## Import

Okta Network Zone can be imported via the Okta ID.

```
$ terraform import okta_network_zone.example &#60;zone id&#62;
```
