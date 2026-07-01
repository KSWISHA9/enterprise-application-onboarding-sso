# 02 - Enterprise Application Creation

## Objective

Create a new Enterprise Application named **OmniVerse Grafana** in Microsoft Entra ID to provide centralized authentication using SAML 2.0.

---

## Business Requirement

The Infrastructure Operations team requested that Grafana be integrated with Microsoft Entra ID to:

- Eliminate local application accounts
- Centralize authentication
- Enforce Multi-Factor Authentication (MFA)
- Enable group-based Role-Based Access Control (RBAC)
- Simplify user lifecycle management

---

## Configuration

| Setting | Value |
|---------|-------|
| Application Name | OmniVerse Grafana |
| Application Type | Non-gallery Enterprise Application |
| Identity Provider | Microsoft Entra ID |
| Authentication Protocol | SAML 2.0 |
| Provisioning | Manual (Phase 1) |

---

## Result

The enterprise application was successfully created and is ready for SAML configuration.

---

## Screenshot

![Application Overview](screenshots/01-Application-Overview.png)

---

## Engineering Notes

Creating a non-gallery enterprise application provides full control over SAML configuration, claims mapping, certificates, and access policies. This mirrors how many organizations onboard custom or internally hosted applications that are not available in the Microsoft Entra application gallery.
