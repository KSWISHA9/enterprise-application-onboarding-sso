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
# APP-1003 — GitHub Enterprise Cloud Application Onboarding

## 1. Business Request

The Development Engineering team requested Single Sign-On for GitHub Enterprise Cloud to centralize authentication, reduce standalone credentials, and protect enterprise repositories through Microsoft Entra ID.

---

## 2. Authentication Protocol

| Area | Configuration |
|---|---|
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | GitHub Enterprise Cloud |
| Authentication Flow | Enterprise SAML SSO |
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

GitHub Enterprise access can be controlled through organizations, teams, and repository permissions.

| Group | Purpose |
|---|---|
| GitHub-Enterprise-Admins | Enterprise administration |
| GitHub-Org-Owners | Organization ownership |
| GitHub-Developers | Repository contributor access |
| GitHub-Readers | Read-only repository access |

---

## 5. Claims / Attributes

| Claim | Source |
|---|---|
| givenname | user.givenname |
| surname | user.surname |
| emailaddress | user.mail |
| name | user.userprincipalname |
| NameID | user.userprincipalname |

---

## 6. Configuration Steps

1. Created a GitHub Enterprise Cloud trial.
2. Created the OmniVerse Enterprise GitHub organization.
3. Opened GitHub Enterprise authentication security settings.
4. Created the GitHub Enterprise Cloud Enterprise Application in Microsoft Entra ID.
5. Configured Basic SAML settings.
6. Downloaded the Microsoft Entra token signing certificate.
7. Entered Entra IdP values into GitHub Enterprise.
8. Tested SAML authentication.
9. Validated successful SAML identity authentication.

---

## 7. Validation

- GitHub redirected authentication to Microsoft Entra ID.
- Microsoft Entra ID authenticated the user.
- GitHub accepted the SAML assertion.
- GitHub displayed a successful SAML validation message.

---

## 8. Troubleshooting

### Issue 1 — Wrong GitHub Enterprise Application Type

The initial configuration used the wrong GitHub Enterprise app type. The configuration was corrected by aligning the Entra application with the GitHub Enterprise SAML configuration.

### Issue 2 — AADSTS650056 Misconfigured Application

The first test returned a misconfigured application error due to a mismatch between the application template and GitHub Enterprise SAML request. After selecting the correct app and updating SAML values, validation succeeded.

---

## 9. Operational Handoff

| Area | Owner |
|---|---|
| Application Owner | Development Engineering |
| Identity Owner | IAM Team |
| Authentication | SAML 2.0 |
| Provisioning | Manual |
| Future Work | SCIM, group sync, access reviews |

---

## 10. Screenshots

### 1. GitHub Enterprise Trial

Shows the GitHub Enterprise Cloud trial setup.

![GitHub Enterprise Trial](screenshots/01-github-enterprise-trial.png)

---
### 2. GitHub Organization Created

Shows the OmniVerse GitHub organization.

![GitHub Organization Created](screenshots/02-github-organization-created.png)

---
### 3. Authentication Security

Shows where enterprise authentication settings are managed.

![Authentication Security](screenshots/03-github-security-settings.png)

---
### 4. Microsoft Entra Gallery Application

Shows GitHub Enterprise Cloud selected from the Entra gallery.

![Microsoft Entra Gallery Application](screenshots/04-github-enterprise-gallery-application.png)

---
### 5. GitHub SAML Configuration

Shows the GitHub SAML configuration page where Entra IdP values were entered.

![GitHub SAML Configuration](screenshots/05-github-saml-configuration-page.png)

---
### 6. Basic SAML Configuration

Shows Entra Basic SAML settings configured for GitHub Enterprise.

![Basic SAML Configuration](screenshots/06-github-basic-saml-configuration.png)

---
### 7. SAML Authentication

Shows Microsoft Entra authentication during the GitHub SAML test.

![SAML Authentication](screenshots/07-github-saml-authentication.png)

---
### 8. Successful Validation

Shows GitHub successfully validating the SAML identity.

![Successful Validation](screenshots/08-github-saml-validation-success.png)

---

## Engineering Takeaways

This onboarding demonstrated enterprise-level SaaS federation, certificate trust, gallery application selection, SAML troubleshooting, and validation of a real GitHub Enterprise SAML integration.
