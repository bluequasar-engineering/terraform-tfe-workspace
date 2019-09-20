# Terraform Cloud Workspace

This module provisions a Terraform Cloud / Terraform Enterprise workspace

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| auto\_apply | Whether to automatically apply changes when a Terraform plan is successful. | string | `"false"` | no |
| file\_triggers\_enabled | Whether to filter runs based on the changed files in a VCS push. If enabled, the working directory and trigger prefixes describe a set of paths which must contain changes for a VCS push to trigger a run. If disabled, any push will trigger a run. | string | `"true"` | no |
| name | Name of the workspace | string | n/a | yes |
| organization | Name of the organization. | string | n/a | yes |
| queue\_all\_runs | Whether all runs should be queued. When set to false, runs triggered by a VCS change will not be queued until at least one run is manually queued. | string | `"true"` | no |
| ssh\_key\_id | The ID of an SSH key to assign to the workspace. | string | `"null"` | no |
| terraform\_version | The version of Terraform to use for this workspace. | string | `"null"` | no |
| trigger\_prefixes | List of repository-root-relative paths which describe all locations to be tracked for changes. workspace. Defaults to the latest available version. | list | `"null"` | no |
| variables | Map of environment or Terraform variables to define in the workspace. To support complex values, these __MUST__ be `base64` encoded. | map(map(string)) | `{}` | no |
| vcs\_repo | The VCS repository to configure. | map(string) | `{}` | no |
| working\_directory | A relative path that Terraform will execute within. Defaults to the root of your repository. | string | `"null"` | no |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

The `variables` block is structured as follows:

```hcl
variables = {
  environment = {
    key1 = base64encode(var.value)
    key2 = base64encode("value2")
  }
  environment_sensitive = {
    ...
  }
  terraform = {
    ...
  }
  terraform_sensitive = {
    ...
  }
  terraform_hcl = {
    ...
  }
  terraform_hcl_sensitive = {
    ...
  }
}
```

The `vcs_repo` block supports:

* `identifier` - (Required) A reference to your VCS repository in the format `:org/:repo` where `:org` and `:repo` refer to the organization and repository in your VCS provider.
* `branch` - (Optional) The repository branch that Terraform will execute from. Default to `master`.
* `ingress_submodules` - (Optional) Whether submodules should be fetched when cloning the VCS repository. Defaults to `false`.
* `oauth_token_id` - (Required) Token ID of the VCS Connection (OAuth Conection Token) to use.