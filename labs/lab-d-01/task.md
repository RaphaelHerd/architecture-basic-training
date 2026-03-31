# 🧪 Lab D-01 — Domain-Driven Design: Understanding the Domain

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Domain-Driven Design &nbsp;|&nbsp; 📐 Artifacts: Ubiquitous Language · Bounded Contexts

---

## 📖 Context

This lab builds directly on the ShopFast case study and the context model you created in the **previous labs**. You now know which external systems interact with ShopFast and where the system boundary lies. The next step is to look inside that boundary and understand the business domain itself.

Before any code is written or architecture is decided, the team must establish a shared understanding of the domain — its language and its internal structure.

---

## ✅ Your Tasks

### 📖 Step 1 — Build a Ubiquitous Language Glossary

In DDD, a **ubiquitous language** is a shared vocabulary used consistently by both business stakeholders and developers. It eliminates ambiguity and ensures that the code reflects the real business.

As a group, identify the key domain terms used in ShopFast and define them precisely. Pay special attention to terms that could be misinterpreted or mean different things in different contexts.

**Write one card per term** and place them on the board. Each card must contain:

- 🏷️ The **term**
- 📝 A precise **definition** in one or two sentences
- ❓ Any **ambiguities or open questions** the group noticed

> 💡 **Tip:** Aim for at least 10–15 cards. Think across the full lifecycle — from a customer browsing products to a shipment being delivered.

---

### 🗺️ Step 2 — Identify Bounded Contexts

A **bounded context** defines a clear boundary within which a particular domain model applies. Inside a bounded context, terms have precise, unambiguous meanings. The same term (e.g. *Product*) may mean something different in another bounded context.

Analyze the ShopFast domain and identify its bounded contexts. On the board:

1. 🏷️ Create a **header card** for each bounded context, named after its business capability
2. 📋 Place the **domain object cards** from Step 1 underneath the bounded context they belong to
3. 🔗 Use lines or arrows to connect **shared domain objects** that appear in multiple contexts — and annotate how their meaning differs

> 💡 **Tip:** A bounded context should align with a clear business capability. If you find yourself unsure which context a card belongs to, that is a signal worth discussing — it often reveals a hidden boundary.

---

## 📦 Deliverable

A single board your group can walk the others through in the review session, showing:

1. 📋 The **ubiquitous language cards** with at least 10 defined terms
2. 🗺️ The **bounded context map** with cards grouped by context and shared objects connected

---

> 🚀 *The bounded contexts you define here will directly drive the microservice decomposition in the next exercises — choose your boundaries thoughtfully.*
