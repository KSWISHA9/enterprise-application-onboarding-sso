# IAM-003 — Enterprise Application Onboarding & SSO

## Overview

This repository documents enterprise application onboarding into Microsoft Entra ID using SAML 2.0, OpenID Connect, OAuth 2.0, and SCIM provisioning concepts.

The goal of this project is to demonstrate a repeatable IAM application onboarding workflow across real enterprise SaaS and internal applications.

---

## Enterprise Application Onboarding Catalog

| Application | Protocol | Status | Guide |
|---|---|:---:|---|
| Grafana | SAML 2.0 | Complete | [Setup Guide](apps/Grafana/README.md) |
| WordPress | OIDC | Complete | [Setup Guide](apps/WordPress/README.md) |
| GitHub Enterprise Cloud | SAML 2.0 | Complete | [Setup Guide](apps/GitHub-Enterprise/README.md) |
| Salesforce | SAML 2.0 | Complete | [Setup Guide](apps/Salesforce/README.md) |
| Atlassian Jira Cloud | SAML 2.0 | Complete | [Setup Guide](apps/Jira/README.md) |
| ServiceNow | SAML 2.0 | Planned | [Setup Guide](apps/ServiceNow/README.md) |
| Slack | SAML 2.0 | Planned | [Setup Guide](apps/Slack/README.md) |
| Zoom | SAML 2.0 | Planned | [Setup Guide](apps/Zoom/README.md) |
| SCIM Provisioning | SCIM 2.0 | Planned | [Setup Guide](apps/SCIM-Provisioning/README.md) |

---

## Standard Onboarding Workflow

```text
Business Request
        |
        v
Authentication Protocol Selection
        |
        v
Provisioning Method Review
        |
        v
Groups / RBAC Planning
        |
        v
Claims / Attribute Mapping
        |
        v
Microsoft Entra ID Configuration
        |
        v
Application-Side Configuration
        |
        v
Validation and Sign-in Testing
        |
        v
Troubleshooting
        |
        v
Operational Handoff
```

---

## Skills Demonstrated

- Enterprise Application Onboarding
- Microsoft Entra ID Enterprise Applications
- Microsoft Entra ID App Registrations
- SAML 2.0 Federation
- OpenID Connect
- OAuth 2.0
- SCIM Provisioning Concepts
- Claims and Attribute Mapping
- Group Assignment Planning
- X.509 Certificate Handling
- Metadata Exchange
- SSO Validation
- Troubleshooting
- Operational Handoff Documentation

---

## Business Outcome

This repository demonstrates how an IAM engineer evaluates, configures, validates, troubleshoots, and documents application integrations with Microsoft Entra ID across multiple enterprise platforms.

Created by **Keshawn Lynch**
