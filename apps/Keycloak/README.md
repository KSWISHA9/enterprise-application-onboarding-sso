## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [GitHub Enterprise SAML Onboarding](../GitHub-Enterprise/README.md)
- [Salesforce SAML Onboarding](../Salesforce/README.md)
- [Atlassian Jira SAML Onboarding](../Jira/README.md)
- [Cisco Duo Identity Integration](../Cisco-Duo/README.md)

---

# APP-1007 - Keycloak SAML Federation with Microsoft Entra ID

## Overview

This onboarding package documents the integration of Keycloak with Microsoft Entra ID using SAML 2.0 identity federation.

Unlike standard enterprise SaaS onboarding, this project demonstrates a more advanced IAM engineering pattern: configuring an open-source identity platform as a SAML Service Provider that trusts Microsoft Entra ID as an external Identity Provider.

This is the same federation pattern used in enterprise environments where organizations run self-hosted identity platforms alongside cloud identity providers.

---

## Business Request

The platform engineering team requested Microsoft Entra ID federation with the OmniVerse Keycloak identity platform to allow centralized authentication for internal applications managed through Keycloak, without requiring separate Keycloak credentials.

---

## Business Objectives

- Deploy Keycloak as a self-hosted identity platform
- Configure Microsoft Entra ID as an external SAML Identity Provider
- Establish SAML 2.0 trust between Entra ID and Keycloak
- Validate federated authentication end-to-end
- Document the Identity Provider brokering pattern

---

## Architecture

```text
User
  |
  v
Keycloak Login Page (omniverse realm)
  |
  v
Redirect to Microsoft Entra ID
  |
  v
Microsoft Entra ID authenticates user (SAML IdP)
  |
  v
SAML Assertion returned to Keycloak broker endpoint
  |
  v
Keycloak validates assertion and creates federated session
  |
  v
User lands in Keycloak account console
```

---

## Environment

| Component | Value |
|---|---|
| Keycloak Version | 26.6.4 |
| Deployment | Docker (quay.io/keycloak/keycloak:latest) |
| Realm | omniverse |
| Identity Provider | Microsoft Entra ID |
| Protocol | SAML 2.0 |
| Federation Pattern | Identity Provider Brokering |
| Keycloak Role | Identity Broker (SAML SP to Microsoft Entra ID) |
| Entra Role | Identity Provider (IdP) |

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Protocol | SAML 2.0 |
| Keycloak Deployment | Docker start-dev |
| Realm | omniverse |
| Identity Provider Alias | microsoft-entra |
| Entra Entity ID | https://sts.windows.net/427c9654-7012-4c8c-be66-268eb6b12f32/ |
| Keycloak ACS URL | http://localhost:8080/realms/omniverse/broker/microsoft-entra/endpoint |
| NameID Format | email |
| Provisioning | Just-in-Time via first broker login flow |
| Status | Successfully Configured |

---

## Key Engineering Decision - Identity Provider Brokering

Initial attempts configured Keycloak as a direct SAML SP using a custom client. This approach failed because Keycloak SAML clients are designed for Keycloak acting as an IdP for downstream applications, not for receiving assertions from an upstream IdP.

The correct pattern is Keycloak Identity Provider Brokering, which provides a dedicated broker endpoint per IdP and handles the full SAML request and response lifecycle automatically.

The broker endpoint URL format is:

```text
http://<keycloak-host>/realms/<realm>/broker/<idp-alias>/endpoint
```

---

## SAML Configuration

### Microsoft Entra ID

| Setting | Value |
|---|---|
| Identifier (Entity ID) | https://sts.windows.net/427c9654-7012-4c8c-be66-268eb6b12f32/ |
| Reply URL (ACS) | http://localhost:8080/realms/omniverse/broker/microsoft-entra/endpoint |
| NameID Format | emailAddress |

### Keycloak Identity Provider

| Setting | Value |
|---|---|
| Alias | microsoft-entra |
| Display Name | Microsoft Entra ID |
| SSO URL | https://login.microsoftonline.com/427c9654-7012-4c8c-be66-268eb6b12f32/saml2 |
| Entity ID | https://sts.windows.net/427c9654-7012-4c8c-be66-268eb6b12f32/ |
| NameID Format | email |
| Post Binding Response | true |
| Post Binding AuthnRequest | true |
| Validate Signature | true |

---

## Implementation Steps

1. Deployed Keycloak 26.6.4 via Docker with environment variable admin credentials.
2. Created the omniverse realm via kcadm CLI.
3. Created the OmniVerse Keycloak Enterprise Application in Microsoft Entra ID.
4. Configured Basic SAML settings in Entra using Keycloak broker endpoint values.
5. Downloaded Entra Federation Metadata XML.
6. Created the microsoft-entra Identity Provider in Keycloak via kcadm CLI.
7. Created a test user in the omniverse realm.
8. Triggered SP-initiated SSO via the Keycloak broker login URL.
9. Completed first broker login profile confirmation.
10. Validated successful federated authentication into the Keycloak account console.

---

## Validation

- Microsoft Entra ID accepted the SAML authentication request from Keycloak.
- Entra ID issued a valid SAML assertion.
- Keycloak received and validated the assertion at the broker endpoint.
- First broker login flow executed successfully.
- User profile created in the omniverse realm via JIT provisioning.
- User landed in the Keycloak account console as an authenticated federated identity.
- Linked accounts page confirmed Microsoft Entra ID as the linked login provider.

---

## Screenshots

### 1. Keycloak Admin Console

Shows the Keycloak 26.6.4 admin console after deployment via Docker.

![Keycloak Admin Console](../../screenshots/01-keycloak-admin-console.png.png)

---

