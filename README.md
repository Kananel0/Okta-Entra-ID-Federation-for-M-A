# Okta–Entra ID Federation for M&A
# Okta–Entra ID Federation for M&A / Multi-Cloud Identity
### Cross-IdP Federation | SCIM Provisioning | Zero Trust Policy Parity

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Platforms](https://img.shields.io/badge/platforms-Okta%20%7C%20Microsoft%20Entra%20ID-blue)
![Scenario](https://img.shields.io/badge/scenario-M%26A%20Integration-yellow)



---

## 📌 What This Project Is

This project simulates one of the most common real-world identity challenges: a **merger or acquisition** where the parent company runs Microsoft Entra ID and the acquired subsidiary runs **Okta** — two different identity providers that now need to work together without ripping either one out.

The project builds:

- **Cross-IdP federation** (SAML/OIDC) so subsidiary users can SSO into parent-company applications, and vice versa
- **SCIM-based provisioning/deprovisioning** synchronizing user lifecycle events between Okta Universal Directory and Entra ID
- **Zero Trust policy parity** — mapping Okta Network Zones to Entra ID Named Locations so access policy stays consistent regardless of which IdP a user authenticates through
- A unified **MFA and device trust** policy translated across both platforms
- **Delegated administration boundaries**, so each entity keeps local admin control without breaking central security governance

## 🎯 Why I Built This

Almost every identity candidate learns one platform in isolation. But real enterprises — especially ones going through M&A activity — end up running **two identity providers side by side**, sometimes for years, and someone has to make sure security policy doesn't have a gap between them.

I built this project to demonstrate that I can:
- Operate across multi-vendor identity ecosystems, not just a single platform
- Design federation that's secure by default rather than "SSO now, fix security later"
- Translate one platform's security controls into another's so there's no policy blind spot at the seam between the two companies
- Support real M&A / multi-cloud identity scenarios that come up constantly in enterprise IT

## 🛡️ How This Protects the Organization

| Risk | Control Implemented | Outcome |
|---|---|---|
| Subsidiary users create duplicate/shadow accounts to access parent apps | SAML/OIDC federation | Users authenticate once through their home IdP, no duplicate credentials |
| A terminated employee in one system keeps access in the other | SCIM provisioning/deprovisioning sync | Leaver events propagate across both platforms automatically |
| Security policy is strong in Entra ID but weak (or different) in Okta | Named Locations ↔ Network Zones policy parity | Consistent risk-based access enforcement regardless of entry point |
| Inconsistent MFA requirements create an easy attack path through the "weaker" IdP | Unified MFA/device trust policy | Attackers can't bypass strong controls by targeting the less-mature platform |
| Central security team loses visibility once a subsidiary is acquired | Delegated admin boundaries with central oversight | Local teams keep operational control; security governance stays centralized |

## 🏗️ Architecture

```
   Subsidiary Users                     Parent Company Users
        │                                       │
        ▼                                       ▼
      Okta                                Microsoft Entra ID
   (Universal Directory)                  (Cloud Identity)
        │                                       │
        └──────────── SAML / OIDC Federation ───┘
        │                                       │
        └──────────────── SCIM Sync ────────────┘
        │                                       │
   Network Zones  ───── Policy Parity ─────  Named Locations
```

## 📂 Repository Structure

```
├── architecture/
│   └── federation-diagram.png
├── federation/
│   ├── saml-oidc-config.md
│   └── scim-attribute-mapping.md
├── policy-parity/
│   └── okta-vs-entra-control-comparison.md
├── screenshots/
└── README.md
```

## 🧰 Skills Demonstrated

`Okta Universal Directory` · `Microsoft Entra ID` · `SAML/OIDC Federation` · `SCIM Provisioning` · `Network Zones` · `Named Locations` · `Delegated Administration` · `Multi-Cloud Identity` · `Zero Trust`

## 🔗 Related Certification

This project was built as part of my preparation for **Microsoft SC-300: Identity and Access Administrator**.

---
📩 Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/kananelo-mohale/) if you'd like to discuss the design decisions behind this project.
