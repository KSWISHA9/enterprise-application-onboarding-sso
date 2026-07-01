# Screenshots

## 1. LocalWP Site Created
Demonstrates deployment of a local WordPress environment used to simulate an enterprise application before integrating Microsoft Entra ID.

![LocalWP Site Created](../../screenshots/04-localwp-site-created.png)

---

## 2. WordPress Administrator Dashboard
Confirms successful installation of WordPress and administrative access prior to implementing Single Sign-On.

![WordPress Dashboard](../../screenshots/05-wordpress-admin-dashboard.png)

---

## 3. OAuth/OpenID Connect Plugin Search
Shows identification of the miniOrange OAuth/OpenID Connect client plugin used for enterprise authentication.

![Plugin Search](../../screenshots/06-oidc-plugin-search.png)

---

## 4. miniOrange Plugin Installed
Confirms installation and activation of the OAuth/OpenID Connect client responsible for communication with Microsoft Entra ID.

![Plugin Installed](../../screenshots/07-miniorange-oidc-plugin-installed.png)

---

## 5. Client Secret Created
Documents creation of a Microsoft Entra ID Client Secret used by WordPress during OAuth authentication.

![Client Secret](../../screenshots/10-client-secret-created.png)

---

## 6. Initial OIDC Configuration
Shows initial configuration of the OpenID Connect provider including Client ID, Client Secret, Callback URL, Authorization Endpoint, Token Endpoint, and Scopes.

![OIDC Configuration](../../screenshots/11-wordpress-oidc-configuration.png)

---

## 7. Completed OIDC Configuration
Demonstrates successful completion of all required OpenID Connect configuration settings.

![Completed Configuration](../../screenshots/12-wordpress-oidc-configured.png)

---

## 8. Successful Token Validation
Shows Microsoft Entra ID successfully issuing a JWT identity token containing authenticated user claims. This confirms the trust relationship between WordPress and Microsoft Entra ID was successfully established.

![Token Validation](../../screenshots/13-successful-oidc-token-validation.png)

---

## 9. Attribute Mapping
Illustrates mapping Microsoft Entra ID claims to WordPress username, email address, and display name to ensure accurate identity representation.

![Attribute Mapping](../../screenshots/14-attribute-mapping.png)

---

## 10. Authentication Troubleshooting
Captures the AADSTS7000215 Invalid Client Secret error encountered during testing and documents the troubleshooting process used to resolve the issue.

![Troubleshooting](../../screenshots/15-invalid-client-secret-error.png)

---

## 11. Successful WordPress Dashboard Login
Confirms successful authentication into WordPress using Microsoft Entra ID through OpenID Connect without requiring local WordPress credentials.

![Successful Login](../../screenshots/18-wordpress-dashboard-after-sso.png)
