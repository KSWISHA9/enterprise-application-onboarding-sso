## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [ServiceNow SAML Onboarding](../ServiceNow/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [Custom OIDC Application](../Custom-OIDC-App/README.md)
- [SCIM Provisioning](../SCIM-Provisioning/README.md)

---

# APP-1003 — GitHub Enterprise Cloud SAML Onboarding

## Overview

This application onboarding package documents the integration of GitHub Enterprise Cloud with Microsoft Entra ID using SAML 2.0. The objective was to centralize authentication for GitHub Enterprise Cloud, reduce standalone credential usage, and validate a real enterprise federation workflow.

This onboarding was completed against a GitHub Enterprise Cloud trial environment and Microsoft Entra ID tenant.

---

## Business Request

The Development Engineering team requested Single Sign-On for GitHub Enterprise Cloud to centralize identity management, enforce corporate authentication policies, and prepare GitHub access for future governance, provisioning, and lifecycle automation.

---

## Business Requirements

- Integrate GitHub Enterprise Cloud with Microsoft Entra ID
- Authenticate users using SAML 2.0
- Centralize GitHub authentication through the corporate identity provider
- Reduce local credential dependency
- Configure token signing certificate trust
- Validate SAML authentication before enforcing SSO
- Document implementation, troubleshooting, and operational handoff

---

## Why SAML?

GitHub Enterprise Cloud supports enterprise SSO using SAML and OIDC. SAML was selected for this onboarding because it is widely used for enterprise SaaS federation and remains a common requirement in IAM engineering roles.

SAML allows GitHub Enterprise Cloud to trust Microsoft Entra ID as the Identity Provider while GitHub operates as the Service Provider. Microsoft Entra ID authenticates the user and issues a signed SAML assertion. GitHub validates the assertion using the configured issuer, sign-on URL, and X.509 signing certificate.

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Application | GitHub Enterprise Cloud |
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | GitHub Enterprise Cloud |
| Enterprise | OmniVerse Enterprise |
| Provisioning | Manual |
| Certificate | Microsoft Entra token signing certificate |
| Status | Successfully Configured and Validated |

---

## SAML Configuration

| Setting | Value |
|---|---|
| Entity ID | `https://github.com/enterprises/omniverse-enterprise` |
| Reply URL / ACS URL | `https://github.com/enterprises/omniverse-enterprise/saml/consume` |
| Sign-On URL | Microsoft Entra Login URL |
| Issuer | Microsoft Entra Identifier |
| Certificate | Entra ID X.509 token signing certificate |
| Signature Method | RSA-SHA256 |
| Digest Method | SHA256 |

---

## Claims Mapping

| Claim | Source Attribute |
|---|---|
| Given Name | `user.givenname` |
| Surname | `user.surname` |
| Email Address | `user.mail` |
| Name | `user.userprincipalname` |
| Unique User Identifier | `user.userprincipalname` |

---

## Validation Results

Validation confirmed that:

- GitHub Enterprise redirected authentication to Microsoft Entra ID.
- Microsoft Entra ID authenticated the user.
- GitHub Enterprise accepted the SAML response.
- The SAML trust relationship was successfully validated.
- GitHub displayed a successful SAML authentication result.

**Result:** Passed — Successfully authenticated the SAML SSO identity.

---

# Screenshots

## 1. GitHub Enterprise Trial Creation

This screenshot documents the creation of the GitHub Enterprise Cloud trial environment. Microsoft Entra ID was selected as the identity provider during setup, which aligns the enterprise environment with the centralized identity model used across OmniVerse Enterprise.

![GitHub Enterprise Trial](../../screenshots/01-github-enterprise-trial.png)

---

## 2. GitHub Organization Created

This screenshot shows the OmniVerse Enterprise GitHub organization. The organization provides the application scope that will later be protected by enterprise-level SAML authentication.

![GitHub Organization Created](../../screenshots/02-github-organization-created.png)

---

## 3. GitHub Authentication Security Settings

