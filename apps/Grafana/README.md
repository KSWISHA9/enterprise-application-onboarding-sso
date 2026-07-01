## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [GitHub Enterprise SAML Onboarding](../GitHub-Enterprise/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [Atlassian Jira SAML Onboarding](../Jira/README.md)
- [ServiceNow SAML Onboarding](../ServiceNow/README.md)
- [Slack SAML Onboarding](../Slack/README.md)
- [Zoom SAML Onboarding](../Zoom/README.md)
- [SCIM Provisioning](../SCIM-Provisioning/README.md)

---
# APP-1001 — Grafana Application Onboarding

## 1. Business Request

The Infrastructure Operations team requested Single Sign-On for Grafana to reduce local account usage, centralize authentication, and prepare the platform for group-based access control.

---

## 2. Authentication Protocol

| Area | Configuration |
|---|---|
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | Grafana |
| Authentication Flow | SP-Initiated SAML |
| Certificate | Microsoft Entra token signing certificate |

---

## 3. Provisioning Method

| Area | Configuration |
|---|---|
| Provisioning Method | Manual |
| SCIM | Not configured |
| Future State | Group-based provisioning / lifecycle automation |

---

## 4. Groups / RBAC

Grafana access was designed around future group-based RBAC. Microsoft Entra ID groups can be used to assign access to the enterprise application and later mapped into Grafana roles.

| Group | Purpose |
|---|---|
| Grafana-Admins | Platform administration |
| Grafana-Editors | Dashboard editing |
| Grafana-Viewers | Read-only access |

---

## 5. Claims / Attributes

| Claim / Attribute | Purpose |
|---|---|
| NameID | Primary user identifier |
| Email | User email mapping |
| Display Name | User profile display |
| Group Claim | Future RBAC mapping |

---

## 6. Configuration Steps

1. Created the Grafana Enterprise Application in Microsoft Entra ID.
2. Selected SAML as the authentication protocol.
3. Configured Basic SAML settings.
4. Downloaded Microsoft Entra SAML metadata and certificate values.
5. Configured Grafana SAML settings with Entra IdP information.
6. Reviewed default and advanced claims.
7. Added group claim support for future RBAC.
8. Validated SAML configuration readiness.

---

## 7. Validation

- SAML application created in Microsoft Entra ID.
- Grafana SAML settings populated.
- Microsoft Entra metadata available.
- Group claim configuration added.
- SAML configuration reached ready/enabled state.

---

## 8. Troubleshooting

- Reply URL mismatch
- Incorrect Entity ID
- Missing or incorrect certificate metadata
- Claim mapping issues
- Group claim formatting issues

---

## 9. Operational Handoff

| Area | Owner |
|---|---|
| Application Owner | Infrastructure Operations |
| Identity Owner | IAM Team |
| Authentication | SAML 2.0 |
| Provisioning | Manual |
| Future Work | RBAC mapping and automated provisioning |

---

## 10. Screenshots

### 1. Application Overview

Shows the Grafana Enterprise Application created in Microsoft Entra ID.

![Application Overview](apps/Grafana/screenshots/01-Application-Overview.png)

---
### 2. Blank SAML Configuration

Shows the initial SAML configuration state before values were added.

![Blank SAML Configuration](apps/Grafana/screenshots/02-SAML-Configuration-Blank.png)

---
### 3. Basic SAML Configuration

Shows the SAML configuration area where Entity ID and Reply URL values are configured.

![Basic SAML Configuration](apps/Grafana/screenshots/07-Entra-Basic-SAML-Configuration.png)

---
### 4. Grafana SAML Settings

Shows the Grafana-side SAML configuration where IdP values are entered.

![Grafana SAML Settings](apps/Grafana/screenshots/04-Grafana-SAML-Settings.png)

---
### 5. Sign Requests

Shows Grafana settings for signed SAML requests.

![Sign Requests](apps/Grafana/screenshots/05-Grafana-Sign-Requests.png)

---
### 6. Identity Provider Configuration

Shows the Grafana identity provider configuration workflow.

![Identity Provider Configuration](apps/Grafana/screenshots/06-Grafana-Identity-Provider-Configuration.png)

---
### 7. Attributes and Claims

Shows default claim mappings in Microsoft Entra ID.

![Attributes and Claims](apps/Grafana/screenshots/08-Default-Attributes-Claims.png)

---
### 8. Group Claim Added

Shows group claim configuration for future RBAC.

![Group Claim Added](apps/Grafana/screenshots/11-Group-Claim-Added.png)

---
### 9. SAML Certificate Metadata

Shows Microsoft Entra SAML certificate and metadata values.

![SAML Certificate Metadata](apps/Grafana/screenshots/12-SAML-Certificate-Metadata.png)

---
### 10. SAML Ready

Shows the SAML configuration reaching a ready/enabled state.

![SAML Ready](apps/Grafana/screenshots/16-SAML-Configuration-Ready.png)

---

## Engineering Takeaways

This onboarding demonstrated SAML application onboarding, IdP/SP metadata exchange, certificate handling, claims review, and RBAC planning for an infrastructure monitoring platform.
