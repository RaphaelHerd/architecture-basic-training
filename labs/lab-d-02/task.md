# 🧪 Lab D-02 — Domain-Driven Design: Modeling the Domain

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Domain-Driven Design &nbsp;|&nbsp; 📐 Artifacts: Domain Model · Aggregate Roots · Domain Events

---

## 📖 Context

This lab continues directly from the **previous labs**. You have already defined a ubiquitous language and identified the bounded contexts of ShopFast. Now it is time to model what is inside those contexts — the domain objects, their responsibilities, and the events that flow between them.

---

## ✅ Your Tasks

### 🧱 Step 1 — From Anemic to Rich Domain Model

In traditional development, domain objects are simple data containers — all business logic lives in a service layer. DDD replaces this **anemic model** with a **rich domain model**, where business logic is encapsulated directly within the domain objects.

Pick one bounded context from your previous lab and identify its core domain objects. For each object, discuss as a group:

- Is this object currently just a data bag, or does it carry behaviour?
- What business rules or validations naturally belong inside this object?

**Write one card per domain object** and place them on the board. Each card must contain:

- 🏷️ The **object name**
- 📋 Its **key attributes**
- ⚙️ The **business logic or rules** that belong inside it (not in a service)

> 💡 **Tip:** Think about what should happen when an attribute changes — e.g. when a quantity drops to zero, or when a payment is confirmed. That logic belongs in the domain object.

---

### 👑 Step 2 — Identify Aggregate Roots

An **aggregate** is a cluster of domain objects treated as a single unit. The **aggregate root** is the only entry point to that cluster — all changes to objects within the aggregate must go through it.

Using the domain object cards from Step 1, group them into aggregates on the board:

1. 👑 Mark the **aggregate root** of each group with a distinct card or label
2. 📋 Place all **child objects** of the aggregate around it
3. ✏️ Annotate the aggregate root card with: which operations must be performed through it, and which invariants it enforces

> 💡 **Tip:** Ask yourself — can this object exist independently, or does it only make sense in the context of another object? If the latter, it likely belongs inside an aggregate.

---

### ⚡ Step 3 — Model Domain Events

A **domain event** represents something meaningful that has happened in the business domain. Events make state changes explicit and allow bounded contexts to react to each other without tight coupling.

For the bounded context you modeled, identify the key domain events. **Write one card per event** and arrange them on the board in the order they occur in a typical business flow. Each card must contain:

- ⚡ The **event name** (past tense, e.g. *OrderPlaced*, *PaymentConfirmed*)
- 🎯 The **trigger** — what action or condition causes this event
- 👂 The **consumers** — which other bounded contexts or components react to it

> 💡 **Tip:** Follow a concrete scenario end-to-end, such as a customer placing an order. Trace each step and ask: *what just happened that the rest of the system should know about?*

---

## 📦 Deliverable

A single board your group can walk the others through in the review session, showing:

1. 🧱 The **rich domain model cards** with attributes and encapsulated business logic
2. 👑 The **aggregate structure** with roots and child objects clearly grouped
3. ⚡ The **domain event flow** arranged in business sequence

---

> 🚀 *The domain model and events you define here will form the contracts between microservices in the next exercises.*
