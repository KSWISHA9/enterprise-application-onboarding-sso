## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [GitHub Enterprise SAML Onboarding](../GitHub-Enterprise/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [Atlassian Jira SAML Onboarding](../Jira/README.md)
- [Cisco Duo Identity Integration](../Cisco-Duo/README.md)
- [Keycloak SAML Federation](../Keycloak/README.md)

---

# APP-1008 - SCIM Provisioning with Microsoft Entra ID and Atlassian Cloud

## Overview

This onboarding package documents the configuration of SCIM 2.0 automated provisioning between Microsoft Entra ID and Atlassian Cloud.

After configuring SAML Single Sign-On for Atlassian Jira, SCIM provisioning was layered on top to automate the full user lifecycle — eliminating manual account creation, attribute drift, and deprovisioning gaps.

---

## Business Request

The Identity and Access Management team requested automated user provisioning for Atlassian Cloud to eliminate manual account management, ensure consistent attribute synchronization, and enable automatic deprovisioning when users leave the organization.

---

## Business Objectives

- Configure SCIM 2.0 automatic provisioning from Microsoft Entra ID to Atlassian Cloud
- Establish secure API connectivity using Atlassian SCIM credentials
- Validate attribute mapping between Entra ID and Atlassian Cloud
- Test provisioning using Provision on Demand before enabling full sync
- Monitor and validate provisioning activity through provisioning logs

---

## Architecture

```text
Microsoft Entra ID
        |
        | SCIM 2.0 over HTTPS
        v
Atlassian Cloud SCIM Endpoint
        |
        v
Atlassian Cloud User Directory
        |
        v
Jira / Confluence / Atlassian Apps
```

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Protocol | SCIM 2.0 |
| Identity Provider | Microsoft Entra ID |
| Target Application | Atlassian Cloud |
| Provisioning Mode | Automatic |
| Scope | Assigned users and groups |
| Object Actions | Create, Update, Delete |
| Connectivity | Atlassian SCIM Base URL and API Key |
| Status | Successfully Configured |

---

## Configuration Steps

1. Opened the Atlassian Cloud Enterprise Application in Microsoft Entra ID.
2. Navigated to Provisioning and set Provisioning Mode to Automatic.
3. Retrieved the SCIM Base URL and API Key from Atlassian Administration.
4. Entered the SCIM credentials into Microsoft Entra ID Admin Credentials.
5. Tested connectivity and confirmed a successful connection.
6. Reviewed and configured attribute mappings.
7. Configured scoping filters to provision assigned users only.
8. Ran Provision on Demand to validate provisioning before full sync.
9. Resolved provisioning errors identified during testing.
10. Reviewed provisioning logs to confirm successful user creation.

---

## SCIM Attribute Mapping

| Microsoft Entra ID | Atlassian Cloud | Mapping Type |
|---|---|---|
| userPrincipalName | userName | Direct |
| givenName | name.givenName | Direct |
| surname | name.familyName | Direct |
| mail | emails[type eq "work"].value | Direct |
| objectId | externalId | Direct |
| Switch([IsSoftDeleted]) | active | Expression |

---

## Validation

- Provisioning Mode set to Automatic.
- SCIM connectivity validated using Test Connection.
- Attribute mappings confirmed for all required user attributes.
- Provision on Demand successfully created a test user in Atlassian Cloud.
- Provisioning logs confirmed synchronization activity.
- Scoping confirmed as assigned users only with Create, Update, Delete enabled.

---

## Screenshots

### 1. SCIM Provisioning Overview

Shows the Atlassian Cloud Enterprise Application provisioning overview in Microsoft Entra ID, including the provisioning configuration workflow.

![SCIM Provisioning Overview](../../screenshots/01-scim-provisioning-overview_png.png)

---

### 2. Admin Credentials Configuration

Shows the SCIM provisioning configuration page where Provisioning Mode was set to Automatic and the Atlassian SCIM Tenant URL and API Key were entered.

![Admin Credentials](../../screenshots/02-scim-admin-credentials_png.png)

---

### 3. SCIM API Key and Provisioning Settings

Shows the Atlassian Administration identity provider page where the SCIM API key was generated and the provisioning connection was established.

