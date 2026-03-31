# 🧪 Lab AG-02 — Research: OAuth 2.0 & OpenID Connect

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: API Gateway · Security &nbsp;|&nbsp; 📐 Artifact: Knowledge Summary

---

## 📖 Context

Before you can design a security concept for ShopFast, you need to understand the tools available to you. **OAuth 2.0** is the industry-standard delegation framework for API security. **OpenID Connect (OIDC)** extends it with identity — enabling applications to know *who* the user is, not just *what* they are allowed to do.

This lab is a guided research session. Your goal is to build enough understanding of OAuth 2.0 and OIDC to apply it to a real system in the next lab.

---

## 📚 Sources

Use the following resources as your research material. You do not need to read everything — focus on the questions in each step and find the relevant sections.

| 🔗 Source | 📋 What it covers |
|---|---|
| [OAuth 2.0 — RFC 6749 (simplified overview)](https://oauth.net/2/) | Official OAuth 2.0 overview, grant types, token types |
| [OAuth 2.0 Simplified (aaronparecki.com)](https://www.oauth.com/) | Highly readable guide to all OAuth concepts with examples |
| [OpenID Connect explained (connect2id.com)](https://connect2id.com/learn/openid-connect) | Clear explanation of OIDC, ID tokens, UserInfo, and claims |
| [JWT.io](https://jwt.io/) | Interactive JWT decoder — paste any token to inspect its structure |
| [OAuth 2.0 Grant Types (aaronparecki.com)](https://www.oauth.com/oauth2-servers/differences-between-oauth-1-2/grant-types/) | Overview of all grant types and when to use them |
| [PKCE explained (auth0.com)](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-pkce) | What PKCE is, why it exists, how it works |
| [Token lifetimes and refresh tokens (auth0.com)](https://auth0.com/docs/secure/tokens) | Access tokens, refresh tokens, revocation |
| [OpenID Connect scopes and claims (openid.net)](https://openid.net/specs/openid-connect-core-1_0.html#ScopeClaims) | Standard OIDC scopes and the claims they return |

---

## ✅ Your Tasks

### 🔐 Step 1 — Understand OAuth 2.0

Research the core concepts of OAuth 2.0 and capture your findings on cards. Place one card per concept on the board.

Answer the following questions:

- 🤔 What problem does OAuth 2.0 solve? What existed before it — and why was it insufficient?
- 👥 Who are the **four roles** in OAuth 2.0? Define each one.
- 🎟️ What is an **Access Token**? What is a **Refresh Token**? How do they differ?
- 🔀 What are the **grant types** (flows)? Name at least four and describe when each is appropriate.
- 🔒 What is **PKCE**? Why is it needed, and which clients must use it?
- 🏷️ What are **scopes**? How do they control access?

---

### 🪪 Step 2 — Understand OpenID Connect

Research how OpenID Connect extends OAuth 2.0 and capture your findings on cards.

Answer the following questions:

- 🤔 What does OAuth 2.0 **not** provide that OpenID Connect adds?
- 🪪 What is an **ID Token**? How does it differ from an Access Token?
- 📦 What is a **JWT (JSON Web Token)**? What are its three parts?
- 🔖 What are **claims**? Name at least five standard OIDC claims.
- 🌐 What is the **UserInfo endpoint**? When should a client use it instead of reading claims from the ID token?
- 🔗 What scopes trigger which claims? (e.g. what does requesting `email` return?)

---

### 🗺️ Step 3 — Map Concepts to ShopFast

Using what you have learned, discuss as a group how these concepts apply to ShopFast. On the board, place cards for:

- 🔐 Which **grant type** would you use for a mobile app? For a server-side web app? For a background service with no user?
- 🏷️ What **scopes** would ShopFast need? Think across the services in your service map.
- 🪪 Which **claims** would ShopFast need in the ID token? Are there any custom claims needed beyond the OIDC standard?
- 🔄 How long should **access tokens** live? When should a **refresh token** be used?

> 💡 **Tip:** You do not need to design the full security concept here — that is the task of the next lab. The goal is to arrive with enough understanding to make those decisions confidently.

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 🔐 **OAuth 2.0 concept cards** — roles, tokens, grant types, PKCE, scopes
2. 🪪 **OIDC concept cards** — ID token, JWT, claims, UserInfo endpoint
3. 🗺️ **Initial ShopFast mapping cards** — grant types, scopes, and claims relevant to the system

---

> 🚀 *Everything you document here will be your reference material in the next lab, where you will design the full end-to-end security concept for ShopFast.*
