---
page_title: "doppler_secrets_sync_flyio Resource - terraform-provider-doppler"
subcategory: ""
description: |-
	Manage a Fly.io Doppler sync.
---

# doppler_secrets_sync_flyio (Resource)

Manage a Fly.io Doppler sync.

## Example Usage

```terraform
resource "doppler_integration_flyio" "prod" {
  name    = "TF Fly.io"
  api_key = "fo1_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}

resource "doppler_secrets_sync_flyio" "backend_prod" {
  integration = doppler_integration_flyio.prod.id
  project     = "backend"
  config      = "prd"

  app_id           = "my-app"
  restart_machines = true

  delete_behavior = "leave_in_target"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `app_id` (String) The app ID
- `config` (String) The name of the Doppler config
- `integration` (String) The slug of the integration to use for this sync
- `project` (String) The name of the Doppler project
- `restart_machines` (Boolean) Whether or not to restart the Fly.io machines when secrets are updated

### Optional

- `delete_behavior` (String) The behavior to be performed on the secrets in the sync target when this resource is deleted or recreated. Either `leave_in_target` (default) or `delete_from_target`.

### Read-Only

- `id` (String) The ID of this resource.