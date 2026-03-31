# 🧪 Lab MS-04 — Microservices: Failure Scenarios & Resilience

> 👥 **Group Exercise** &nbsp;|&nbsp; 🗂️ Topic: Microservice Architecture &nbsp;|&nbsp; 📐 Artifacts: Failure Map · Resilience Patterns

---

## 📖 Context

In a distributed system, failure is not an exception — it is the norm. Any service can become slow or unavailable at any time, and a single failing dependency can cascade into a full system outage if not handled deliberately. Resilient systems are not built by hoping things won't fail, but by designing for failure from the start.

This lab uses your service map and integration design from the previous labs as the basis for identifying where ShopFast is most vulnerable — and how to protect it.

---

## ✅ Your Tasks

### 💥 Step 1 — Identify Failure Scenarios

Go through your service map and for each service and integration point, ask: *what happens if this fails?*

**Write one failure card per scenario** and place it on the relevant service or connection on your service map. Each card must contain:

- 💥 The **failure scenario** — what exactly fails? (e.g. payment service is unreachable, inventory response is too slow)
- 🌊 The **blast radius** — which other services or user flows are affected?
- 👤 The **user impact** — what does the customer experience when this failure occurs?
- 🔴 The **severity** — rate it as Critical, High, or Medium

> 💡 **Tip:** Pay special attention to synchronous dependencies — a slow downstream service will block the caller and can exhaust its resources. Asynchronous integrations are typically more resilient by nature.

---

### 🛡️ Step 2 — Apply Resilience Patterns

For each failure scenario identified in Step 1, propose a resilience pattern to mitigate it. **Write one resilience card per scenario** and attach it to the corresponding failure card. Each card must contain:

- 🛡️ The **pattern name**
- 📋 A brief description of how it works in this specific context
- ✅ What it protects against
- ⚠️ Any trade-offs or limitations

> 📖 **Reference:** Use the **Patterns of Resilience** presentation for a full overview of available patterns, their mechanics, and when to apply them. Browse it as a group and select the patterns most applicable to your failure scenarios.

> 💡 **Tip:** Patterns are often combined. A resilient service call typically applies a timeout, a retry with backoff, and a circuit breaker together.

---

### 🔁 Step 3 — Walk Through a Failure Scenario End-to-End

Pick the **most critical failure scenario** from Step 1 and walk through it as a group on the board:

1. 🔴 Mark the **point of failure** on the service map
2. 🌊 Trace the **cascade** — which services are affected, in what order?
3. 🛡️ Apply your resilience cards and describe **step by step** how the system responds and recovers
4. 👤 Describe what the **customer experiences** — is the degradation graceful or does the system fail completely?

> 💡 **Tip:** The goal is not zero failures — it is graceful degradation. A good outcome is: the checkout still works even if the recommendation service is down.

---

## 📦 Deliverable

A board your group can walk the others through in the review session, showing:

1. 💥 The **failure cards** placed on the service map with severity ratings
2. 🛡️ The **resilience pattern cards** attached to each failure
3. 🔁 The **end-to-end walkthrough** of your most critical failure scenario

---

> 🚀 *A system that handles failure gracefully is more trustworthy than one that never fails in the lab but breaks unpredictably in production.*
