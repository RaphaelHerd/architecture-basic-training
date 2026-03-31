# 🧪 Lab MS-02 — Microservices: API First Design

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Microservice Architecture &nbsp;|&nbsp; 📐 Artifacts: API Contract · Resource Model

---

## 📖 Context

This lab connects your domain model to the outside world. In an API First approach, the public contract of a service is designed and agreed upon before any implementation begins. This allows consuming teams to work independently and in parallel, and makes integration boundaries explicit from the start.

You have already done the hard thinking in the previous labs — your **ubiquitous language glossary**, **bounded context map**, **rich domain model cards**, **aggregate roots**, and **domain events** are all direct inputs to this lab. Bring them to the board.

---

## ✅ Your Tasks

### 🎯 Step 1 — Choose Your Service

Pick **one microservice** from your service map. Choose a service that has meaningful interactions with other services or external consumers — the richer the interactions, the more interesting the design.

Write a **service header card** and place it at the top of the board, containing:

- 🏷️ The **service name** — taken from your bounded context map
- 🎯 Its **business capability** in one sentence — as defined on your service card from Lab MS-01
- 👥 The **consumers** — which other services or clients will call this API, based on the communication dependencies in your service map?

---

### 📋 Step 2 — Define Your Resources

Take the **domain object cards** from your rich domain model (DDD labs) and identify which objects are visible to the outside world. Not every domain object becomes a resource — only those that a consumer legitimately needs to interact with.

**Write one resource card per exposed object** and place them on the board. Each card must contain:

- 🏷️ The **resource name** — use the exact term from your ubiquitous language glossary
- 📦 Its **key attributes** — taken from your domain object cards, reduced to what a consumer needs to see
- ⚙️ The **operations** a consumer can perform on it (e.g. create, read, update, cancel)

> 💡 **Tip:** Your aggregate root is usually the primary resource. Child objects and value objects are often part of its representation, not separate resources. Compare with your aggregate structure cards from the DDD labs.

---

### 🔌 Step 3 — Design the API Contract

For each operation identified in Step 2, define the API contract. **Write one card per operation** and place it beneath the relevant resource card. Each card must contain:

- 🔤 The **operation name** and a brief description
- ➡️ The **request** — what input does the consumer provide?
- ⬅️ The **response** — what does the service return on success?
- ⚠️ The **error cases** — what can go wrong, and how is it communicated?

Additionally, look at your **domain event cards** from previous labs. For each event emitted by this service, add an **event contract card** to the board:

- ⚡ The **event name** — in past tense, as defined in the previous Lab
- 📦 The **event payload** — what data does the event carry?
- 👂 The **consumers** of this event — which services react to it?

> 💡 **Tip:** Think from the consumer's perspective. What is the minimum information a consumer needs to send? What is the minimum they need to receive? Avoid leaking internal implementation details into the contract.

---

### 🤝 Step 4 (optional, if time left) — Review as a Consumer

Swap your board with another group. Review their contract from the perspective of a consuming team and answer:

- ✅ Is the contract clear enough to build against without asking questions?
- ❓ Are there any ambiguities or missing error cases?
- 🔗 Does the naming align with the ubiquitous language, or does it introduce new terms?

Write your feedback on sticky notes and attach them to the relevant cards.

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 🎯 The **service header card** with capability and consumers
2. 📋 The **resource cards** with attributes and operations
3. 🔌 The **API contract cards** per operation with request, response, and error cases
4. ⚡ The **event contract cards** for all domain events emitted by the service
5. 🤝 The **consumer feedback** from the cross-group review

---

> 🚀 *The API contracts you define here are the boundaries between microservices — precise, stable contracts are what enable teams to work independently at scale.*
