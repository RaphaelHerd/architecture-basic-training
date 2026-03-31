# 🧪 Lab AG-02 — API Gateway: End-to-End Security with OAuth 2.0 & OIDC

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: API Gateway · Security &nbsp;|&nbsp; 📐 Artifact: End-to-End Security Concept

---

## 📖 Context

ShopFast has multiple client types, multiple microservices, and an API gateway as its front door. Securing this landscape requires more than just adding a password — it requires a deliberate security architecture that controls **who can access what, on whose behalf, and for how long**.

OAuth 2.0 provides the delegation framework. OpenID Connect (OIDC) adds identity on top. Together they form the foundation of modern API security.

---

## ✅ Your Tasks

### 🔑 Step 1 — Choose Grant Types per Client

Not all clients authenticate the same way. Using the grant type decision tree from the presentation, select the appropriate OAuth 2.0 grant type for each client in ShopFast.

**Write one decision card per client** and place it on the board. Each card must contain:

- 📱 The **client name** and type (web app, native app, service, ...)
- 🔑 The **selected grant type**
- ✅ The **justification** — why is this the right choice?
- 🔒 Whether **PKCE** is required and why

Consider at least the following clients:

| Client | Type |
|---|---|
| ShopFast Web Frontend | Browser-based application |
| ShopFast Mobile App | Native application |
| Admin Back-Office Tool | Internal web application |
| Supplier Portal | External web application |
| Microservice-to-Microservice | Background service, no user |

> 💡 **Tip:** Service-to-service calls have no resource owner — no user is involved. Which grant type is designed exactly for this case?

---

### 🏷️ Step 2 — Define Scopes

Scopes control what a token allows a client to do. Define the OAuth scopes for the ShopFast API, grouping them by microservice.

**Write one scope card per scope** and arrange them on the board grouped by service. Each card must contain:

- 🏷️ The **scope name** (e.g. `orders:read`, `orders:write`, `catalog:read`)
- 📋 What access it **grants**
- 👤 Which **clients** would typically request it
- 🔒 Whether it requires **elevated privileges** (e.g. admin-only)

> 💡 **Tip:** Scopes should follow the principle of least privilege — a client should only request the minimum access it needs. A public customer browsing products does not need `orders:write`.

---

### 🪪 Step 3 — Design the OIDC Identity Layer

OAuth 2.0 handles authorisation — but ShopFast also needs to know **who the user is**. OpenID Connect adds this identity layer on top of OAuth 2.0 via an ID token.

Design the OIDC integration for ShopFast on the board:

1. 🪪 Define the **standard OIDC claims** ShopFast needs from the ID token (e.g. `sub`, `email`, `name`)
2. 🏷️ Define any **custom claims** specific to ShopFast (e.g. customer tier, account status, roles)
3. 📦 Decide which claims go into the **ID token** (consumed by the client) and which are fetched from the **UserInfo endpoint** (on demand)
4. 🔗 Map claims to **scopes** — which scope must a client request to receive each claim?

> 💡 **Tip:** The ID token is for the client to identify the user. The access token is for the resource server to authorise the request. Do not use the ID token to call APIs.

---

### 🔄 Step 4 — Design the Token Lifecycle

Tokens are not permanent. Design the full token lifecycle for ShopFast:

**Write one lifecycle card per client type**, covering:

- ⏱️ The **access token lifetime** — how long should it be valid?
- 🔄 **Refresh token** — is one issued? Under what conditions is it used?
- ❌ **Token revocation** — when and how are tokens revoked? (e.g. logout, account suspension)
- 🔁 **Re-authentication** — when must the user authenticate again?

> 💡 **Tip:** Short-lived access tokens reduce the blast radius of a stolen token. Refresh tokens allow sessions to be maintained without re-authenticating the user on every request.

---

### 🏛️ Step 5 — End-to-End Security Flow

Bring everything together. On the board, trace the complete security flow for the following scenario:

> *A customer logs into the ShopFast mobile app and places an order. The order service needs to call the inventory service internally to reserve stock.*

For each step in this flow, annotate the board with:

- 🔐 Which **grant type and flow** is used
- 🎟️ Which **token** is presented (access token, ID token, or none)
- 🛡️ Where **token validation** happens (API gateway, microservice, or both)
- 🏷️ Which **scopes and claims** are checked at each step

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 🔑 The **grant type decision cards** per client with PKCE decisions
2. 🏷️ The **scope cards** grouped by microservice
3. 🪪 The **OIDC claims design** with ID token vs. UserInfo split
4. 🔄 The **token lifecycle cards** per client type
5. 🏛️ The **end-to-end security flow** for the order placement scenario

---

> 🚀 *Security is not a feature added at the end — it is a design decision that shapes every layer of the architecture, from the client through the gateway to the microservice.*
