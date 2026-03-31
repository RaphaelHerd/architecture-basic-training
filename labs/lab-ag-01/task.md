# 🧪 Lab AG-01 — API Gateway: Cross-Cutting Concerns & Gateway Design

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: API Gateway &nbsp;|&nbsp; 📐 Artifacts: Concern Map · Gateway Design · Solution Recommendation

---

## 📖 Context

As the number of microservices grows, certain technical concerns appear in every single service — authentication, logging, rate limiting, and more. Implementing these individually per service is expensive, error-prone, and hard to keep consistent. An API gateway centralises these concerns at the edge of the system, so each service can focus purely on its business capability.

This lab uses your ShopFast service map from the previous labs as the foundation.

---

## ✅ Your Tasks

### 🔍 Step 1 — Identify Cross-Cutting Concerns

Go through your service map and identify all technical concerns that would need to be implemented in **every service** if there were no gateway.

**Write one concern card per topic** and place them on the board next to the services they affect. Each card must contain:

- 🏷️ The **concern name** (e.g. Authentication, Rate Limiting, Logging)
- 📋 A brief description of **what it does** and **why it is needed**
- 🟢 The **benefit of centralising it** at a gateway

> 💡 **Tip:** Think beyond security. Concerns like request logging, response caching, CORS headers, and protocol translation are equally valid candidates.

---

### 🗺️ Step 2 — Design the API Gateway Layer

Using the concerns identified in Step 1 and the REST endpoints from the previous labs, design the API gateway layer for ShopFast on the board.

Draw a gateway box in front of your service map and define:

1. 🌐 Which **external endpoints** are exposed through the gateway — create one endpoint card per route
2. 🔀 The **internal service** each route maps to
3. 🛡️ The **policies applied** per route — which cross-cutting concerns apply to which endpoints?
4. 🚫 Which services or endpoints are **not** accessible from outside and remain internal only

> 💡 **Tip:** Not every policy applies to every route. A public product catalog endpoint has different requirements than an internal order management endpoint.

---

### 🔎 Step 3 — Research & Select a Gateway Solution

As a group, research available API gateway solutions and select the one you would recommend for ShopFast. Consider at least the following options in your research:

- Kong
- AWS API Gateway
- Azure API Management
- Traefik
- nginx

**Write one evaluation card per solution** and place them on the board. Each card must contain:

- 🏷️ The **solution name**
- ✅ Its **key strengths** relevant to ShopFast
- ❌ Its **limitations or trade-offs**
- 💰 Its **licensing model** — open source, managed service, or commercial

Then write a **recommendation card** summarising:

- 🏆 Your **recommended solution** for ShopFast
- 🎯 The **key reasons** for your choice
- ⚠️ The **main risk** of this decision

> 💡 **Tip:** There is no universally correct answer. The right solution depends on your team's infrastructure, cloud strategy, and operational maturity — make your assumptions explicit.

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 🔍 The **cross-cutting concern cards** mapped onto the service landscape
2. 🗺️ The **gateway design** with external routes, internal mappings, and per-route policies
3. 🏆 The **solution evaluation cards** and your justified recommendation

---

> 🚀 *A well-designed API gateway is the single front door to your system — it is where security, observability, and traffic control meet the business.*
