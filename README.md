# Enterprise Application Onboarding & SSO

## Overview

This repository documents enterprise application onboarding into Microsoft Entra ID using SAML, OpenID Connect, OAuth 2.0, and SCIM provisioning concepts.

The project is designed as an enterprise-style application onboarding portfolio. Each application package documents the business request, protocol selection, configuration requirements, validation results, troubleshooting, screenshots, and engineering takeaways.

---

## Business Scenario

OmniVerse Enterprise is centralizing authentication for business applications through Microsoft Entra ID.

The IAM team is responsible for onboarding applications into the identity platform using the appropriate SSO protocol, assigning access through groups, validating authentication flows, documenting troubleshooting, and preparing each application for production handoff.

---

## Application Packages

| App | Protocol | Status | Guide |
|---|---|---|---|
| Grafana | SAML | Complete | [Setup Guide](apps/Grafana/README.md) |
| WordPress | OIDC | Complete | [Setup Guide](apps/WordPress/README.md) |
| ServiceNow | SAML | Planned | [Setup Guide](apps/ServiceNow/README.md) |
| Salesforce | SAML | Planned | [Setup Guide](apps/Salesforce/README.md) |
| GitHub Enterprise | SAML/OIDC | Planned | [Setup Guide](apps/GitHub-Enterprise/README.md) |
| Custom OIDC App | OIDC | Planned | [Setup Guide](apps/Custom-OIDC-App/README.md) |
| SCIM Provisioning | SCIM | Planned | [Setup Guide](apps/SCIM-Provisioning/README.md) |

---

## Standard Onboarding Workflow

```text
Business Request
        |
        v
Application Intake
        |
        v
Protocol Selection
        |
        v
Identity Provider Configuration
        |
        v
Application Configuration
        |
        v
Claims / Attribute Mapping
        |
        v
User or Group Assignment
        |
        v
Validation and Sign-in Logs
        |
        v
Troubleshooting
        |
        v
Production Handoff
```

---

## Skills Demonstrated

- Enterprise application onboarding
- Microsoft Entra ID Enterprise Applications
- Microsoft Entra ID App Registrations
- SAML 2.0
- OpenID Connect
- OAuth 2.0
- SCIM provisioning concepts
- Claims mapping
- Attribute mapping
- Group assignment
- Client secrets
- Redirect URIs
- Token validation
- SSO troubleshooting
- Application owner handoff documentation

---

## Business Outcome

This project demonstrates a repeatable process for onboarding enterprise applications into a centralized identity platform.

The completed packages show how an IAM engineer evaluates an application, selects the correct authentication protocol, configures Microsoft Entra ID, validates authentication, troubleshoots failures, and documents the integration for operational support.

---

Created by **Keshawn Lynch**
