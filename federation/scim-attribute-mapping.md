# SCIM 2.0 User Provisioning & Attribute Mapping

To eliminate shadow accounts and ensure real-time deprovisioning during M&A transitions, SCIM 2.0 lifecycle synchronization is established between Okta Universal Directory and Microsoft Entra ID.

---

## 🔄 SCIM Provisioning Engine Configuration

* **Sync Direction:** Okta (Source of Truth for Subsidiary) $\longrightarrow$ Entra ID (Target / External B2B / Member Users).
* **Sync Interval:** Real-time push for Joiner/Leaver events via Webhooks; 40-minute scheduled delta sync.

---

## 📋 Attribute Mapping Schema

| Okta Source Attribute | SCIM 2.0 Core Attribute | Entra ID Target Attribute | Sync Action / Transformation |
|---|---|---|---|
| `user.id` | `externalId` | `onPremisesImmutableId` | **Matching Precedence 1** (Unique key) |
| `user.email` | `userName` | `userPrincipalName` | **Matching Precedence 2** |
| `user.firstName` | `name.givenName` | `givenName` | Create / Update |
| `user.lastName` | `name.familyName` | `surname` | Create / Update |
| `user.department` | `department` | `department` | Drives Dynamic Group Membership |
| `user.title` | `title` | `jobTitle` | Role-based provisioning trigger |
| `user.status` | `active` | `accountEnabled` | `ACTIVE` $\rightarrow$ `True`<br>`SUSPENDED/DEPROVISIONED` $\rightarrow$ `False` |

---

## ⚡ Deprovisioning & Offboarding Protocol
1. **Okta Suspend/Deprovision Event:** Admin or HR feed marks user as Terminated in Okta.
2. **SCIM Push:** Okta SCIM connector sends an HTTP `PATCH` payload setting `active: false` to Entra ID.
3. **Entra ID Actions Triggered:**
   * `accountEnabled` set to `False`.
   * Active HTTP sessions / OAuth Refresh Tokens invalidated immediately.
   * Entitlement Management access packages unassigned.

