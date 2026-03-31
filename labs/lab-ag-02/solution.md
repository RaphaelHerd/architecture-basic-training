# ✅ Lab AG-02 — Solution: OAuth 2.0 & OpenID Connect Research

> 🗂️ Topic: API Gateway · Security &nbsp;|&nbsp; 📐 Artifact: Knowledge Summary &nbsp;|&nbsp; 🔒 Trainer Reference

---

## 🔐 Step 1 — OAuth 2.0 Concepts

### What problem does OAuth 2.0 solve?

Before OAuth, applications that needed access to a user's data on another service had to ask the user for their username and password and replay those credentials. This meant:

- The application had full access to everything — no way to limit scope
- The user could only revoke access by changing their password
- The third-party application stored credentials it should never have seen

OAuth 2.0 solves the **delegated authorisation problem** — a user can grant an application limited access to their data on another service, without sharing their credentials, and can revoke that access at any time independently.

---

### 👥 The Four OAuth 2.0 Roles

| Role | Definition | ShopFast Example |
|---|---|---|
| **Resource Owner** | The entity that owns the data being accessed — usually a human user | The ShopFast customer |
| **Client** | The application requesting access to the protected resource on behalf of the resource owner | ShopFast Web Frontend, Mobile App, Admin Tool |
| **Authorization Server** | Issues tokens after authenticating the resource owner and obtaining their consent | Identity Provider (e.g. Keycloak, Auth0, Okta) |
| **Protected Resource** | The API or service that holds the data the client wants to access | ShopFast microservices (Order Service, Catalog Service, etc.) |

---

### 🎟️ Token Types

| Token | Lifetime | Purpose | Opaque to Client? |
|---|---|---|---|
| **Access Token** | Short (minutes) | Presented to the protected resource to prove authorisation. The resource server validates it and uses its scopes to decide what the client may do. | Often no — JWTs are self-contained. Opaque tokens require introspection. |
| **Refresh Token** | Long (hours to days) | Used by the client to obtain a new access token from the Authorization Server when the current one expires — without involving the user again. | Yes — opaque, handled only by the Authorization Server. |

> **Key difference:** An access token is for calling APIs. A refresh token is for getting new access tokens. A refresh token must never be sent to an API.

---

### 🔀 Grant Types (Flows)

| Grant Type | When to Use | Key Characteristics |
|---|---|---|
| **Authorization Code** | Server-side web apps with a confidential client | Front channel for consent, back channel for token exchange. Most secure flow. Requires client secret. |
| **Authorization Code + PKCE** | Browser SPAs, mobile and native apps (public clients) | Same as Authorization Code but replaces client secret with a cryptographic PKCE challenge. Mandatory for public clients. |
| **Client Credentials** | Machine-to-machine / service-to-service with no user involved | Back channel only. Client authenticates with its own credentials. No resource owner. |
| **Device Code** | Devices with limited input capability (smart TVs, IoT devices) | User completes authentication on a secondary device (e.g. phone). |
| **Resource Owner Password** | Legacy trusted applications only — strongly discouraged | Client collects username and password directly. Avoid: reintroduces the credential-sharing anti-pattern. |
| **Implicit** | ⛔ Deprecated — do not use | Access token returned directly in the front channel. Replaced by Authorization Code + PKCE. |

---

### 🔒 PKCE — Proof Key for Code Exchange

PKCE (pronounced "pixy") is a security extension for the Authorization Code flow designed to protect **public clients** that cannot safely store a client secret.

**How it works:**
1. The client generates a random `code_verifier`
2. The client hashes it to produce a `code_challenge` and sends it with the authorization request
3. The Authorization Server stores the challenge
4. When the client exchanges the authorization code for a token, it sends the original `code_verifier`
5. The Authorization Server hashes it and compares it to the stored challenge — if they match, the token is issued

**Why it is needed:** Without PKCE, an attacker who intercepts the authorization code (e.g. via a malicious app registered to the same redirect URI scheme) could exchange it for tokens. PKCE binds the code to the original client that requested it.

**Who must use it:** All public clients — browser SPAs, mobile apps, desktop apps. Also recommended for confidential clients as defence-in-depth.

---

### 🏷️ Scopes

Scopes are strings that represent the **specific permissions** a client is requesting. The resource owner approves or denies them during the consent step.

- The client requests scopes in the authorization request
- The Authorization Server includes approved scopes in the access token
- The protected resource checks the token's scopes before fulfilling a request

Examples: `orders:read`, `orders:write`, `catalog:read`, `admin:*`

> Scopes follow the **principle of least privilege** — a client should request only the minimum access it needs.

---

## 🪪 Step 2 — OpenID Connect Concepts

### What does OIDC add to OAuth 2.0?

OAuth 2.0 handles *authorisation* — it proves that a client has been granted permission. It says nothing about *who the user is*. OpenID Connect adds **authentication** on top of OAuth 2.0 by introducing:

- An **ID Token** — a signed JWT containing identity claims about the authenticated user
- A **UserInfo endpoint** — an API to fetch additional user attributes
- Standardised **scopes and claims** for identity data
- A **discovery endpoint** (`/.well-known/openid-configuration`) for dynamic configuration

---

### 🪪 ID Token vs. Access Token

| | ID Token | Access Token |
|---|---|---|
| **Purpose** | Tells the **client** who the user is | Tells the **resource server** what the client is allowed to do |
| **Consumed by** | The client application | The protected resource (API) |
| **Format** | Always a signed JWT | JWT or opaque string |
| **Should be sent to APIs?** | ❌ Never | ✅ Yes — as Bearer token |
| **Contains** | User identity claims (`sub`, `name`, `email`, ...) | Scopes, expiry, audience |

---

