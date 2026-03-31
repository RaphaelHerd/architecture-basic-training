# 🧪 Lab D-03 — Domain-Driven Design: Full Design & Architecture

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Domain-Driven Design &nbsp;|&nbsp; 📐 Artifacts: Full DDD Design · Hexagonal Architecture

---

## 📖 Context

This lab is the culmination of the **previous labs**. You have defined a ubiquitous language, identified bounded contexts, modeled domain objects and aggregate roots, and described domain events. Now you will bring everything together into a complete domain design and map it onto a hexagonal architecture.

---

## ✅ Your Tasks

### 🛒 Step 1 — Full DDD Design for the Checkout Process

Design the complete domain model for the ShopFast **checkout process** — from a customer confirming their cart to the order being handed off to the shipping provider.

On the board, model the following using cards:

1. 👑 The **aggregate root** and all domain objects involved in the checkout
2. ⚙️ The **business rules** that must be enforced during checkout (e.g. stock availability, coupon validation, payment authorisation)
3. 🔀 The **domain service** responsible for logic that spans multiple aggregates
4. 🎛️ The **application service** that orchestrates the overall checkout flow
5. ⚡ The **domain events** emitted during the process, in sequence

> 💡 **Tip:** Clearly separate what belongs in the domain layer (business rules, invariants) from what belongs in the application layer (orchestration, calling external systems). If a rule references business terminology, it belongs in the domain.

---

### 🔷 Step 2 — Map to Hexagonal Architecture

Hexagonal architecture (also known as Ports & Adapters) keeps the domain model at the centre, free from any technical dependencies. Everything outside the domain communicates through well-defined **ports**, implemented by **adapters**.

Take one bounded context from Step 1 and map it onto a hexagonal architecture diagram on the board. Place cards for:

1. 🟦 The **domain core** — domain objects, aggregate roots, domain services
2. 🎛️ The **application services** — use case orchestration, sitting just outside the domain core
3. 🔌 **Inbound ports** — interfaces that expose the application to the outside world (e.g. REST API, message consumer)
4. 🔌 **Outbound ports** — interfaces the application uses to reach external systems (e.g. payment gateway, database, message broker)
5. 🔧 **Adapters** — concrete implementations of the ports (e.g. Stripe adapter, JPA repository, Kafka producer)

> 💡 **Tip:** The domain core must have zero knowledge of the adapters. Dependency arrows always point inward — toward the domain.

---

## 📦 Deliverable

A single board your group can walk the others through in the review session, showing:

1. 🛒 The **full DDD checkout design** with all layers, rules, services, and events
2. 🔷 The **hexagonal architecture diagram** for one bounded context with ports and adapters clearly identified

---

> 🚀 *This design directly reflects how you would structure a microservice — one bounded context, one hexagon, one deployable unit.*
