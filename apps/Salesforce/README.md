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
# APP-1004 — Salesforce Application Onboarding

## 1. Business Request

The Sales Operations team requested Single Sign-On for Salesforce to reduce local credential management, improve security, and align Salesforce access with Microsoft Entra ID.

---

## 2. Authentication Protocol

| Area | Configuration |
|---|---|
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | Salesforce |
| Authentication Flow | IdP-Initiated SAML |
| Certificate | Microsoft Entra token signing certificate |

---

## 3. Provisioning Method

| Area | Configuration |
|---|---|
| Provisioning Method | Manual |
| SCIM | Not configured |
| Future State | Automated provisioning and Federation ID mapping |

---

## 4. Groups / RBAC

Salesforce access was manually validated in this phase. Future state would use Entra groups for assignment and Salesforce profiles/permission sets for authorization.

| Group | Purpose |
|---|---|
| Salesforce-Admins | Salesforce administrators |
| Salesforce-SalesOps | Sales operations users |
| Salesforce-ReadOnly | Read-only reporting users |

---

## 5. Claims / Attributes

| Attribute | Purpose |
|---|---|
| NameID | Salesforce username or Federation ID |
| user.userprincipalname | Primary user identifier |
| user.mail | Email address |
| givenname | First name |
| surname | Last name |

---

## 6. Configuration Steps

1. Created a Salesforce Developer Edition environment.
2. Confirmed Salesforce My Domain was deployed.
3. Retrieved the Salesforce Organization ID.
4. Created the Salesforce Enterprise Application in Microsoft Entra ID.
5. Configured Entity ID, Reply URL, and Sign-on URL.
6. Downloaded the Microsoft Entra SAML certificate.
7. Configured Salesforce SAML Single Sign-On settings.
8. Uploaded the Entra certificate into Salesforce.
9. Tested SSO from Microsoft Entra ID.
10. Validated successful Salesforce access.

---

## 7. Validation

- Entra accepted the Salesforce SAML configuration.
- Salesforce accepted the IdP certificate and login URL.
- SSO test completed from Microsoft Entra ID.
- User landed successfully in Salesforce.

---

## 8. Troubleshooting

### Issue 1 — Reply URL Format

Microsoft Entra rejected the Reply URL until a slash was added before the query parameter.

Correct format:

``text
https://orgfarm-f3028ef358-dev-ed.develop.my.salesforce.com/?so=00Dfj00000T4EJp
``

### Issue 2 — Salesforce Organization ID Required

The Salesforce ACS URL required the Salesforce Organization ID from Company Information.

---

## 9. Operational Handoff

| Area | Owner |
|---|---|
| Application Owner | Sales Operations |
| Identity Owner | IAM Team |
| Authentication | SAML 2.0 |
| Provisioning | Manual |
| Future Work | SCIM, Federation ID, Conditional Access |

---

## 10. Screenshots

### 1. Salesforce Home

Shows the Salesforce Developer Edition environment.

![Salesforce Home](screenshots/01-salesforce-home.png)

---
### 2. Salesforce SSO Settings

Shows the Salesforce Single Sign-On Settings page.

![Salesforce SSO Settings](screenshots/02-salesforce-sso-settings.png)

---
### 3. Salesforce Gallery Application

Shows the Salesforce Enterprise Application in the Entra gallery.

![Salesforce Gallery Application](screenshots/03-salesforce-gallery-app.png)

---
### 4. Basic SAML Configuration

Shows the Entra Basic SAML Configuration for Salesforce.

![Basic SAML Configuration](screenshots/04-salesforce-basic-saml.png)

---
### 5. Salesforce SAML Settings

Shows the Salesforce-side SAML configuration.

![Salesforce SAML Settings](screenshots/05-salesforce-saml-settings.png)

---
### 6. SAML Configured

Shows Salesforce SAML configuration saved successfully.

![SAML Configured](screenshots/06-salesforce-saml-configured.png)

---
### 7. SAML Test

Shows the Entra SAML test workflow.

![SAML Test](screenshots/07-salesforce-saml-test.png)

---
### 8. SSO Success

Shows successful access to Salesforce after SAML authentication.

![SSO Success](screenshots/08-salesforce-sso-success.png)

---

## Engineering Takeaways

This onboarding demonstrated Salesforce My Domain, ACS URL construction, certificate exchange, SAML identity mapping, and successful Entra-to-Salesforce SSO validation.
