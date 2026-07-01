## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [GitHub Enterprise SAML Onboarding](../GitHub-Enterprise/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [Atlassian Jira SAML Onboarding](../Jira/README.md)

---

# APP-1006 - Cisco Duo Identity Integration with Microsoft Entra ID

## Overview

This onboarding package documents the integration of Cisco Duo with Microsoft Entra ID using Azure authorization, administrator consent, and automatic Enterprise Application registration.

Unlike traditional SAML-only onboarding, this integration demonstrates a modern identity security workflow involving Duo, Microsoft Entra ID, OAuth 2.0 authorization, admin consent, and audit log validation.

---

## Business Request

The security team requested Cisco Duo integration with Microsoft Entra ID to strengthen multi-factor authentication, improve identity protection, and prepare for Zero Trust access controls.

---

## Business Objectives

- Integrate Cisco Duo with Microsoft Entra ID
- Authorize Duo to access required Entra directory data
- Validate Enterprise Application creation in Microsoft Entra ID
- Document admin consent and audit evidence
- Prepare the environment for future Conditional Access and Zero Trust policies

---

## Application Information

| Item | Value |
|---|---|
| Application | Cisco Duo |
| Microsoft Integration | Duo Azure Authentication |
| Identity Platform | Microsoft Entra ID |
| Integration Type | OAuth 2.0 Authorization / Admin Consent |
| Security Capability | MFA / Conditional Access / Universal Prompt |
| Status | Completed |

---

## Architecture

```text
User
  |
  v
Microsoft Entra ID
  |
  v
Duo Azure Authentication Enterprise Application
  |
  v
Cisco Duo
  |
  v
MFA / Universal Prompt / Conditional Access Integration
```

---

## Implementation Summary

1. Opened Cisco Duo Single Sign-On configuration.
2. Reviewed available Duo SSO applications.
3. Selected Microsoft Azure Active Directory integration.
4. Started Azure authorization from Cisco Duo.
5. Granted Microsoft Entra administrator consent.
6. Verified Duo Azure Authentication Enterprise Application in Entra.
7. Confirmed audit logs showing service principal creation, delegated permissions, and consent activity.

---

## Validation

Validation was completed using Microsoft Entra Enterprise Applications and audit logs.

Evidence confirmed:

- Duo Azure Authentication Enterprise Application was created.
- Application ID matched the Duo custom control configuration.
- Admin consent was granted successfully.
- Delegated permissions were added.
- Service principal creation was logged.
- Application role assignment activity was recorded.

---

## Screenshots

### 1. Cisco Duo Single Sign-On Dashboard

Shows the Cisco Duo Single Sign-On dashboard where the Azure AD integration was initiated.

![Duo SSO Dashboard](../../screenshots/01-duo-single-sign-on-dashboard.png)

---

### 2. Duo SSO Application Catalog

Shows the available Duo SSO applications, including the Microsoft Azure Active Directory option.

![Duo SSO Applications](../../screenshots/02-duo-sso-applications.png)

---

### 3. Azure Authorization Step

Shows the Azure authorization request initiated from within Cisco Duo.

![Duo Azure Authorization](../../screenshots/03-duo-azure-authorization.png)

---

### 4. Microsoft Entra Admin Consent

Shows the Microsoft Entra administrator consent screen where permissions were reviewed and granted.

![Microsoft Consent](../../screenshots/04-duo-microsoft-consent.png)

---

### 5. Duo Azure Application Configuration

Shows the Duo Azure application configuration confirming the integration settings.

![Duo Azure App Configuration](../../screenshots/05-duo-azure-application-configuration.png)

---

### 6. Duo Enterprise Application in Entra

Shows the Duo Azure Authentication Enterprise Application created automatically in Microsoft Entra ID after admin consent.

![Entra Duo Enterprise Application](../../screenshots/06-entra-duo-enterprise-application.png)

---

### 7. Entra Audit Logs

Shows the Microsoft Entra audit logs confirming service principal creation, delegated permissions, and consent activity.

![Entra Duo Audit Logs](../../screenshots/07-entra-duo-audit-logs.png)

---

## Security Considerations

- Administrator consent should be reviewed before approval.
- Enterprise Applications should be monitored for permissions and ownership.
- Audit logs should be retained for compliance evidence.
- Duo policies should be aligned with Conditional Access requirements.
- Break-glass accounts should be excluded from restrictive MFA policies.
- This integration should be revisited during IAM-004 Conditional Access and Zero Trust.

---

## Lessons Learned

Cisco Duo uses a different onboarding pattern than traditional SAML applications. Instead of manually creating an Entra Enterprise Application first, the integration begins in Duo, requests Microsoft Entra authorization, and creates the Duo Azure Authentication Enterprise Application automatically after admin consent.

This demonstrates an important IAM engineering concept: not all enterprise integrations follow the same SAML setup pattern. Understanding OAuth-based admin consent flows is critical for modern IAM work.

---

## Operational Handoff

The Duo integration is ready for future Conditional Access and Zero Trust policy testing. The application should be monitored through:

- Microsoft Entra Enterprise Applications
- Microsoft Entra Audit Logs
- Duo Authentication Logs
- Duo Policy Configuration
- Conditional Access Policies

---

## Related Projects

| Project | Description |
|---|---|
| [IAM-001 Hybrid Identity](https://github.com/KSWISHA9/hybrid-identity-engineering) | Active Directory + Microsoft Entra Connect |
| [APP-1001 Grafana](../Grafana/README.md) | SAML 2.0 onboarding |
| [APP-1002 WordPress](../WordPress/README.md) | OpenID Connect onboarding |
| [APP-1003 GitHub Enterprise](../GitHub-Enterprise/README.md) | SAML 2.0 onboarding |
| [APP-1004 Salesforce](../Salesforce/README.md) | SAML 2.0 onboarding |
| [APP-1005 Atlassian Jira](../Jira/README.md) | SAML 2.0 onboarding |
| IAM-004 Conditional Access and Zero Trust | Upcoming |

---

## Future Enhancements

- Configure Duo with Microsoft Entra Conditional Access
- Test Universal Prompt authentication
- Add Duo policy enforcement scenarios
- Document risk-based authentication
- Connect to IAM-004 Conditional Access and Zero Trust