### 📦 JWT — JSON Web Token

A JWT consists of three Base64URL-encoded parts separated by dots:

```
header.payload.signature
```

| Part | Content | Purpose |
|---|---|---|
| **Header** | Algorithm (`alg`) and key ID (`kid`) | Tells the receiver how to verify the signature |
| **Payload** | Claims — key/value pairs (e.g. `sub`, `email`, `exp`, `iss`) | The actual data carried by the token |
| **Signature** | Cryptographic signature over header + payload | Proves the token was issued by the Authorization Server and has not been tampered with |

> Tokens can be inspected at **https://jwt.io** — paste any JWT to decode its header and payload.

---

### 🔖 Standard OIDC Claims

| Claim | Meaning | Scope Required |
|---|---|---|
| `sub` | Subject — unique, immutable user identifier | `openid` |
| `iss` | Issuer — URL of the Authorization Server that issued the token | `openid` |
| `aud` | Audience — the intended recipient(s) of the token | `openid` |
| `iat` | Issued At — Unix timestamp of when the token was issued | `openid` |
| `exp` | Expiration — Unix timestamp after which the token is invalid | `openid` |
| `email` | User's email address | `email` |
| `email_verified` | Whether the email has been verified | `email` |
| `name` | Full display name | `profile` |
| `given_name` | First name | `profile` |
| `family_name` | Last name | `profile` |
| `preferred_username` | Username or handle | `profile` |
| `nonce` | Mitigates replay attacks — echoed back from the authorization request | `openid` |

---

### 🌐 ID Token vs. UserInfo Endpoint

| | ID Token | UserInfo Endpoint |
|---|---|---|
| **When returned** | Always, as part of the token response | On demand — client calls `GET /userinfo` with access token |
| **Best for** | Core identity needed immediately after login (`sub`, `email`, `roles`) | Rich profile data fetched only when needed (address, preferences, custom attributes) |
| **Size** | Should be kept small — sent on every request | Can be larger — fetched once and cached |

> **Rule of thumb:** Put only what the client needs immediately into the ID token. Fetch everything else from UserInfo on demand.

---

### 🔗 Standard OIDC Scopes and Their Claims

| Scope | Claims Returned |
|---|---|
| `openid` | `sub`, `iss`, `aud`, `iat`, `exp` (mandatory for OIDC) |
| `profile` | `name`, `given_name`, `family_name`, `preferred_username`, `picture`, `birthdate`, `locale` |
| `email` | `email`, `email_verified` |
| `address` | `address` (structured postal address object) |
| `phone` | `phone_number`, `phone_number_verified` |
| `offline_access` | Requests issuance of a Refresh Token |

---

## 🗺️ Step 3 — Initial ShopFast Mapping

### Grant Types per Client

| Client | Grant Type | PKCE? |
|---|---|---|
| Web Frontend (SPA) | Authorization Code + PKCE | ✅ Yes |
| Mobile App | Authorization Code + PKCE | ✅ Yes |
| Admin Back-Office (server-side) | Authorization Code | Recommended |
| Supplier Portal (server-side) | Authorization Code | Recommended |
| Service-to-Service | Client Credentials | ❌ Not applicable |

### Initial Scope Ideas

| Scope | Purpose | Elevated? |
|---|---|---|
| `catalog:read` | Browse products | ❌ |
| `orders:read` | Read own orders | ❌ |
| `orders:write` | Place and cancel orders | ❌ |

> 💡 These scopes are the starting point. Lab AG-03 maps each scope to its requestors, consumers, and gateway policies in full.

### Initial Claims Needed

| Claim | Standard / Custom | 📦 Location | Why ShopFast needs it |
|---|---|---|---|
| `sub` | Standard | ID Token | Unique user identifier across all services |
| `email` | Standard | ID Token | Customer communications and account identification |
| `email_verified` | Standard | ID Token | Only allow verified emails to place orders |
| `name` | Standard | ID Token | Personalisation in the frontend |
| `given_name` | Standard | UserInfo | Profile page display |
| `family_name` | Standard | UserInfo | Profile page display |
| `preferred_username` | Standard | UserInfo | Account settings display |
| `roles` | Custom | ID Token | Distinguish customer / admin / supplier — drives authorisation decisions |
| `shopfast_customer_id` | Custom | ID Token | ShopFast-internal customer UUID used by microservices to associate data |
| `customer_tier` | Custom | UserInfo | Loyalty programme logic (gold, silver, bronze) — fetched on demand |
| `account_status` | Custom | UserInfo | Prevent suspended accounts from placing orders — checked at login |

> 💡 Claims in the **ID Token** are available immediately after login. Claims from the **UserInfo endpoint** are fetched on demand. Keep the ID token small — only include what is needed on every request. This split is designed in full in Lab AG-03.

## 💡 Trainer Notes

- Groups often struggle with the **ID Token vs. Access Token** distinction. The clearest way to resolve this: *"The ID token is a letter addressed to the client, telling it who the user is. The access token is a key card the client hands to the API."*
- **PKCE** is frequently confused with a replacement for TLS. Clarify: TLS protects the transport; PKCE protects the authorization code from being stolen and replayed by a different client.
- The **Client Credentials** flow surprises groups — they expect every flow to involve a user. Emphasise: in a microservice landscape, services themselves are security principals that authenticate to each other.
- The **Implicit flow** appears in older tutorials. Flag it as deprecated (replaced by Authorization Code + PKCE per OAuth 2.1 draft) and redirect any group proposing it.
- The **UserInfo endpoint vs. ID token** decision becomes very practical in Step 3: if the frontend needs to show the user's name immediately after login, it must be in the ID token. If it only needs the address when the user navigates to their profile, fetch it from UserInfo then.
