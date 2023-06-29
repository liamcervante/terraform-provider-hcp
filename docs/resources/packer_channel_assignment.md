---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "hcp_packer_channel_assignment Resource - terraform-provider-hcp"
subcategory: ""
description: |-
  The Packer Channel Assignment resource allows you to manage the iteration assigned to a bucket channel in an active HCP Packer Registry.
---

# hcp_packer_channel_assignment (Resource)

The Packer Channel Assignment resource allows you to manage the iteration assigned to a bucket channel in an active HCP Packer Registry.

## Example Usage

```terraform
resource "hcp_packer_channel_assignment" "staging" {
  bucket_name  = "alpine"
  channel_name = "staging"

  # Exactly one of version, id, or fingerprint must be set:
  iteration_version = 12
  # iteration_id = "01H1SF9NWAK8AP25PAWDBGZ1YD"
  # iteration_fingerprint = "01H1ZMW0Q2W6FT4FK27FQJCFG7"
}

# To set the channel to have no assignment, use one of the iteration attributes with their zero value.
# The two string-typed iteration attributes, id and fingerprint, use "none" as their zero value.
resource "hcp_packer_channel_assignment" "staging" {
  bucket_name  = "alpine"
  channel_name = "staging"

  iteration_version = 0
  # iteration_id = "none"
  # iteration_fingerprint = "none"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `bucket_name` (String) The slug of the HCP Packer Registry bucket where the channel is located.
- `channel_name` (String) The name of the HCP Packer channel being managed.

### Optional

- `iteration_fingerprint` (String) The fingerprint of the iteration assigned to the channel.
- `iteration_id` (String) The ID of the iteration assigned to the channel.
- `iteration_version` (Number) The incremental version of the iteration assigned to the channel.
- `project_id` (String) The ID of the HCP project where the channel is located. 
If not specified, the project specified in the HCP Provider config block will be used, if configured.
If a project is not configured in the HCP Provider config block, the oldest project in the organization will be used.
- `timeouts` (Block, Optional) (see [below for nested schema](#nestedblock--timeouts))

### Read-Only

- `id` (String) The ID of this resource.
- `organization_id` (String) The ID of the HCP organization where this channel is located. Always the same as the associated channel.

<a id="nestedblock--timeouts"></a>
### Nested Schema for `timeouts`

Optional:

- `create` (String)
- `default` (String)
- `delete` (String)
- `update` (String)

## Import

Import is supported using the following syntax:

```shell
# Using an explicit project ID, the import ID is:
# {project_id}:{bucket_name}:{channel_name}
terraform import hcp_packer_channel_assignment.staging f709ec73-55d4-46d8-897d-816ebba28778:alpine:staging
# Using the provider-default project ID, the import ID is:
# {bucket_name}:{channel_name}
terraform import hcp_packer_channel_assignment.staging alpine:staging
```