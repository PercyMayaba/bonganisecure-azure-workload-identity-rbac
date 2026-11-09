# Service Principal Security Assessment

## 1. Assessment Overview

This assessment reviews the Microsoft Entra Enterprise Application `BonganiSecure-Finance-Portal-Lab`.

The objective is to assess its service principal configuration, permissions, application assignments and access controls.

## 2. Identity Inventory

| Attribute | Observed result |
|---|---|
| Enterprise Application | BonganiSecure-Finance-Portal-Lab |
| Application ID | Populated |
| Service Principal Object ID | Populated |
| Enterprise Application | Present |
| App registration visibility | Not found in current App registrations list |

## 3. Permission Assessment

The Enterprise Application Permissions page displayed:

**No admin-consented permissions for the app.**

No admin-consented API permissions were identified during this inspection.

## 4. Application Assignment Assessment

The Users and groups page displayed:

**No app assignments found.**

No user or group assignments were identified during this inspection.

## 5. Authentication and Access Properties

| Control | Observed state |
|---|---|
| Enabled for users to sign in | Yes |
| Assignment required | Yes |

Assignment required is enabled, but no assignments currently exist.

An actual user sign-in test was not performed.

## 6. Security Analysis

The service principal exists and has no admin-consented permissions or user/group assignments identified during this review.

Assignment required is enabled, which provides an additional access restriction for applications configured to use assignment-based access.

The absence of assignments means no assigned users or groups were identified.

The app registration was not visible in the current App registrations list, although the Enterprise Application and service principal were present. This discrepancy requires further investigation.

## 7. Recommendations

1. Investigate why the application registration is not visible.
2. Confirm the application's business purpose and ownership.
3. Retain assignment required if assignment-based access is intended.
4. Grant access only to approved users or groups when required.
5. Review API permissions before granting admin consent.
6. Monitor service principal permissions and assignments over time.

## 8. Evidence Limitations

This assessment records portal observations.

No application permissions or assignments were changed.

No actual application authentication or API access test was performed.

## 9. Conclusion

The Enterprise Application currently presents a minimally configured service principal from the perspective of the inspected permissions and assignment settings.

Further investigation is required to reconcile the missing App registrations entry and establish the application's ownership and operational purpose.

## 10. Azure CLI Verification

The service principal was independently inspected using Azure Cloud Shell.

| Attribute | Result |
|---|---|
| Service principal returned by CLI | Yes |
| Account enabled | True |
| Display name search | Successful using partial-name matching |

This confirms that the Enterprise Application's service principal is enabled and retrievable through Azure CLI.

The initial exact-name query returned no results, but a partial-name search successfully located the service principal.

No application configuration or permissions were changed during this verification.
## 11. Azure RBAC Assessment

The Finance service principal was queried for Azure RBAC role assignments using Azure Cloud Shell.

**Observed result:** No role assignments were returned.

### Security interpretation

No Azure RBAC permissions were identified for this service principal through the queried role assignments.

This limits its direct Azure resource access through Azure RBAC, based on the evidence inspected.

This finding does not establish that the application has no access through other authorization mechanisms, such as Microsoft Graph permissions or application-specific access controls.

### Recommendation

Maintain least-privilege access. Grant Azure RBAC roles only when the application has a documented requirement, and scope those assignments to the minimum necessary resources.

No permissions were changed during this assessment.
## 12. Service Principal Ownership Review

The service principal owner query returned no owners.

### Security observation

No application owners were identified through the inspected Microsoft Entra service principal owner records.

An owner should be assigned to provide accountability for application identity governance, permission reviews and lifecycle management.

### Recommendation

1. Identify the responsible application or security team.
2. Assign an appropriate owner through Microsoft Entra.
3. Review ownership periodically.
4. Ensure ownership is transferred when personnel or responsibilities change.

### Evidence limitation

The empty owner query does not establish that no team or individual is operationally responsible. It establishes only that no owners were returned by this query.

# Managed Identity RBAC Least-Privilege Improvement

## 1. Current Configuration

| Attribute | Current state |
|---|---|
| Identity | mi-bongani-day1 |
| Identity type | User-assigned managed identity |
| Role | Reader |
| Scope | Azure subscription |
| Additional roles identified | None |

## 2. Security Observation

The identity has subscription-wide Reader access.

Reader is a read-only role, but its subscription-level scope provides visibility across a wider environment than may be required.

## 3. Proposed Improvement

Consider narrowing the Reader assignment to the BonganiSecurity resource group.

| Attribute | Proposed state |
|---|---|
| Identity | mi-bongani-day1 |
| Role | Reader |
| Scope | BonganiSecurity resource group |

## 4. Expected Security Benefit

A narrower scope would reduce the identity's visibility into unrelated Azure resources.

It would demonstrate least-privilege access design while retaining read-only access to the lab resource group.

## 5. Preconditions

Before implementing the change:

1. Identify the workload using the identity.
2. Confirm whether it requires subscription-wide visibility.
3. Check for dependencies on resources outside BonganiSecurity.
4. Confirm that resource-group Reader permissions satisfy the workload's requirements.
5. Plan a controlled change and rollback.

## 6. Implementation Status

**Status: Proposed, not implemented.**

The existing subscription-level Reader assignment has not been changed.

No Azure permissions were modified during this assessment.

## 7. Conclusion

Reducing the scope of the managed identity's Reader role is a potential least-privilege improvement.

Implementation should follow workload dependency validation and a controlled access-change process.
