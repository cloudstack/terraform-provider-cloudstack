---
layout: "cloudstack"
page_title: "CloudStack: cloudstack_nic"
sidebar_current: "docs-cloudstack-resource-nic"
description: |-
  Creates an additional NIC to add a VM to the specified network.
---

# cloudstack_nic

Creates an additional NIC to add a VM to the specified network.

## Example Usage

Basic usage:

```hcl
resource "cloudstack_nic" "test" {
  network_id         = "6eb22f91-7454-4107-89f4-36afcdf33021"
  ip_address         = "192.168.1.1"
  virtual_machine_id = "f8141e2f-4e7e-4c63-9362-986c908b7ea7"
}
```

With MAC address:

```hcl
resource "cloudstack_nic" "test" {
  network_id         = "6eb22f91-7454-4107-89f4-36afcdf33021"
  ip_address         = "192.168.1.1"
  mac_address        = "02:1a:4b:3c:5d:6e"
  virtual_machine_id = "f8141e2f-4e7e-4c63-9362-986c908b7ea7"
}
```

## Argument Reference

The following arguments are supported:

* `network_id` - (Required) The ID of the network to plug the NIC into. Changing
    this forces a new resource to be created.

* `ip_address` - (Optional) The IP address to assign to the NIC. Changing this
    forces a new resource to be created.

* `mac_address` - (Optional) The MAC address to assign to the NIC. If not specified,
    a MAC address will be automatically generated. Changing this forces a new resource
    to be created.

* `virtual_machine_id` - (Required) The ID of the virtual machine to which to
    attach the NIC. Changing this forces a new resource to be created.

* `project` - (Optional) The name or ID of the project the virtual machine
    belongs to. Required when the virtual machine belongs to a project,
    otherwise the NIC cannot be read back. Changing this forces a new resource
    to be created.

## Attributes Reference

The following attributes are exported:

* `id` - The ID of the NIC.
* `ip_address` - The assigned IP address.
* `mac_address` - The assigned MAC address.

## Import

NICs can be imported using `<virtual_machine_id>/<nic_id>`, e.g.

```shell
$ terraform import cloudstack_nic.test f8141e2f-4e7e-4c63-9362-986c908b7ea7/2b1a4b3c-5d6e-4f70-8192-a3b4c5d6e7f8
```

When the virtual machine belongs to a project, prefix the project:

```shell
$ terraform import cloudstack_nic.test my-project/f8141e2f-4e7e-4c63-9362-986c908b7ea7/2b1a4b3c-5d6e-4f70-8192-a3b4c5d6e7f8
```
