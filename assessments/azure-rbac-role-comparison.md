# Azure RBAC Built-in Role Comparison

## 1. Objective

This assessment examines three fundamental Azure built-in roles: Reader, Contributor and Owner. The purpose is to understand how Azure Role-Based Access Control (RBAC) separates resource visibility, resource management and access administration.

## 2. Role comparison

| Role | Resource access | Access administration |
|---|---|---|
| Reader | View resources | Cannot assign roles |
| Contributor | Create, modify and delete resources | Cannot assign roles |
| Owner | Full resource access | Can assign roles and manage access |

## 3. Security observations

- Reader supports read-only operational visibility.
- Contributor provides resource management capabilities without granting general RBAC role-assignment authority.
- Owner is highly privileged because it combines resource management with access administration.
- Assigning Owner unnecessarily increases the risk of privilege escalation and excessive access.

## 4. Least-privilege recommendation

Use the lowest level of access required for each identity.

Where a workload only needs to read resources, Reader may be sufficient. Contributor should only be considered where resource modification is required. Owner should be restricted to authorised administrators with a clearly justified operational requirement.

## 5. Lab verification

The three role definitions were inspected using Azure CLI:

- Reader
- Contributor
- Owner

No role assignments were changed as part of this comparison.

## 6. Scope and limitations

This assessment documents built-in role definitions. It does not claim that every possible permission, data-plane permission or resource-specific restriction has been exhaustively tested.

## 7. Engineering outcome

This exercise demonstrates an understanding of Azure RBAC privilege boundaries and the importance of least-privilege access design in cloud environments.
