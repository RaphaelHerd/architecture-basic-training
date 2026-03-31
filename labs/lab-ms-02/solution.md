# ✅ Lab MS-02 — Solution: API First Design

> 🗂️ Topic: Microservice Architecture &nbsp;|&nbsp; 📐 Artifacts: API Contract · Resource Model &nbsp;|&nbsp; 🔒 Trainer Reference

> This solution uses the **Order Service** as the example. It is the most interconnected service in ShopFast and the richest subject for API First design.

---

## 🎯 Step 1 — Service Header Card

| Field | Value |
|---|---|
| 🏷️ **Service Name** | Order Service |
| 🎯 **Business Capability** | Manages the full lifecycle of a customer order — from placement through payment confirmation to fulfilment or cancellation. |
| 👥 **Consumers** | Web Frontend (place order, view history), Mobile App (place order, track status), Shipping Service (read confirmed orders), Admin Tool (read/update any order) |

---

## 📋 Step 2 — Resource Cards

| 🏷️ Resource | 📦 Key Attributes | ⚙️ Operations |
|---|---|---|
| **Order** | `id`, `customerId`, `status`, `items`, `total`, `couponCode`, `placedAt` | Create, Read, Cancel |
| **OrderItem** | `productId`, `productName`, `quantity`, `unitPrice`, `lineTotal` | Read only (part of Order representation — not a standalone resource) |

> **Note:** `OrderItem` is not a top-level resource — it is nested inside the `Order` representation. Exposing it as a separate resource would leak the aggregate structure.

---

## 🔌 Step 3 — API Contract Cards

### Resource: Order

#### ➕ Create Order

| Field | Value |
|---|---|
| 🔤 **Operation** | Place a new order for the authenticated customer |
| ➡️ **Request** | `POST /orders` — Body: `{ customerId, items: [{ productId, quantity }], couponCode? }` |
| ⬅️ **Response** | `201 Created` — Body: full Order object including generated `id` and `status: PLACED` |
| ⚠️ **Error Cases** | `400` — invalid input (missing fields, quantity ≤ 0); `409` — stock unavailable; `422` — coupon invalid or not applicable |

#### 🔍 Get Order by ID

| Field | Value |
|---|---|
| 🔤 **Operation** | Retrieve a single order by its ID |
| ➡️ **Request** | `GET /orders/{id}` |
| ⬅️ **Response** | `200 OK` — Body: full Order object |
| ⚠️ **Error Cases** | `404` — order not found; `403` — caller is not the order owner or an admin |

#### 📋 List Orders for Customer

| Field | Value |
|---|---|
| 🔤 **Operation** | Retrieve all orders for a given customer |
| ➡️ **Request** | `GET /customers/{customerId}/orders?page=1&size=20` |
| ⬅️ **Response** | `200 OK` — Body: paginated list of Order summaries |
| ⚠️ **Error Cases** | `403` — caller is not the customer or an admin; `404` — customer not found |

#### ❌ Cancel Order

| Field | Value |
|---|---|
| 🔤 **Operation** | Cancel an order that has not yet been dispatched |
| ➡️ **Request** | `PATCH /orders/{id}/cancel` — no body required |
| ⬅️ **Response** | `200 OK` — Body: updated Order object with `status: CANCELLED` |
| ⚠️ **Error Cases** | `404` — order not found; `403` — caller not authorised; `409` — order already shipped or delivered and cannot be cancelled |

---

## ⚡ Event Contract Cards

| ⚡ Event | 📦 Payload | 👂 Consumers |
|---|---|---|
| `OrderPlaced` | `{ orderId, customerId, items: [{ productId, quantity, unitPrice }], total, placedAt }` | Inventory Service (reserve stock), Payment Service (initiate payment), Notification Service (send confirmation) |
| `OrderCancelled` | `{ orderId, customerId, reason, cancelledAt }` | Inventory Service (release stock), Payment Service (initiate refund if paid), Notification Service (inform customer) |
| `OrderDelivered` | `{ orderId, customerId, deliveredAt }` | Notification Service (delivery confirmation), Marketing Service (trigger post-purchase campaign) |

---

## 💡 Trainer Notes

- Groups often expose `OrderItem` as a separate resource (e.g. `GET /orders/{id}/items/{itemId}`). Challenge this: *does a consumer ever need to act on a single item independently?* If not, it should remain nested in the Order response.
- The `PATCH /orders/{id}/cancel` pattern is preferred over `DELETE /orders/{id}` — orders are never truly deleted, only transitioned to a cancelled state. This is a good discussion about REST semantics vs. domain semantics.
- Some groups will use `PUT /orders/{id}` for updates. Probe whether they mean a full replacement (PUT) or a partial update (PATCH). In most cases PATCH is correct for lifecycle transitions.
- The `customerId` in `GET /customers/{customerId}/orders` is a good entry point to discuss **who should enforce authorisation** — the API gateway or the service itself?
- Payload size in events is a recurring discussion. The `OrderPlaced` event carries enough for consumers to act without querying back — this is the **self-contained event** pattern and worth naming explicitly.
