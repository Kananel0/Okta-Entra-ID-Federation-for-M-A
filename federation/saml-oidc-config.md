# Cross-IdP Federation Configuration (Okta ↔ Microsoft Entra ID)

This document specifies the trust configuration enabling cross-organization Single Sign-On (SSO) between Okta (Subsidiary IdP) and Microsoft Entra ID (Parent IdP).

---

## 🔗 Federation Trust Architecture

* **Inbound Trust Model:** Okta is configured as an **External Identity Provider (Inbound SAML/WS-Fed)** inside Microsoft Entra ID.
* **Outbound Trust Model:** Entra ID enterprise applications are exposed to Okta users via **OIDC / OAuth 2.0 Web Applications**.

---

## 🛠️ Configuration Parameters

### 1. Entra ID Inbound Identity Provider Settings (Okta → Entra ID)
* **Issuer URI:** `https://subsidiary.okta.com`
* **Passive Authentication Endpoint:** `https://subsidiary.okta.com/app/office365/sso/saml`
* **Certificate:** Self-signed x509 Signing Certificate (2048-bit RSA, auto-rotated via Okta API)
* **Federated Domain:** `subsidiary-domain.com`
* **ImmutableID Mapping:** Mapped to Okta `user.id` or `externalId` to prevent collision during account merges.

### 2. SAML Token Claims Mapping

| Okta Claim Attribute | Entra ID Target Attribute | Description |
|---|---|---|
| `user.mail` | `userPrincipalName` / `mail` | Primary user identity identifier |
| `user.id` | `immutableId` | Unique, immutable identifier mapping |
| `user.firstName` | `givenName` | User's first name |
| `user.lastName` | `surname` | User's last name |
| `appuser.roles` | `roles` | Group/Role claims passed for RBAC in parent apps |

---

## 🔒 Security & Token Verification Controls
* **SAML Token Signing:** Response & Assertion signed using SHA-256.
* **Audience Restriction:** Hardened to accept requests only matching `urn:federation:MicrosoftOnline`.
* **Prompt Behavior:** Forces re-authentication for high-risk application sign-ins (`prompt=login`).