This screenshot shows the GitHub Enterprise authentication security area where SAML Single Sign-On is configured. This confirms that the GitHub Enterprise environment supports enterprise identity provider integration.

![GitHub Authentication Security](../../screenshots/03-github-security-settings.png)

---

## 4. Microsoft Entra Gallery Application

This screenshot documents selection of the GitHub Enterprise Cloud application from the Microsoft Entra application gallery. Choosing the correct gallery application is important because GitHub provides different integrations for organization-level and enterprise-level SSO.

![Microsoft Entra Gallery Application](../../screenshots/04-github-enterprise-gallery-application.png)

---

## 5. GitHub SAML Configuration Page

This screenshot shows the GitHub Enterprise SAML configuration page where the Microsoft Entra Login URL, Issuer, and public X.509 signing certificate are entered. These values establish trust between GitHub Enterprise Cloud and Microsoft Entra ID.

![GitHub SAML Configuration Page](../../screenshots/05-github-saml-configuration-page.png)

---

## 6. Microsoft Entra Basic SAML Configuration

This screenshot shows the completed Basic SAML Configuration in Microsoft Entra ID. The Entity ID and Reply URL establish the Service Provider details required for Entra ID to issue SAML assertions to GitHub Enterprise Cloud.

![Basic SAML Configuration](../../screenshots/06-github-basic-saml-configuration.png)

---

## 7. SAML Authentication Test

This screenshot shows Microsoft Entra ID authentication during the GitHub SAML validation process. The redirect to Microsoft confirms that GitHub is using Microsoft Entra ID as the configured Identity Provider.

![SAML Authentication Test](../../screenshots/07-github-saml-authentication.png)

---

## 8. Successful SAML Validation

This screenshot confirms that GitHub Enterprise successfully validated the SAML configuration. The successful test proves that Microsoft Entra ID issued a valid SAML response and GitHub Enterprise accepted it.

![Successful SAML Validation](../../screenshots/08-github-saml-validation-success.png)

---

# Troubleshooting

## Issue 1 — Wrong GitHub Enterprise Application Type

### Problem

The first Microsoft Entra gallery application selected was not aligned with the GitHub Enterprise SSO configuration being performed.

### Root Cause

GitHub provides multiple Microsoft Entra gallery applications, including organization-level and enterprise-level integrations. Selecting the wrong application type can cause mismatched identifiers, reply URLs, or SAML request behavior.

### Resolution

The GitHub Enterprise Cloud Enterprise Account application was selected and configured with the enterprise-level GitHub SAML values.

### Result

The SAML configuration matched the GitHub Enterprise environment and authentication testing proceeded successfully.

---

## Issue 2 — AADSTS650056 Misconfigured Application

### Problem

During testing, Microsoft Entra ID returned an AADSTS650056 misconfigured application error.

### Root Cause

The SAML request was associated with a different client application than the one configured in Microsoft Entra ID. This indicated a mismatch between the selected GitHub gallery application and the GitHub Enterprise SAML configuration.

### Resolution

The application selection and SAML configuration were reviewed. The correct GitHub Enterprise application was configured with the enterprise ACS URL, Entity ID, and Microsoft Entra IdP metadata.

### Result

GitHub Enterprise successfully authenticated the SAML SSO identity after the configuration was corrected.

---

# Engineering Takeaways

This onboarding demonstrated a real enterprise SAML federation between GitHub Enterprise Cloud and Microsoft Entra ID.

Key engineering activities included:

- Enterprise application onboarding
- SAML 2.0 federation
- Microsoft Entra gallery application selection
- Entity ID and ACS URL configuration
- X.509 certificate trust
- Metadata exchange
- Claims mapping
- SAML validation
- Authentication troubleshooting
- Enterprise documentation

---

# Future Enhancements

- Enforce SAML SSO after validating break-glass access
- Configure SCIM provisioning if available
- Add Microsoft Entra group-based assignment
- Integrate Conditional Access policies
- Document break-glass recovery procedure
- Monitor GitHub SSO sign-ins through Microsoft Entra logs
- Add access reviews for GitHub organization membership

