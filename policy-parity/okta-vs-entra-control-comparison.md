# Zero Trust Policy Parity Framework (Okta vs. Entra ID)

To avoid security blind spots during an acquisition, access policies must maintain **structural parity** across both platforms.

---

## 🛡️ Control Comparison & Translation Matrix

| Security Domain | Okta Policy Engine | Entra ID Policy Engine | Policy Parity Objective |
|---|---|---|---|
| **Location-Based Risk** | **Network Zones**<br>*(IP / Geo / Dynamic proxy zones)* | **Named Locations**<br>*(Trusted IPs / Country Geo-Blocking)* | Ensure IP whitelist/blacklist parity across both IdPs. |
| **Step-Up Authentication** | **Okta Sign-On Policy / App Rules** | **Conditional Access Policies** | Require MFA for administrative or sensitive app access in both tools. |
| **Device Compliance** | **Okta Verify Device Trust / FastPass** | **Intune Device Compliance / CA Grants** | Permit sign-ins only from registered/compliant devices. |
| **Risk-Based Access** | **Okta Identity Threat Protection / Risk Engine** | **Entra ID Protection** *(User & Sign-In Risk)* | Automatically block high-risk logins regardless of entry point. |
| **Privileged Access** | **Okta Privileged Access (OPA)** | **Entra ID Privileged Identity Management (PIM)** | Enforce Just-In-Time (JIT) elevation for all admin roles. |

---

## 🗺️ Network Zone $\leftrightarrow$ Named Location Parity Mapping
Okta Network Zones                    Entra ID Named Locations
┌──────────────────────────────┐          ┌──────────────────────────────┐
│  Blocked Geo Zone            │  ──────► │  Blocked Countries Location  │
│  (High-Risk Foreign IPs)     │  Parity  │  (Geo-Block Policy Target)   │
└──────────────────────────────┘          └──────────────────────────────┘
┌──────────────────────────────┐          ┌──────────────────────────────┐
│  Corporate Network Zone      │  ──────► │  Trusted HQ Locations        │
│  (Egress Public IP Ranges)   │  Parity  │  (MFA Bypass / Location Tag) │
└──────────────────────────────┘          └──────────────────────────────┘


### 1. High-Risk Foreign IP Parity
* **Okta:** Defined under **Security $\rightarrow$ Networks $\rightarrow$ Dynamic Zone** (Blocking TOR exit nodes and untrusted regions).
* **Entra ID:** Configured in **Named Locations $\rightarrow$ Countries Location** (Mapped to a `[BLOCK] Geo-Location` Conditional Access Policy).

### 2. Device Trust Parity
* **Okta Configuration:** App access rule requires **Okta Verify with Device Health check**.
* **Entra ID Configuration:** Conditional Access requires **"Require device to be marked as compliant"** (Intune) or **"Require Hybrid Entra Joined Device"**.