### 2. OmniVerse Realm Created

Shows the omniverse realm created in Keycloak where the Microsoft Entra Identity Provider was configured.

![Realm Created](../../screenshots/02-keycloak-realm-created.png.png)

---

### 3. SAML Client Created

Shows the initial SAML client created in Keycloak during the first configuration attempt using the direct SP client pattern.

![Client Created](../../screenshots/03-keycloak-client-created.png.png)

---

### 4. SAML Client Settings

Shows the SAML client settings including Client ID, protocol, and access configuration.

![Client Settings](../../screenshots/04-keycloak-client-saml-settings.png.png)

---

### 5. OmniVerse Keycloak Enterprise Application in Entra

Shows the OmniVerse Keycloak Enterprise Application created in Microsoft Entra ID for SAML federation, including the App Gallery selection using the non-gallery application option.

![Entra Enterprise App](../../screenshots/05-keycloak-entra-enterprise-application.png.png)

---

### 6. Blank SAML Configuration

Shows the initial SAML configuration state before Entity ID and Reply URL were configured in Microsoft Entra ID.

![Blank SAML Config](../../screenshots/06-keycloak-saml-configuration-blank.png.png)

---

### 7. Basic SAML Configuration

Shows the completed Basic SAML Configuration in Microsoft Entra ID with the Keycloak broker endpoint as the Reply URL.

![Basic SAML Config](../../screenshots/07-keycloak-basic-saml-configuration.png.png)

---

### 8. SAML Certificate

Shows the Microsoft Entra SAML signing certificate used to validate assertions sent to Keycloak.

![SAML Certificate](../../screenshots/09-keycloak-saml-certificate.png.png)

---

### 9. Metadata Import

Shows the Keycloak client configuration with the Entra App Federation Metadata URL imported for automatic IdP configuration.

![Metadata Import](../../screenshots/09-keycloak-metadata-import.png.png)

---

### 10. Keycloak IdP Metadata

Shows the Keycloak realm SAML metadata descriptor confirming the SSO endpoints and signing certificate.

![Keycloak IdP Metadata](../../screenshots/10-keycloak-idp-metadata.png.png)

---

### 11. Final SAML Configuration

Shows the final Keycloak client SAML configuration with the Entra metadata URL imported and signature settings confirmed.

![Final SAML Config](../../screenshots/10-keycloak-final-saml-configuration.png.png)

---

### 12. First Broker Login

Shows the Keycloak first broker login prompt where the user completes their profile after the initial SAML authentication from Microsoft Entra ID.

![First Broker Login](../../screenshots/09-Keycloak-First-Broker-Login.png.png)

---

### 13. Account Information Update

Shows the profile update confirmation after the first broker login flow completed successfully.

![Account Update](../../screenshots/10-Keycloak-Account-Information-Update.png.png)

---

### 14. Linked Identity Provider

Shows the Keycloak account console Linked Accounts page confirming Microsoft Entra ID is linked as the federated login provider for this user.

![Linked Provider](../../screenshots/11-Keycloak-Linked-Identity-Provider.png.png)

---

## Troubleshooting

### Issue 1 - Wrong Federation Pattern

**Problem:** Initial configuration used a Keycloak SAML client to receive Entra assertions directly. Keycloak returned `Invalid Request` and `Unknown saml response` errors.

**Root Cause:** Keycloak SAML clients are designed for Keycloak acting as an IdP, not for receiving upstream IdP assertions.

**Resolution:** Switched to Keycloak Identity Provider Brokering, which provides a dedicated broker endpoint and handles the full SAML lifecycle correctly.

---

### Issue 2 - Admin Password Unknown

**Problem:** Keycloak container admin password was unknown after the original container was replaced.

**Resolution:** Stopped and removed the existing container. Deployed a fresh container with known credentials via `KEYCLOAK_ADMIN` and `KEYCLOAK_ADMIN_PASSWORD` environment variables.

---

### Issue 3 - Reply URL Mismatch (AADSTS50011)

**Problem:** Entra returned a reply URL mismatch because Keycloak was sending the old SAML client ACS URL instead of the broker endpoint URL.

**Resolution:** Added both URLs to the Entra Reply URL configuration and used the broker login URL to trigger a clean SP-initiated flow.

---

### Issue 4 - Entity ID Mismatch (AADSTS700016)

**Problem:** Entra returned application not found because the Entity ID in the SAML request did not match any registered application.

**Resolution:** Updated the Entra Identifier to match the Keycloak broker SP metadata Entity ID exactly.

---

## Lessons Learned

Keycloak is primarily designed as an Identity Provider. When federating with an upstream IdP like Microsoft Entra ID, the correct pattern is Identity Provider Brokering, not a custom SAML client.

JIT provisioning through the first broker login flow is the standard Keycloak pattern for federating external identities. Users are created in the Keycloak realm on first login without requiring pre-provisioning.

---

## Operational Handoff

| Area | Owner |
|---|---|
| Keycloak Platform | Platform Engineering |
| Identity Provider | IAM Team |
| Entra Enterprise App | IAM Team |
| Authentication | SAML 2.0 Federation |
| Provisioning | JIT via first broker login |
| Future Work | SCIM provisioning, Conditional Access, production TLS |

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
| APP-1007 Keycloak | Current |
| IAM-004 Conditional Access and Zero Trust | Upcoming |

---

## Future Enhancements

- Configure SCIM provisioning from Entra to Keycloak
- Add group-to-role mapping from Entra claims to Keycloak roles
- Configure Conditional Access policies in Entra
- Deploy Keycloak behind HTTPS with a real domain
- Integrate downstream OIDC applications through Keycloak
- Connect to IAM-004 Conditional Access and Zero Trust

