---
page_title: "doppler_group_members Resource - terraform-provider-doppler"
subcategory: ""
description: |-
	Manage a Doppler group's memberships.
---

# doppler_group_members (Resource)

Manage a Doppler group's memberships.

**Note:** The `doppler_group_members` resource will clear/replace all existing memberships.
Multiple `doppler_group_members` resources or combinations of `doppler_group_members` and `doppler_group_member` will produce inconsistent behavior.
To non-exclusively manage group memberships, use `doppler_group_member` only.

## Example Usage

```terraform
resource "doppler_group" "engineering" {
  name = "engineering"
}

data "doppler_user" "nic" {
  email = "nic@doppler.com"
}

data "doppler_user" "andre" {
  email = "andre@doppler.com"
}

resource "doppler_group_members" "engineering" {
  group_slug = doppler_group.engineering.slug
  user_slugs = [
    data.doppler_user.nic.slug,
    data.doppler_user.andre.slug
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `group_slug` (String) The slug of the group
- `user_slugs` (Set of String) A list of user slugs in the group

### Read-Only

- `id` (String) The ID of this resource.

## Import

Import is supported using the following syntax:

```shell
# import using the group slug from the URL:
# https://dashboard.doppler.com/workplace/[workplace-slug]/team/groups/[group-slug]
# and the user slugs from the URL:
# https://dashboard.doppler.com/workplace/[workplace-slug]/team/users/[user-slug]
terraform import doppler_group_members.default <group-slug>
```