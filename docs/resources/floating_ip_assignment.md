---
page_title: "DigitalOcean: digitalocean_floating_ip_assignment"
subcategory: "Networking"
---

# digitalocean\_floating_ip_assignment

~> **Deprecated:** DigitalOcean Floating IPs have been renamed reserved IPs. This resource will be removed in a future release. Please use `digitalocean_reserved_ip_assignment` instead.

Provides a resource for assigning an existing DigitalOcean Floating IP to a Droplet. This
makes it easy to provision floating IP addresses that are not tied to the lifecycle of your
Droplet.

## Example Usage

```hcl
resource "digitalocean_floating_ip" "foobar" {
  region = "sgp1"
}

resource "digitalocean_droplet" "foobar" {
  name               = "baz"
  size               = "s-1vcpu-1gb"
  image              = "ubuntu-18-04-x64"
  region             = "sgp1"
  ipv6               = true
  private_networking = true
}

resource "digitalocean_floating_ip_assignment" "foobar" {
  ip_address = digitalocean_floating_ip.foobar.ip_address
  droplet_id = digitalocean_droplet.foobar.id
}
```

## Argument Reference

The following arguments are supported:

* `ip_address` - (Required) The Floating IP to assign to the Droplet.
* `droplet_id` - (Optional) The ID of Droplet that the Floating IP will be assigned to.

## Import

Floating IP assignments can be imported using the Floating IP itself and the `id` of
the Droplet joined with a comma. For example:

```
terraform import digitalocean_floating_ip_assignment.foobar 192.0.2.1,123456
```
