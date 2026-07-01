## Enterprise Application Packages

- [Repository Home](../../README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [ServiceNow SAML Onboarding](../ServiceNow/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [GitHub Enterprise Onboarding](../GitHub-Enterprise/README.md)
- [Custom OIDC Application](../Custom-OIDC-App/README.md)
- [SCIM Provisioning](../SCIM-Provisioning/README.md)

---
# APP-1001 — OmniVerse Grafana Onboarding

## Overview

This application onboarding package documents the integration of **OmniVerse Grafana** with Microsoft Entra ID using SAML 2.0.

The goal was to centralize authentication, reduce local account dependency, and prepare Grafana for group-based access control using Microsoft Entra security groups.

---

## Business Request

The Infrastructure Operations team requested SSO for Grafana so users could authenticate with their enterprise identity instead of separate local credentials.

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Application | OmniVerse Grafana |
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | Grafana Cloud |
| Provisioning | Manual |
| Access Model | Group-based RBAC prepared |
| Status | SAML configured and enabled |

---

## Step 1 — Create Enterprise Application

A non-gallery Enterprise Application was created in Microsoft Entra ID for OmniVerse Grafana. This establishes the application object that Entra uses to manage SSO, claims, certificates, and access assignment.

![Application Overview](screenshots/01-Application-Overview.png)

**Result**

The Enterprise Application was created and prepared for SAML configuration.

---

## Step 2 — Open SAML Configuration

The SAML configuration page was opened before any values were entered. This documents the starting point of the application onboarding process.

![Blank SAML Configuration](screenshots/02-SAML-Configuration-Blank.png)

**Result**

The application was ready for SAML setup.

---

## Step 3 — Review Basic SAML Configuration

The Basic SAML Configuration panel contains the Service Provider values required by Microsoft Entra ID, including the Entity ID and Assertion Consumer Service URL.

![Basic SAML Configuration](screenshots/03-Basic-SAML-Configuration-Blank.png)

**Result**

The required SAML fields were identified before configuration.

---

## Step 4 — Review Grafana SAML Settings

Grafana SAML settings were reviewed to identify the Service Provider metadata, ACS URL, and integration requirements.

![Grafana SAML General Settings](screenshots/04-Grafana-General-SAML-Settings.png)

**Result**

Grafana provided the Service Provider values required for Entra configuration.

---

## Step 5 — Review Request Signing

Grafana supports signed SAML requests. Request signing settings were reviewed as part of the trust relationship between Grafana and Microsoft Entra ID.

![Grafana Sign Requests](screenshots/05-Grafana-Sign-Requests.png)

**Result**

Request signing options were reviewed before continuing.

---

## Step 6 — Connect Grafana to Identity Provider

Grafana provided the metadata URL and ACS URL needed by Microsoft Entra ID. These values define how Entra identifies Grafana and where SAML responses are sent.

![Grafana Connect Identity Provider](screenshots/06-Grafana-Connect-Identity-Provider.png)

**Result**

The Grafana Service Provider endpoints were captured for Entra configuration.

---

## Step 7 — Configure Entra Basic SAML Settings

Microsoft Entra ID was configured with Grafana's Entity ID, Reply URL, and Sign-on URL.

![Entra Basic SAML Configuration](screenshots/07-Entra-Basic-SAML-Configuration.png)

**Result**

The SAML trust was established from Microsoft Entra ID to Grafana.

---

## Step 8 — Review Default Attributes and Claims

Default SAML claims were reviewed to confirm what identity attributes Microsoft Entra ID would send to Grafana.

![Default Attributes and Claims](screenshots/08-Default-Attributes-Claims.png)

**Result**

The default claim set was reviewed before adding authorization-related claims.

---

## Step 9 — Review Advanced Claims

Advanced claim options were reviewed to determine how Grafana would receive user identity attributes and future authorization data.

![Advanced SAML Claims](screenshots/09-Advanced-SAML-Claims.png)

**Result**

Claim configuration options were validated before adding group claims.

---

## Step 10 — Add Group Claim

A group claim was added so Microsoft Entra ID can send group membership inside the SAML assertion. This prepares Grafana for future RBAC mapping.

![Group Claim Added](screenshots/11-Group-Claim-Added.png)

**Result**

Grafana can receive group membership data from Microsoft Entra ID.

---

## Step 11 — Review Certificate and Metadata

The SAML certificate and federation metadata were reviewed. Federation metadata allows Grafana to trust Microsoft Entra ID as the Identity Provider.

![SAML Certificate Metadata](screenshots/12-SAML-Certificate-Metadata.png)

**Result**

The Identity Provider metadata source was identified.

---

## Step 12 — Configure Grafana IdP Metadata

Grafana was configured with the Microsoft Entra App Federation Metadata URL. This corrected an earlier issue where the Entra portal URL was entered instead of the real metadata endpoint.

![Grafana IdP Metadata](screenshots/13-Grafana-Identity-Provider-Metadata.png)

**Result**

Grafana accepted the correct Identity Provider metadata.

---

## Step 13 — Configure User Mapping

Grafana user mapping was configured so SAML claims from Microsoft Entra ID could map to Grafana user fields.

| Grafana Field | Entra Claim |
|---|---|
| Name | `name` |
| Login | `NameID` |
| Email | `mail` |
| Groups | `groups` |

![Grafana User Mapping](screenshots/14-Grafana-User-Mapping.png)

**Result**

Grafana can map authenticated Entra users to Grafana identities.

---

## Step 14 — Enable SAML

After metadata, claims, and user mappings were configured, SAML was enabled in Grafana.

![SAML Enabled](screenshots/15-SAML-Configuration-Enabled.png)

**Result**

The Grafana SAML provider was enabled.

---

## Step 15 — Ready for Authentication Testing

The SAML configuration was completed and is ready for user assignment and authentication testing.

![SAML Ready](screenshots/16-SAML-Configuration-Ready.png)

**Result**

OmniVerse Grafana is configured for Microsoft Entra SAML authentication.

---

## Troubleshooting Highlight

During configuration, Grafana displayed:

`Failed to update provider settings`

The issue was caused by entering the Microsoft Entra portal URL instead of the **App Federation Metadata URL**.

**Resolution**

The correct federation metadata URL was copied from the Microsoft Entra SAML Certificates section and entered into Grafana.

---

## Outcome

The Grafana SAML integration was configured and enabled using Microsoft Entra ID as the Identity Provider. The application is ready for user assignment, login testing, and future RBAC role mapping.


