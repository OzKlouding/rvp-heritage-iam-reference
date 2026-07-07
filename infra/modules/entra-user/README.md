Entra ID User Module

Automates user creation in Microsoft Entra ID (Azure AD).

Usage

hcl# Password is sourced from a variable, never hardcoded.
# In production, source from Azure Key Vault or a secrets manager.
variable "initial_password" {
  type      = string
  sensitive = true
}

module "test_user" {
  source              = "../../modules/entra-user"
  user_principal_name = "john.doe@yourdomain.onmicrosoft.com"
  display_name        = "John Doe"
  password            = var.initial_password
  job_title           = "Cloud Engineer"
  department          = "IT"
}

Inputs

NameTypeRequiredDescriptionuser_principal_namestringyesUser's UPNdisplay_namestringyesDisplay namepasswordstring (sensitive)yesInitial password; source from a secrets managerforce_password_changeboolnoForce password change on first login (default: true)account_enabledboolnoWhether the account is enabled (default: true)job_titlestringnoJob titledepartmentstringnoDepartment

Outputs

NameDescriptionobject_idAzure AD object IDuser_principal_nameUser UPNdisplay_nameDisplay name

Design decisions & tradeoffs


Password marked sensitive and defaulted to force-change on first login. The module never logs the credential and requires rotation at first use. In production the initial password should come from Azure Key Vault, not a variable file.
User creation is intentionally atomic (one user per module call). This keeps the lifecycle auditable and lets group membership and role assignment be composed separately, rather than bundling everything into one opaque resource. Tradeoff: bulk provisioning uses iteration (for_each) at the root, which is the correct place for it.
Optional attributes default to null rather than empty strings, so Terraform does not report spurious drift on fields the business has not set.
Scope boundary: this module provisions the identity only. Entitlements are granted through the entra-group module, enforcing least privilege by separating "who exists" from "what they can access."