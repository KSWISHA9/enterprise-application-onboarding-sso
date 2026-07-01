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

This application onboarding package documents the integration of GitHub Enterprise Cloud with Microsoft Entra ID using SAML 2.0. The objective was to centralize authentication for GitHub Enterprise Cloud, eliminate local GitHub credentials, and demonstrate a repeatable SAML federation onboarding process.

---

## Business Request

The Engineering team requested Single Sign-On for GitHub Enterprise Cloud to centralize identity management, enforce corporate authentication policies, and eliminate standalone GitHub credentials across the organization.

---

## Business Requirements

- Integrate GitHub Enterprise Cloud with Microsoft Entra ID
- Authenticate users using SAML 2.0
- Eliminate local GitHub credential management
- Centralize identity management
- Validate SAML-based authentication
- Document a repeatable onboarding process

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Application | GitHub Enterprise Cloud |
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | GitHub Enterprise Cloud |
| Gallery Application | GitHub Enterprise Cloud (Entra Gallery) |
| Provisioning | Manual |
| Status | Successfully Configured |

---

## Configuration Highlights

The implementation included:

- Provisioning a GitHub Enterprise Cloud trial organization
- Locating the GitHub Enterprise Cloud gallery application in Microsoft Entra ID
- Configuring Basic SAML settings including Entity ID and Reply URL
- Downloading the Entra ID SAML signing certificate
- Configuring SAML SSO settings within GitHub Enterprise Security
- Validating SAML authentication end-to-end

---

## Validation

### 1. GitHub Enterprise Trial Creation
![Enterprise Trial](../../screenshots/01-github-enterprise-trial.png)

### 2. GitHub Organization Created
![Organization](../../screenshots/01-github-organization-created.png)

### 3. Authentication Security Settings
![Security](../../screenshots/02-github-security-settings.png)

### 4. Microsoft Entra Gallery Application
![Gallery](../../screenshots/01-github-enterprise-gallery-application.png)

### 5. GitHub SAML Configuration Page
![GitHub SAML](../../screenshots/01-github-saml-configuration-page.png)

### 6. Basic SAML Configuration
![Basic SAML](../../screenshots/02-github-basic-saml-configuration.png)

### 7. SAML Authentication Test
![Authentication](../../screenshots/07-github-saml-authentication.png)

### 8. Successful SAML Validation
![Validation](../../screenshots/08-github-saml-validation-success.png)

---

## Skills Demonstrated

- Enterprise Application Onboarding
- Microsoft Entra ID
- SAML 2.0 Federation
- Claims Mapping
- Certificate Management
- Metadata Exchange
- Authentication Validation
