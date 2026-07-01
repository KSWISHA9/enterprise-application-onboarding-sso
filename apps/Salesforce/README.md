## Enterprise Application Packages

- [Repository Home](../../README.md)
- [Grafana SAML Onboarding](../Grafana/README.md)
- [WordPress OIDC Onboarding](../WordPress/README.md)
- [GitHub Enterprise SAML Onboarding](../GitHub-Enterprise/README.md)
- [Atlassian Jira SAML Onboarding](../Jira/README.md)
- [Cisco Duo Identity Integration](../Cisco-Duo/README.md)
- [Keycloak SAML Federation](../Keycloak/README.md)
- [SCIM Provisioning](../SCIM-Provisioning/README.md)

---


# APP-1004 - Salesforce SAML Onboarding

## Business Request

The Sales Operations team requested Single Sign-On for Salesforce to reduce local credential management, improve authentication security, and align Salesforce access with Microsoft Entra ID.

---

## Implementation Summary

| Area | Configuration |
|---|---|
| Application | Salesforce |
| Protocol | SAML 2.0 |
| Identity Provider | Microsoft Entra ID |
| Service Provider | Salesforce |
| Authentication Flow | IdP-Initiated SAML |
| Certificate | Microsoft Entra token signing certificate |
| Provisioning | Manual |
| Status | Successfully Configured |

---

## Architecture

```mermaid
flowchart LR
    A[Sales User] --> B[Microsoft Entra ID]
    B --> C[SAML Assertion]
    C --> D[Salesforce ACS URL]
    D --> E[Salesforce Dashboard]
```

---

## Configuration Steps

1. Created a Salesforce Developer Edition environment.
2. Confirmed Salesforce My Domain was deployed.
3. Retrieved the Salesforce Organization ID from Company Information.
4. Created the Salesforce Enterprise Application in Microsoft Entra ID.
5. Configured Entity ID, Reply URL, and Sign-on URL.
6. Downloaded the Microsoft Entra SAML certificate.
7. Configured Salesforce SAML Single Sign-On settings.
8. Uploaded the Entra certificate into Salesforce.
9. Tested SSO from Microsoft Entra ID.
10. Validated successful Salesforce access.

---

## Claims and Attribute Mapping

| Claim | Value |
|---|---|
| NameID | Salesforce username or Federation ID |
| user.userprincipalname | Primary user identifier |
| user.mail | Email address |
| givenname | First name |
| surname | Last name |

---

## Validation

- Entra accepted the Salesforce SAML configuration.
- Salesforce accepted the IdP certificate and login URL.
- SSO test completed successfully from Microsoft Entra ID.
- User landed in Salesforce without using local credentials.

---

## Screenshots

### 1. Salesforce Home
Shows the Salesforce Developer Edition environment used for onboarding.
![Salesforce Home](../../screenshots/01-salesforce-home.png)

### 2. Salesforce SSO Settings
Shows the Salesforce Single Sign-On Settings page.
![SSO Settings](../../screenshots/02-salesforce-sso-settings.png)

### 3. Salesforce Gallery App
Shows the Salesforce Enterprise Application selected from the Entra gallery.
![Gallery App](../../screenshots/03-salesforce-gallery-app.png)

### 4. Basic SAML Configuration
Shows the Entity ID, Reply URL, and Sign-on URL configured in Entra.
![Basic SAML](../../screenshots/04-salesforce-basic-saml.png)

### 5. Salesforce SAML Settings
Shows the Salesforce-side SAML configuration.
![SAML Settings](../../screenshots/05-salesforce-saml-settings.png)

### 6. SAML Configured
Confirms the Salesforce SAML configuration was saved successfully.
![Configured](../../screenshots/06-salesforce-saml-configured.png)

### 7. SAML Test
Shows the Microsoft Entra SAML test workflow.
![SAML Test](../../screenshots/07-salesforce-saml-test.png)

### 8. SSO Success
Confirms successful login to Salesforce after SAML authentication.
![Success](../../screenshots/08-salesforce-sso-success.png)

---

## Troubleshooting

### Issue 1 - Reply URL Format
Entra rejected the Reply URL until a forward slash was added before the query parameter. Correct format: `https://orgfarm.develop.my.salesforce.com/?so=<OrgID>`

### Issue 2 - Salesforce Organization ID Required
The Salesforce ACS URL requires the Organization ID from Setup > Company Information.

---

## Engineering Takeaways

This onboarding demonstrated Salesforce My Domain configuration, ACS URL construction, SAML certificate exchange, identity mapping, and successful Entra-to-Salesforce SSO validation.

---

## Future Enhancements

- SCIM provisioning and Federation ID mapping
- Conditional Access policy integration
- Access reviews for Salesforce profiles
