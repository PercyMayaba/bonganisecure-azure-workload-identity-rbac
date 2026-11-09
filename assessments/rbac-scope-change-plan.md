# Azure RBAC Scope Reduction and Change Plan

## 1. Objective

Reduce excessive permissions assigned to the user-assigned managed identity `mi-bongani-day1` by narrowing its Reader role from subscription scope to the `BonganiSecurity` resource group.

## 2. Current verified configuration

| Field | Value |
|---|---|
| Identity | mi-bongani-day1 |
| Identity type | User-assigned managed identity |
| Current role | Reader |
| Current scope | Azure subscription |
| Intended workload scope | BonganiSecurity resource group |

The assignment was verified using Azure CLI by matching the managed identity's principal ID against the RBAC assignment record.

## 3. Proposed configuration

| Field | Proposed value |
|---|---|
| Identity | mi-bongani-day1 |
| Role | Reader |
| Target scope | BonganiSecurity resource group |
| Change type | RBAC scope reduction |
| Status | Proposed, not implemented |

## 4. Security justification

Subscription-wide Reader access provides visibility beyond the intended workload boundary.

Restricting the assignment to the resource group follows the principle of least privilege and reduces unnecessary access to unrelated subscription resources.

## 5. Pre-change checks

Before implementation:

1. Confirm workload ownership and purpose.
2. Identify all dependencies that may require access outside the resource group.
3. Confirm the workload can operate with resource-group-level Reader.
4. Record the existing assignment ID and scope.
5. Confirm an authorised administrator can perform and reverse the change.

The resource attachment query returned no resources using the managed identity. This is not proof that no external dependencies exist.

## 6. Proposed implementation sequence

1. Create a Reader assignment at the `BonganiSecurity` resource-group scope.
2. Verify the new assignment against the managed identity's principal ID.
3. Test the workload and confirm required access.
4. Remove the subscription-level Reader assignment only after successful verification.
5. Confirm the final RBAC configuration.

## 7. Rollback plan

If the workload loses required access:

1. Recreate the original subscription-level Reader assignment.
2. Verify the restored assignment.
3. Investigate the dependency that required broader access.
4. Retain the narrower assignment only if it remains operationally appropriate.

## 8. Change status

**Proposed only.**

No RBAC assignments have been modified as part of this planning exercise.

## 9. Engineering outcome

This change plan demonstrates Azure IAM engineering practices, including least privilege, RBAC scope management, change control, verification and rollback planning.
