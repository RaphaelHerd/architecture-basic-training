# 🧪 Lab RE-01 — Requirements Engineering: Context Model

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Requirements Engineering &nbsp;|&nbsp; 📐 Artifact: Context Model

---

## 📖 Case Study: ShopFast — An Online Shop Platform

ShopFast is a newly founded e-commerce company building a modern online shop platform. The platform enables customers to discover products, place orders, and track deliveries. ShopFast is designed with growth in mind and anticipates a future in which multiple independent teams will own and evolve different parts of the system.

### 🏢 Business Context

ShopFast sells physical products sourced from various suppliers. Customers can register an account or proceed as guests. The platform supports product search and filtering, detailed product pages, a shopping cart, and order placement. Following a successful order, customers receive status updates via email.

**Payments** are delegated to an external payment provider (e.g. Stripe or PayPal). ShopFast does not store or process payment card data directly.

**Shipping** is handled by an external logistics provider. When an order is ready for dispatch, ShopFast transmits the shipment data and receives tracking information in return. Customers can monitor their shipment status through their order history.

**Product management** is the responsibility of an internal back-office team operating an admin tool. This includes maintaining product descriptions, prices, and stock levels. Stock is adjusted both when orders are placed and when new goods are received from suppliers.

**Suppliers** have access to a dedicated supplier portal, through which they can register new products and update delivery quantities.

**Marketing** campaigns are executed through an external email marketing platform (e.g. Mailchimp). ShopFast provides anonymized customer segments to drive targeted outreach.

**Analytics** are powered by an external analytics platform (e.g. Google Analytics or a data warehouse). ShopFast forwards relevant business events — such as orders, registrations, and browsing activity — to this platform.

### ⚠️ Key Challenges

| Challenge | Description |
|---|---|
| 🔒 Privacy & Security | Customer and payment data must be handled with strict confidentiality and access controls. |
| 📦 Stock Consistency | Inventory levels must remain accurate at all times — overselling must be prevented. |
| ⚡ Availability | The system must remain stable and responsive under high-traffic conditions, such as sales events. |
| 🏗️ Team Scalability | The architecture must support independent development and deployment across multiple teams. |

---

## ✅ Your Tasks

### 🔍 Step 1 — Analyze the Case Study

Read the case study as a group and discuss the following questions:

- 🔗 Which **external systems** interact with ShopFast?
- 🎯 What are the **core responsibilities** of the ShopFast platform itself?
- ↔️ What data or events flow **into** the system, and what flows **out**?

---

### 🗺️ Step 2 — Create a Context Model

Create a **context model** (system boundary diagram) for ShopFast.

Use a component diagram or a simple box-and-arrow notation — UML is recommended but not mandatory. The model must clearly show:

1. 🟦 The **ShopFast system** as a unified black box
2. 🌐 All **external systems** that interact with ShopFast
3. ➡️ The **direction and nature** of each interaction, expressed as labeled arrows

> 💡 **Focus on boundaries, not internals.** The goal is to define what is inside and outside the system — internal structure will be addressed in the next exercise.

---

## 📦 Deliverable

Produce a single context model diagram — on a whiteboard, paper, or a digital tool of your choice — that your group can present and walk through in the subsequent review session.

---

> 🚀 *The context model you create today will serve as the architectural foundation for the next exercises, in which the system's internal components will be designed using Domain-Driven Design and decomposed into microservices.*
