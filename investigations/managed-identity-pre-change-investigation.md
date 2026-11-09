# Managed Identity Pre-Change Investigation

## 1. Objective

Investigate the usage, dependencies and RBAC permissions of `mi-bongani-day1` before considering a subscription-level Reader scope reduction.

## 2. Identity details

- Identity: `mi-bongani-day1`
- Type: User-assigned managed identity
- Resource group: `BonganiSecurity`
- Current RBAC role: Reader
- Current scope: Azure subscription

## 3. Workload attachment investigation

A subscription-wide Azure resource inventory was performed to identify resources with user-assigned managed identities attached.

**Finding:** No attached resources were returned by the inventory query.

This does not prove that the identity has no external dependencies or integrations.

## 4. RBAC investigation

Azure CLI returned one assignment for the managed identity:

| Role | Scope |
|---|---|
| Reader | Subscription |

No additional role assignments were returned.

## 5. Activity Log investigation

A 90-day Activity Log query returned management operations associated with the managed identity resource ID.

Observed outcomes included:
- Succeeded
- Started
- Failed

The caller information showed the user's email accounts.

These records demonstrate administrative management activity. They do not establish workload authentication or prove that the identity is being used by an application.

## 6. Metadata investigation

- Creation timestamp: Null
- Last modification timestamp: Null
- Tags: None

The available metadata was insufficient to establish identity age or operational ownership.

## 7. Security assessment

Subscription-level Reader provides broader visibility than the intended `BonganiSecurity` resource group boundary.

No workload attachment was identified, but external dependencies and workload ownership remain unconfirmed.

## 8. Recommendation

Before implementing the proposed RBAC scope reduction:

1. Confirm the identity's owner and intended workload.
2. Investigate external integrations and dependencies.
3. Test resource-group-level Reader access.
4. Verify workload functionality.
5. Remove subscription-level Reader only after successful validation.

## 9. Change status

**Investigation completed. Scope reduction not implemented.**

No Azure permissions were changed during this investigation.