![SCIM API Key](../../screenshots/03-scim-api-key-and-provisioning_png.png)

---

### 4. Provisioning Email Error

Shows the provisioning error encountered during initial testing when the mail attribute was not correctly mapped. The error was used to identify the missing attribute mapping before correcting the configuration.

![Provisioning Error](../../screenshots/04-scim-required-email-error_png.png)

---

### 5. Provision on Demand

Shows the Provision on Demand interface used to test provisioning for a specific user before enabling full automatic synchronization.

![Provision on Demand](../../screenshots/Provision_on_Demand.png)

---

### 6. Scoping Filters and Assignments

Shows the scoping configuration confirming provisioning is limited to assigned users, with Create, Update, and Delete lifecycle operations enabled and five users in scope.

![Scoping Configuration](../../screenshots/06-scim-scope-settings-and-assignments_png.png)

---

### 7. Attribute Mapping

Shows the configured attribute mappings between Microsoft Entra ID and Atlassian Cloud, including the soft delete expression mapping for the active attribute.

![Attribute Mapping](../../screenshots/07-scim-attribute-mapping_png.png)

---

### 8. Provisioning Logs

Shows the Microsoft Entra ID provisioning logs confirming synchronization activity for the test user, with source system identified as Microsoft Entra ID.

![Provisioning Logs](../../screenshots/08-scim-provisioning-logs_png.png)

---

## Troubleshooting

### Issue 1 - Missing Email Attribute Mapping

**Problem:** Initial provisioning failed because the required email attribute was not correctly mapped to Atlassian Cloud.

**Root Cause:** The mail attribute was not mapped to `emails[type eq "work"].value`, which is the SCIM-compliant format Atlassian Cloud requires for email addresses.

**Resolution:** Updated the attribute mapping to map `mail` to `emails[type eq "work"].value` using a Direct mapping type. Provisioning completed successfully after the correction.

---

## Lessons Learned

SCIM provisioning requires exact attribute mapping to the target application's SCIM schema. Atlassian Cloud expects email addresses in the `emails[type eq "work"].value` format rather than a simple email field.

Provision on Demand is an essential validation step before enabling full automatic provisioning. It surfaces attribute mapping errors and connectivity issues without affecting the entire user population.

Provisioning logs provide detailed per-object visibility into synchronization status, errors, and attribute values — they should be reviewed after every configuration change.

---

## Operational Handoff

| Area | Owner |
|---|---|
| Identity Provider | IAM Team |
| Target Application | Atlassian Administration |
| Provisioning Mode | Automatic |
| Scope | Assigned users and groups |
| Monitoring | Microsoft Entra ID Provisioning Logs |
| Future Work | Group provisioning, deprovisioning validation, lifecycle automation |

---

## Related Projects

| Project | Description |
|---|---|
| [IAM-001 Hybrid Identity](https://github.com/KSWISHA9/hybrid-identity-engineering) | Active Directory and Microsoft Entra Connect |
| [APP-1001 Grafana](../Grafana/README.md) | SAML 2.0 onboarding |
| [APP-1002 WordPress](../WordPress/README.md) | OpenID Connect onboarding |
| [APP-1003 GitHub Enterprise](../GitHub-Enterprise/README.md) | SAML 2.0 onboarding |
| [APP-1004 Salesforce](../Salesforce/README.md) | SAML 2.0 onboarding |
| [APP-1005 Atlassian Jira](../Jira/README.md) | SAML 2.0 onboarding |
| [APP-1006 Cisco Duo](../Cisco-Duo/README.md) | OAuth 2.0 admin consent |
| [APP-1007 Keycloak](../Keycloak/README.md) | SAML 2.0 identity federation |
| APP-1008 SCIM Provisioning | Current |
| IAM-004 Conditional Access and Zero Trust | Upcoming |

---

## Future Enhancements

- Configure group provisioning and group-to-role mapping
- Validate deprovisioning behavior when users are removed from scope
- Extend SCIM provisioning to additional Atlassian products
- Automate provisioning lifecycle with Microsoft Graph
- Connect to IAM-004 Conditional Access and Zero Trust
