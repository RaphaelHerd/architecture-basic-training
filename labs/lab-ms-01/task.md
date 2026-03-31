# 🧪 Lab MS-01 — Microservices: Service Decomposition

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Microservice Architecture &nbsp;|&nbsp; 📐 Artifacts: Service Map · Team Ownership

---

## 📖 Context

This lab builds directly on the bounded contexts you defined in the **previous labs**. Each bounded context represents a candidate for an independent microservice. Now it is time to make that decomposition concrete — defining not just what each service does, but who owns it, what data it controls, and how it fits into the larger system.

---

## ✅ Your Tasks

### 🗂️ Step 1 — Define Your Microservices

For each bounded context from the previous labs, define a corresponding microservice. **Write one card per service** and place them on the board. Each card must contain:

- 🏷️ The **service name**
- 🎯 Its **business capability** — what single responsibility does this service own?
- 📦 The **data it owns** — which domain objects and their persistence belong exclusively to this service?
- 🚫 What it explicitly does **not** do — where does its responsibility end?

> 💡 **Tip:** A well-scoped microservice should be explainable in one sentence. If you need more, it may be doing too much. Apply the two-pizza team rule: could a small team of up to a dozen people fully own and operate this service?

---

### 👥 Step 2 — Assign Team Ownership

A microservice without a clear owner tends to become nobody's responsibility. Assign a team to each service card on the board:

1. 🏷️ Label each service card with a **team name**
2. 📋 Note the **core competencies** that team would need
3. ⚠️ Identify any services where ownership is unclear or where two teams might conflict — mark these cards visibly

> 💡 **Tip:** Think about Conway's Law — your team structure will inevitably shape your service boundaries. If two services are always changed together, they may belong to the same team or should be merged.

---

### 🗺️ Step 3 — Draw the Service Map

Arrange all service cards on the board to form a **service map** for ShopFast:

1. 🟦 Place each service as a labeled box
2. ➡️ Draw connections between services that need to communicate, with a brief label describing the interaction
3. 🔴 Highlight any connections that cross team boundaries — these are the integration points that require the most careful design

> 💡 **Tip:** Do not design the communication mechanism yet — just identify which services need to talk to each other and why. That comes in the next labs.

---

## 📦 Deliverable

A single board your group can walk the others through in the review session, showing:

1. 🗂️ All **service cards** with capability, data ownership, and team assignment
2. 🗺️ A **service map** with communication dependencies and cross-team integration points highlighted

---

> 🚀 *The service map you create here is the architectural backbone of ShopFast as a microservice system — all subsequent labs will build on it.*
