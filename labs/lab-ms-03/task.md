# 🧪 Lab MS-03 — Microservices: Integration Design

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Microservice Architecture &nbsp;|&nbsp; 📐 Artifacts: Integration Map · REST API · Event Flow

---

## 📖 Context

Your service map from the previous labs defines which microservices exist and which of them need to communicate. This lab is about deciding **how** they communicate. Not every interaction is the same — some require an immediate response, others are better handled asynchronously. Getting these decisions right determines how loosely coupled and resilient your system will be.

---

## ✅ Your Tasks

### 🔀 Step 1 — Choose Integration Styles

Go through each connection on your service map and decide whether the interaction should be **synchronous** or **asynchronous**.

**Write one decision card per connection** and place it on the relevant arrow of your service map. Each card must contain:

- 🔗 The **two services** involved
- 🔄 The **integration style** — synchronous (REST / gRPC) or asynchronous (event-based)
- ✅ The **justification** — why is this the right choice for this interaction?
- ⚠️ The **trade-off accepted** — what do you give up with this choice?

Use the following questions to guide your decision:

| Question | Points toward Synchronous | Points toward Asynchronous |
|---|---|---|
| Does the caller need an immediate result? | ✅ | ❌ |
| Can the interaction tolerate delay? | ❌ | ✅ |
| Is tight coupling acceptable here? | ✅ | ❌ |
| Does the consumer need to know who produced the data? | ✅ | ❌ |

> 💡 **Tip:** Prefer asynchronous communication wherever possible — it reduces coupling and improves resilience. Only choose synchronous when an immediate response is truly required by the business flow.

---

### 🌐 Step 2 — Design the REST API

For all connections you marked as **synchronous** in Step 1, design the REST API for the providing service.

Take the API contract cards from your previous lab as a starting point and extend them with REST-specific decisions. **Update or create one card per endpoint**:

- 🔤 The **HTTP method** — GET, POST, PUT, PATCH, or DELETE
- 🌐 The **resource path** — following REST conventions (e.g. `/orders/{id}`)
- ➡️ The **request body or path/query parameters**
- ⬅️ The **response body and HTTP status code** on success
- ⚠️ The **HTTP status codes** for each error case

Arrange the endpoint cards grouped by resource on the board and aim for at least **Richardson Maturity Level 2**:

| Level | Requirement |
|---|---|
| Level 0 | Single URI, single HTTP method |
| Level 1 | Multiple URIs per resource |
| **Level 2** | **Multiple URIs + correct use of HTTP methods and status codes** |
| Level 3 | Level 2 + HATEOAS hypermedia links |

> 💡 **Tip:** Check that your resource names come from the ubiquitous language. A path like `/process-order` is a procedure, not a resource — prefer `/orders` with a POST.

---

### ⚡ Step 3 — Design the Event-Driven Integration

For all connections you marked as **asynchronous** in Step 1, design the event-driven integration.

Take the domain event cards from the DDD labs and extend them into a full event flow on the board. **Write one event flow card per event**:

- ⚡ The **event name** — in past tense (e.g. `OrderPlaced`)
- 📢 The **producer** — which service emits this event?
- 📦 The **event payload** — what data does the event carry?
- 👂 The **consumers** — which services subscribe and what do they do in response?
- 🔁 What happens if a consumer is **temporarily unavailable**?

Arrange the event flow cards in the sequence they occur during a business scenario, such as the checkout process.

> 💡 **Tip:** An event describes something that **has already happened** — the producer does not know or care who reacts. If your producer needs to know who receives the event, reconsider whether this should be synchronous instead.

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 🔀 The **integration decision cards** on your service map, with justifications
2. 🌐 The **REST endpoint cards** grouped by resource, at Maturity Level 2 or above
3. ⚡ The **event flow cards** arranged in business sequence with producers, payloads, and consumers

---

> 🚀 *Integration is where microservices either stay loosely coupled or inadvertently become a distributed monolith — the decisions you make here have long-lasting architectural consequences.*
