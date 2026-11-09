# Managed Identity Usage Investigation

## 1. Investigation Objective

Determine whether the existing Azure User-Assigned Managed Identity `mi-bongani-day1` is attached to an Azure workload and identify available activity evidence.

## 2. Investigation Environment

- Subscription: Azure sub 1
- Resource group: BonganiSecurity
- Identity: mi-bongani-day1
- Investigation tool: Azure Cloud Shell
- Log source: Azure Activity Log
- Investigation window: Previous 90 days

## 3. Findings

| Investigation | Result |
|---|---|
| Managed identity exists | Confirmed |
| Identity type | User-assigned |
| RBAC assignment | Reader |
| RBAC scope | Subscription |
| Workload attachment query | No matching resources returned |
| Creation metadata | Null |
| Update metadata | Null |
| Matching Activity Log events | No matching events returned |

## 4. Security Analysis

The identity exists and has subscription-wide Reader permissions.

The workload attachment query did not identify an Azure resource using this identity within the inspected resource group.

The Activity Log query returned no matching events during the 90-day investigation window.

These observations raise a potential identity lifecycle governance concern.

However, they do not conclusively establish that the identity is unused or orphaned.

The investigation did not establish whether the identity is attached to resources outside the inspected resource group or whether it has been used through authentication activity not represented in the queried logs.

## 5. Recommendations

1. Identify the business or technical owner of the identity.
2. Confirm whether any workload requires it.
3. Review its subscription-wide Reader assignment.
4. Reduce its RBAC scope if narrower access meets the workload requirement.
5. Apply resource governance tags.
6. Remove the identity only after ownership and dependency checks are complete.

## 6. Evidence Limitations

The investigation used read-only Azure CLI queries.

No permissions, identities or resources were modified.

The results represent the available evidence from the inspected resource group and Activity Log window, not a complete audit of all possible identity usage.

## 7. Conclusion

The managed identity requires an ownership and usage review.

Its subscription-level Reader assignment should be assessed against the principle of least privilege.

**Evidence classification:** Live Azure configuration and read-only investigation.

**Project:** BonganiSecure Azure Workload Identity and RBAC Security Lab.
