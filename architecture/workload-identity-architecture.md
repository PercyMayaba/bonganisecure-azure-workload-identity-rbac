# Azure Workload Identity and RBAC Architecture

## 1. Architecture Overview

This lab demonstrates how Microsoft Azure workload identities can be designed and governed using Microsoft Entra ID and Azure Role-Based Access Control (RBAC).

Workload identities allow applications, services and automated processes to authenticate to Azure resources without relying on an individual employee's account.

The architecture applies Zero Trust principles, least privilege and identity lifecycle governance.

## 2. Core Identity Components

### Microsoft Entra ID

Microsoft Entra ID provides the identity directory and authentication foundation.

It manages application identities, service principals, users and groups.

### App Registrations

An app registration defines an application's identity configuration in Microsoft Entra ID.

It describes the application and its authentication configuration.

### Service Principals

A service principal represents an application identity within a specific Microsoft Entra tenant.

It is the identity that can be assigned permissions to access Azure resources.

### Managed Identities

Managed identities provide Azure-managed credentials for supported workloads.

Two types are relevant:

- System-assigned managed identity: tied to the lifecycle of a specific Azure resource.
- User-assigned managed identity: an independent Azure identity that can be associated with multiple supported resources.

Managed identities reduce the need to store and manage application credentials.

## 3. Azure RBAC Security Model

Azure RBAC controls what an identity can do within an Azure scope.

The main scopes are:

1. Management group.
2. Subscription.
3. Resource group.
4. Individual resource.

Role assignments combine three elements:

- Security principal: the user, group, service principal or managed identity.
- Role definition: the permissions granted.
- Scope: the Azure resources to which the permissions apply.

The lab will prioritise read-only access where possible and avoid unnecessary Contributor or Owner assignments.

## 4. Proposed Architecture

The intended identity flow is:

1. An application or workload uses its assigned identity.
2. Microsoft Entra ID authenticates the workload.
3. The workload obtains an access token for the intended Azure resource.
4. Azure evaluates the identity's RBAC role assignments.
5. Access is granted or denied according to the assigned permissions.
6. Identity activity and configuration are reviewed for security risks.

## 5. Security Controls

The lab will assess the following controls:

- Least-privilege role assignments.
- Service principal governance.
- Managed identity configuration.
- Application permission exposure.
- Credential and secret management.
- Role assignment scope.
- Privileged identity exposure.
- Unnecessary or excessive permissions.
- Identity lifecycle and access removal.

## 6. Implementation Boundaries

This repository distinguishes three implementation states:

**Live configuration:** Azure or Microsoft Entra settings that have actually been configured and verified.

**Simulated investigation:** Synthetic identity events and security scenarios used to demonstrate investigation techniques.

**Planned architecture:** Components documented for engineering purposes but not yet deployed.

No simulated or planned component will be represented as a live Azure deployment.

## 7. Cost Management

The project will prioritise Microsoft Entra ID Free capabilities, existing Azure subscription resources and low-cost Azure control-plane operations.

No virtual machines or other potentially billable compute resources will be deployed without reviewing their costs first.

## 8. Engineering Outcome

The completed project will demonstrate the ability to:

- Explain Azure workload identity architecture.
- Assess managed identities and service principals.
- Design Azure RBAC role assignments.
- Identify excessive application permissions.
- Investigate workload identity security risks.
- Document identity security findings and recommendations.

**Project status:** Architecture documented; implementation and verification in progress.
