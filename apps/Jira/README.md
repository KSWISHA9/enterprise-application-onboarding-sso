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
# APP-1005 — Atlassian Jira Cloud Application Onboarding

## 1. Business Request

The Engineering and Project Management teams requested SSO for Jira Cloud to centralize authentication, reduce local credential dependency, and align Atlassian access with Microsoft Entra ID.

---

## 2. Authentication Protocol

| Area | Configuration |
|---|---|
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | Atlassian Cloud |
| Platform | Atlassian Guard |
| Certificate | Microsoft Entra token signing certificate |

---

## 3. Provisioning Method

| Area | Configuration |
|---|---|
| Provisioning Method | Manual |
| SCIM | Not configured in this phase |
| Future State | SCIM provisioning and group synchronization |

---

## 4. Groups / RBAC

Jira authorization is managed through Atlassian groups and project permissions. This phase focused on authentication only.

| Group | Purpose |
|---|---|
| Jira-Admins | Jira administration |
| Jira-Developers | Project contributor access |
| Jira-Viewers | Read-only access |
| Jira-ServiceDesk | Service desk users |

---

## 5. Claims / Attributes

| Claim | Source |
|---|---|
| NameID | user.userprincipalname |
| emailaddress | user.mail |
| givenname | user.givenname |
| surname | user.surname |

---

## 6. Configuration Steps

1. Created the Jira / Atlassian Cloud environment.
2. Started Atlassian Guard SAML setup.
3. Created the Atlassian Cloud Enterprise Application in Microsoft Entra ID.
4. Copied Microsoft Entra IdP values into Atlassian.
5. Imported the Microsoft Entra X.509 certificate.
6. Copied Atlassian SP Entity ID and ACS URL into Entra.
7. Saved the SAML configuration.
8. Tested SSO.
9. Validated successful access to Atlassian Cloud.

---

## 7. Validation

- Atlassian accepted the Microsoft Entra IdP configuration.
- Entra accepted the Atlassian SP Entity ID and ACS URL.
- Atlassian completed SAML setup.
- User successfully accessed Atlassian after SAML login.

---

## 8. Troubleshooting

### Issue 1 — Initial Login Retry Required

The first SAML login attempt displayed a temporary Atlassian login issue. Retrying the login completed successfully. This was documented as likely session state or propagation behavior immediately after enabling SAML.

---

## 9. Operational Handoff

| Area | Owner |
|---|---|
| Application Owner | Engineering / Project Management |
| Identity Owner | IAM Team |
| Authentication | SAML 2.0 |
| Provisioning | Manual |
| Future Work | SCIM and authentication policy enforcement |

---

## 10. Screenshots

### 1. Jira Home

Shows the Atlassian / Jira environment used for onboarding.

![Jira Home](screenshots/01-jira-home.png)

---
### 2. Atlassian Cloud Gallery App

Shows Atlassian Cloud selected from Microsoft Entra.

![Atlassian Cloud Gallery App](screenshots/02-jira-gallery-app.png)

---
### 3. SAML Setup Start

Shows Atlassian Guard SAML setup start.

![SAML Setup Start](screenshots/03-jira-saml-setup-start.png)

---
### 4. Identity Provider Configuration

Shows Microsoft Entra IdP values entered into Atlassian.

![Identity Provider Configuration](screenshots/04-jira-saml-configuration.png)

---
### 5. Entra SAML Settings

Shows Entra configured with Atlassian SAML values.

![Entra SAML Settings](screenshots/05-jira-entra-saml-settings.png)

---
### 6. Service Provider URLs

Shows Atlassian-generated SP Entity ID and ACS URL.

![Service Provider URLs](screenshots/06-jira-service-provider-urls.png)

---
### 7. SAML Configured

Shows Atlassian SAML setup completion.

![SAML Configured](screenshots/07-jira-saml-configured.png)

---
### 8. SSO Test

Shows the SSO test workflow.

![SSO Test](screenshots/08-jira-sso-test.png)

---
### 9. SSO Success

Shows successful access to Atlassian after SAML authentication.

![SSO Success](screenshots/09-jira-sso-success.png)

---

## Engineering Takeaways

This onboarding demonstrated Atlassian Guard SAML configuration, IdP/SP metadata exchange, X.509 certificate handling, ACS URL configuration, authentication testing, and troubleshooting.
