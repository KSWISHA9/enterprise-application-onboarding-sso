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
# APP-1002 — WordPress Application Onboarding

## 1. Business Request

The Digital Services team requested Single Sign-On for WordPress to centralize authentication through Microsoft Entra ID and reduce local WordPress credential management.

---

## 2. Authentication Protocol

| Area | Configuration |
|---|---|
| Protocol | OpenID Connect |
| Identity Provider | Microsoft Entra ID |
| Service Provider | WordPress |
| Authentication Flow | OAuth 2.0 / OIDC |
| Plugin | miniOrange OAuth Single Sign-On |

---

## 3. Provisioning Method

| Area | Configuration |
|---|---|
| Provisioning Method | Manual |
| SCIM | Not configured |
| Future State | JIT or SCIM provisioning |

---

## 4. Groups / RBAC

WordPress access was manually validated for this onboarding. Future state would include group-based access and role mapping.

| Group | Purpose |
|---|---|
| WordPress-Admins | Site administration |
| WordPress-Editors | Content publishing |
| WordPress-Readers | Read-only access |

---

## 5. Claims / Attributes

| Claim | Purpose |
|---|---|
| preferred_username | Username mapping |
| email | Email mapping |
| name | Display name mapping |
| oid | Entra object identifier |
| tid | Tenant identifier |

---

## 6. Configuration Steps

1. Built a local WordPress environment using LocalWP.
2. Installed the miniOrange OAuth/OpenID Connect plugin.
3. Created a Microsoft Entra App Registration.
4. Generated a client secret.
5. Configured OIDC endpoints in WordPress.
6. Updated WordPress from HTTP to HTTPS so the callback URL matched Entra requirements.
7. Tested token issuance and JWT validation.
8. Configured attribute mapping.
9. Validated successful access to the WordPress dashboard.

---

## 7. Validation

- Entra ID issued a valid identity token.
- WordPress accepted the OIDC response.
- JWT claims returned correctly.
- Attribute mapping completed successfully.
- User reached the WordPress dashboard after authentication.

---

## 8. Troubleshooting

### Issue 1 — HTTP Callback URL

The plugin originally generated an HTTP callback URL. WordPress Address and Site Address were updated to HTTPS.

### Issue 2 — Invalid Client Secret

Authentication failed with AADSTS7000215 because the Secret ID was used instead of the Secret Value. A new secret was generated and configured.

---

## 9. Operational Handoff

| Area | Owner |
|---|---|
| Application Owner | Digital Services |
| Identity Owner | IAM Team |
| Authentication | OpenID Connect |
| Provisioning | Manual |
| Future Work | RBAC and automated provisioning |

---

## 10. Screenshots

### 1. LocalWP Site Created

Shows the local WordPress environment used for the application onboarding.

![LocalWP Site Created](screenshots/04-localwp-site-created.png)

---
### 2. WordPress Administrator Dashboard

Confirms WordPress was deployed and accessible before SSO configuration.

![WordPress Administrator Dashboard](screenshots/05-wordpress-admin-dashboard.png)

---
### 3. OIDC Plugin Search

Shows discovery of the miniOrange OAuth/OpenID Connect plugin.

![OIDC Plugin Search](screenshots/06-oidc-plugin-search.png)

---
### 4. miniOrange Plugin Installed

Confirms the OIDC plugin was installed and activated.

![miniOrange Plugin Installed](screenshots/07-miniorange-oidc-plugin-installed.png)

---
### 5. Client Secret Created

Shows the Microsoft Entra client secret creation step used by the OIDC application.

![Client Secret Created](screenshots/10-client-secret-created.png)

---
### 6. OIDC Configuration

Shows initial WordPress OIDC configuration values.

![OIDC Configuration](screenshots/11-wordpress-oidc-configuration.png)

---
### 7. Completed OIDC Configuration

Shows completed endpoint and credential configuration.

![Completed OIDC Configuration](screenshots/12-wordpress-oidc-configured.png)

---
### 8. Successful Token Validation

Shows successful JWT token validation after authentication.

![Successful Token Validation](screenshots/13-successful-oidc-token-validation.png)

---
### 9. Attribute Mapping

Shows claim mapping from Entra ID to WordPress attributes.

![Attribute Mapping](screenshots/14-attribute-mapping.png)

---
### 10. Invalid Client Secret Error

Documents the real troubleshooting issue encountered during testing.

![Invalid Client Secret Error](screenshots/15-invalid-client-secret-error.png)

---
### 11. Successful Dashboard Access

Confirms successful access to WordPress after OIDC authentication.

![Successful Dashboard Access](screenshots/18-wordpress-dashboard-after-sso.png)

---

## Engineering Takeaways

This onboarding demonstrated OIDC application registration, redirect URI handling, client secret management, JWT validation, attribute mapping, and real-world troubleshooting.
