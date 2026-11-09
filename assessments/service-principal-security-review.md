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
