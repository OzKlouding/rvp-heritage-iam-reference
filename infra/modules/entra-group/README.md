Entra ID Group Module

Creates and manages Microsoft Entra ID (Azure AD) groups, including membership and ownership. Access is granted through group membership, keeping entitlements separate from identity.

Usage

hclmodule "clinical_staff" {
  source           = "../../modules/entra-group"
  display_name     = "Clinical Staff"
  description       = "All clinical staff requiring EHR access"
  security_enabled = true
  members          = [module.test_user.object_id]
}

Inputs

NameTypeRequiredDescriptiondisplay_namestringyesThe group's display namedescriptionstringnoGroup descriptionsecurity_enabledboolnoWhether the group is a security group (default: true)mail_enabledboolnoWhether the group is mail-enabled (default: false)mail_nicknamestringnoMail alias; auto-derived from display_name if omittedmemberslist(string)noMember object IDs (default: empty)ownerslist(string)noOwner object IDs; defaults to the deploying identity if omitted

Outputs

NameDescriptionobject_idThe group's Azure AD object IDdisplay_nameThe group's display name

Design decisions & tradeoffs


Groups are never left ownerless. If no owners are supplied, the module assigns the deploying identity as owner. Orphaned, unowned groups are a common governance gap and an audit finding; this default prevents them by construction.
Access is granted through group membership, not direct assignment. This module pairs with entra-user to enforce least privilege by separating "who exists" (the user module) from "what they can access" (this module). It keeps entitlement reviews tractable: certify the group, not thousands of individual grants.
mail_nickname is auto-derived from the display name when not provided, removing a manual step and preventing inconsistent naming, with an explicit override available when the business requires a specific alias.
Security-enabled by default, mail-disabled by default. The common case for access control is a security group; mail groups are the exception and must be opted into deliberately.