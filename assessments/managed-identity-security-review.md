# Managed Identity Security Assessment

## 1. Assessment Overview

This assessment reviews an existing Azure User-Assigned Managed Identity in the BonganiSecurity resource group.

The assessment uses live Azure configuration retrieved through Azure Cloud Shell.

## 2. Identity Inventory

| Attribute | Observed configuration |
|---|---|
| Identity name | mi-bongani-day1 |
| Identity type | User-Assigned Managed Identity |
| Resource group | BonganiSecurity |
| Azure location | Retrieved from Azure |
| Tags | None configured |
| Principal ID | Retrieved and verified |
| Client ID | Retrieved and verified |

## 3. RBAC Assessment

The managed identity has the following role assignment:

| Role | Scope |
|---|---|
| Reader | Subscription |

Reader provides read-only access within its assigned scope.

### Security observation

The identity has subscription-wide visibility.

Although Reader does not grant write permissions, subscription-level access may expose resource configuration and operational information across a broader environment than the workload requires.

## 4. Least-Privilege Recommendation

Review the business and technical purpose of the managed identity.

If subscription-wide visibility is unnecessary, consider reducing its scope to the specific resource group or resources required by the workload.

Any permission change must be tested against the workload's requirements before implementation.

## 5. Resource Tagging Recommendation

The identity currently has no tags.

Recommended governance tags:

- Project: BonganiSecure
- Environment: Lab
- Owner: Security Engineering
- Purpose: Workload Identity Testing
- Classification: Non-Production

Tags improve resource ownership, inventory and governance.

## 6. Security Findings

| Finding | Assessment |
|---|---|
| Managed identity exists | Verified |
| Identity type | User-assigned |
| Reader role assigned | Verified |
| Subscription-wide scope | Verified |
| Write permissions observed | None in the returned role assignment |
| Resource tags | Not configured |
| Least-privilege review | Recommended |

## 7. Assessment Limitations

This assessment records the configuration observed during the review.

It does not establish whether the identity is currently attached to a workload, actively used, or required to retain subscription-wide Reader access.

No permissions or Azure resources were changed during this assessment.

## 8. Conclusion

The existing managed identity provides a practical example of Azure workload identity management.

The principal security recommendation is to validate the need for subscription-wide Reader access and apply a narrower scope where appropriate.

**Evidence classification:** Live Azure configuration observed through Azure Cloud Shell.

**Project:** BonganiSecure Azure Workload Identity and RBAC Security Lab.
