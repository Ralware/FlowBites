# FlowBites — Smart Ordering. Smarter Pickup.

> A capacity-aware food ordering and canteen management platform that connects customers, kitchens, payments, and pickup through one intelligent system.

## 1. Project Overview

**FlowBites** is a mobile-first food ordering and kitchen management platform designed for college canteens, food stalls, cafeterias, and small food businesses.

The platform enables customers to scan a QR code, browse a digital menu, place orders, pre-book food for a future time, make digital payments, track preparation progress, and collect their orders through secure counter verification.

Unlike conventional food ordering applications, FlowBites also considers the kitchen's workload before assigning pickup times. Vendors can configure kitchen capacity, allocate a portion of their preparation capacity to digital orders, and allow the system to distribute orders across available pickup slots.

The system aims to reduce physical queues, prevent kitchen overload, improve order accuracy, minimize waiting time, and help vendors make better operational decisions.

FlowBites provides two connected interfaces:

- **Customer Interface:** Menu browsing, ordering, pre-ordering, payments, pickup scheduling, order tracking, verification, and rewards.
- **Vendor Dashboard:** Order management, kitchen capacity configuration, pickup-slot scheduling, preparation tracking, secure handover, menu management, and analytics.

Both interfaces operate using a shared order record that connects payment, preparation, scheduling, and collection.

---

## 2. Problem Statement

During peak hours, especially college lunch breaks, canteens experience a sudden increase in customer demand.

Students often have limited time to purchase and eat their food, while kitchen staff must handle multiple tasks simultaneously.

### Major Problems

1. **Long queues:** Customers crowd around counters to place orders and make payments.
2. **Kitchen overload:** Too many orders arrive within the same short period.
3. **Unpredictable waiting times:** Customers do not know when their food will be ready.
4. **Pickup confusion:** Staff must identify which customer belongs to which prepared order.
5. **Payment disputes:** Verbal confirmations and payment screenshots can create confusion.
6. **Poor demand visibility:** Vendors lack a clear view of upcoming orders and peak-hour demand.
7. **Food wastage:** Preparing food without sufficient demand information can lead to unsold items.
8. **Operational inefficiency:** Staff must repeatedly answer questions, check payments, and coordinate handovers.

### Core Problem

Ordering, payment verification, kitchen preparation, and food collection compete for the same limited counter and staff attention.

FlowBites addresses this by coordinating the entire process through one connected digital system.

---

## 3. Proposed Solution

FlowBites separates the ordering process from physical counter operations while keeping the kitchen in control.

Customers place orders through their phones, while the system manages queue priority, pickup-slot availability, payment confirmation, and order status.

The vendor controls the available kitchen capacity, menu availability, preparation workflow, and order-release process.

### Key Objectives

- Reduce physical queues and unnecessary counter interactions.
- Introduce automatic, capacity-aware pickup scheduling.
- Support both immediate ordering and advance pre-ordering.
- Verify payments before confirming eligible orders.
- Provide real-time order status updates.
- Prevent unauthorized or duplicate food collection.
- Give vendors control over kitchen workload.
- Use historical demand to improve preparation planning.
- Support customer retention through loyalty rewards.
- Operate with existing phones and printed QR codes, without requiring dedicated kiosks.

---

## 4. Complete Feature List

### 4.1. QR-Based Ordering Without Installation

Customers scan a QR code displayed at the canteen or food stall and open the FlowBites ordering interface in their mobile browser.

**Features:**

- Unique QR codes for participating outlets.
- No mandatory application download.
- Mobile-friendly digital menu.
- Food categories, item descriptions, prices, and images.
- Quantity selection and supported customizations.
- Cart management.
- Live menu availability.
- Automatic hiding or disabling of unavailable items.
- Secure checkout.
- Access to order history and active order details.

The QR code identifies the relevant outlet and directs the customer to its ordering page.

### 4.2. Digital Menu Management

Vendors can manage their menus through the dashboard.

**Features:**

- Add, edit, and remove food items.
- Set prices and descriptions.
- Upload food images.
- Organize items into categories.
- Mark items as available or sold out.
- Configure supported customizations and add-ons.
- Update menu availability during operating hours.
- Control which items can be ordered during specific periods.

The menu displayed to customers reflects the vendor's latest published settings.

### 4.3. AI-Assisted Menu Setup

FlowBites can simplify vendor onboarding through AI-assisted menu digitization.

A vendor uploads a menu as a PDF, image, or supported spreadsheet. The system extracts the available item names, prices, and categories and converts them into an editable digital menu.

**Workflow:**

1. Upload the existing menu.
2. Extract text, item names, and prices.
3. Organize the extracted information into menu categories.
4. Flag uncertain or incomplete entries for review.
5. Allow the vendor to edit the extracted information.
6. Publish the menu only after vendor approval.

This feature reduces manual data entry while preserving the vendor's control over the final menu.

### 4.4. Immediate Ordering

Customers can order food for the earliest suitable pickup time.

**Workflow:**

1. Browse the live menu.
2. Add items to the cart.
3. Select immediate ordering.
4. View an available pickup estimate or slot.
5. Complete payment.
6. Receive order confirmation.
7. Track preparation.
8. Collect the order after verification.

Immediate ordering remains subject to menu availability, payment confirmation, and kitchen capacity.

### 4.5. Pre-Ordering and Scheduled Pickup

Customers can place orders in advance and reserve a suitable future pickup slot.

This is particularly useful for students who know when their lunch break begins or employees who have limited break periods.

**Features:**

- Schedule orders for a future pickup time.
- View available pickup slots.
- Check availability before checkout.
- Reserve capacity for confirmed pre-orders.
- Receive a confirmation with the assigned pickup time.
- Track upcoming and active orders.
- Receive notifications when the order is ready.
- Allow vendors to view and prepare upcoming orders in advance.

The system must distinguish between an order's scheduled pickup time and its preparation start time. This allows the kitchen to prepare the food at an appropriate point before collection.

### 4.6. Capacity-Based Pickup Slot Allocation

**This is one of the primary differentiating features of FlowBites.**

Every kitchen has a limited preparation capacity. Accepting too many orders for the same pickup period can cause delays even when the ordering process is digital.

FlowBites allows vendors to configure how many orders or preparation-workload units the kitchen can handle within a defined time interval.

**Vendor controls:**

- Configure pickup-slot intervals.
- Set a capacity limit for each slot.
- Allocate a percentage or portion of capacity to digital orders.
- Reserve capacity for walk-in customers.
- Set operating hours and order cut-off times.
- Adjust capacity during peak or low-demand periods.
- Pause new digital orders temporarily.
- Mark slots as full or unavailable.
- Account for existing scheduled orders.

**Automatic scheduling process:**

1. A customer submits an order.
2. The system validates item availability and payment.
3. The scheduler calculates the order's preparation workload.
4. It checks the available capacity in eligible pickup slots.
5. It considers existing orders and their preparation requirements.
6. It assigns the earliest suitable slot with sufficient capacity.
7. If the requested slot is full, the customer is offered another available slot.
8. The confirmed slot is reserved in the database.
9. The customer receives the assigned pickup time.

#### First-Come, First-Served Rule

FlowBites follows first-come, first-served priority among eligible orders within the applicable scheduling rules.

However, orders may require different preparation times. Therefore, capacity should be based on preparation workload where possible, rather than treating every order as identical.

The system must also account for already-confirmed pre-orders, item-specific preparation requirements, operating hours, and realistic pickup estimates.

Capacity reservation must occur on the server through a safe, atomic operation so that simultaneous orders cannot exceed the configured slot limit.

**Example:**

Suppose a canteen can handle 10 standard-order equivalents in a 10-minute pickup interval.

- Slot A has reached its capacity.
- Slot B has three standard-order equivalents remaining.
- Slot C has six standard-order equivalents remaining.

A new eligible order requiring two equivalents may be assigned to Slot B. An order requiring four equivalents would need another suitable slot.

These values are illustrative. Actual limits must be configured and calibrated using the kitchen's preparation times and available staff.

### 4.7. Digital Payment Verification

FlowBites integrates digital payments into the order lifecycle.

**Features:**

- Payment gateway integration.
- Server-side payment verification.
- Unique payment and order references.
- Payment confirmation through trusted gateway responses or signed webhooks.
- Prevention of duplicate payment processing.
- Payment status tracking.
- Handling of failed, pending, and successful transactions.
- Appropriate cancellation and refund workflows.

An order must not be treated as paid merely because the customer reaches a success screen or uploads a screenshot.

The backend verifies the payment before treating the order as confirmed and committing it to the normal preparation queue.

If payment remains pending, the system must not promise capacity indefinitely. Any temporary reservation should have an appropriate expiry policy.

### 4.8. Secure Pickup Verification

FlowBites ensures that prepared food is released only against a valid order.

Every confirmed order receives a unique order ID and pickup credential. Depending on the vendor's enabled verification level, the credential can include a pickup token, a short authentication code, and a QR code.

**Pickup verification checks:**

- The order belongs to the correct outlet.
- Payment has been verified.
- The pickup credential is valid and active.
- The order is eligible for collection.
- The order has not already been collected.
- The backend accepts the state transition to collected.

**Pickup workflow:**

1. The customer arrives at the designated pickup counter.
2. The customer presents the pickup QR code, token, or authentication code.
3. The vendor scans the QR code or enters the code.
4. The backend retrieves the corresponding order.
5. The system checks payment, readiness, token validity, and collection status.
6. If all checks pass, the vendor receives authorization to release the food.
7. The order is marked as collected.
8. The token is invalidated for subsequent collection attempts.

If verification fails, the system blocks the normal handover and displays an appropriate message for staff.

The system should not rely on a visual code alone. Validation must occur against the current server-side order record.

### 4.9. Real-Time Order Tracking

Customers can follow their orders without repeatedly asking canteen staff for updates.

**Order lifecycle:**

1. Payment pending.
2. Payment confirmed.
3. Scheduled or queued.
4. Preparing.
5. Ready for pickup.
6. Collected.

Additional states may include cancelled, payment failed, refunded, or delayed where appropriate.

**Features:**

- Current order status.
- Assigned pickup time.
- Preparation progress.
- Ready-for-pickup notification.
- Delay notifications when an updated estimate is available.
- Active order history.
- Completed order history.

The backend remains the source of truth for order and payment statuses. Customer interfaces display the latest valid state.

### 4.10. Vendor Order Management Dashboard

Vendors receive a browser-based dashboard for daily operations.

**Dashboard features:**

- Live incoming orders.
- Immediate-order queue.
- Upcoming pre-orders.
- Orders currently being prepared.
- Ready-for-pickup orders.
- Completed and cancelled orders.
- Pickup-slot availability.
- Kitchen capacity configuration.
- Menu availability controls.
- Payment verification status.
- Pickup verification interface.
- Sales summaries.
- Rush-hour reports.
- Customer and loyalty statistics.

The interface should prioritize actions that staff need during busy periods rather than overwhelming them with unnecessary information.

### 4.11. Kitchen Workload Management

The kitchen dashboard helps vendors organize production based on confirmed orders and their required pickup times.

**Features:**

- View orders by preparation status.
- Separate upcoming pre-orders from immediate orders.
- Display required preparation start times.
- Estimate workload for upcoming intervals.
- Identify overloaded time periods.
- Adjust future capacity where possible.
- Pause new incoming orders during exceptional conditions.
- Notify customers when delays affect promised pickup times.

Capacity management should avoid disrupting already-confirmed orders. Changes to the schedule must preserve existing commitments wherever possible and communicate material delays to customers.

### 4.12. Loyalty and Rewards

FlowBites can encourage repeat purchases through a configurable loyalty programme.

**Features:**

- Earn points on eligible purchases.
- View the current points balance.
- Track progress toward rewards.
- Redeem points for eligible items or discounts.
- Maintain a transaction ledger.
- Prevent duplicate reward credits.
- Reverse or adjust points when qualifying transactions are refunded.

**Illustrative reward configuration:**

- Every ₹100 spent earns 10 points.
- 80 points can be redeemed for a configured reward, such as a free diet Coke.

The reward values and eligible items are configurable rather than fixed platform rules.

### 4.13. Vendor Analytics and Reporting

Each completed order becomes an operational data point.

**Analytics include:**

- Total sales.
- Number of orders.
- Average order value.
- Orders per time interval.
- Peak-demand periods.
- Popular and slow-moving menu items.
- Average order-to-ready time.
- Pickup waiting time.
- Slot utilization.
- Orders completed per staff hour.
- Pre-order versus immediate-order proportions.
- Repeat-order rate.
- Payment disputes.
- Cancelled and refunded orders.
- Uncollected orders.
- Potential food-waste indicators.

These reports help vendors make better decisions about staffing, preparation batches, item availability, and capacity allocation.

### 4.14. Demand Forecasting

A future enhancement can use historical order data to estimate demand during upcoming periods.

The system may recommend:

- Expected demand by time interval.
- Likely peak periods.
- Suitable digital-order capacity.
- Preparation quantities for popular items.
- Potential staffing adjustments.
- Items that may require earlier availability updates.

Forecasts should initially serve as recommendations. Vendors retain final control over kitchen settings and food preparation.

### 4.15. Multi-Vendor and Multi-Outlet Support

FlowBites can begin with one canteen and expand to multiple food outlets.

**Features:**

- Individual vendor accounts.
- Separate menus and operating hours.
- Outlet-specific kitchen capacity.
- Independent pickup-slot schedules.
- Outlet-specific payment and order records.
- Vendor-level analytics.
- Institution-level administration.
- Multi-outlet reporting for authorized users.

Each order must remain associated with its correct vendor and outlet throughout payment, preparation, and pickup.

### 4.16. Responsible Promotions and Offers

Vendors can promote eligible food items and customer offers.

**Features:**

- Clearly labelled featured menu items.
- Vendor-funded offers.
- Campus sponsorships.
- Promotional discounts.
- Reward-linked offers.

Promotions must not interrupt checkout or obstruct the ordering process.

---

## 5. Complete Customer Workflow

The standard customer journey is as follows:

1. **Scan:** Scan the canteen's QR code.
2. **Browse:** View the live menu and item availability.
3. **Select:** Customize items and build the cart.
4. **Choose:** Select immediate ordering or pre-ordering.
5. **Schedule:** Select an available pickup slot or accept the earliest suitable assignment.
6. **Pay:** Complete the payment process.
7. **Confirm:** Receive confirmation after the backend verifies the payment.
8. **Track:** View the assigned pickup time and order status.
9. **Prepare:** The kitchen prepares the order according to the production schedule.
10. **Notify:** Receive a notification when the food is ready.
11. **Verify:** Present the pickup credential at the counter.
12. **Collect:** Receive the food after successful verification.
13. **Reward:** Receive eligible loyalty points after the qualifying transaction.

---

## 6. Complete Vendor Workflow

1. Register the canteen and configure the outlet.
2. Create the menu manually or upload it for AI-assisted extraction.
3. Review and publish the menu.
4. Configure operating hours and pickup-slot intervals.
5. Set kitchen capacity and digital-order allocation.
6. Publish available ordering slots.
7. Receive immediate orders and advance pre-orders.
8. Review confirmed orders and upcoming preparation requirements.
9. Prepare food according to the queue and scheduled workload.
10. Update order statuses.
11. Notify customers when food is ready.
12. Verify the pickup credential.
13. Release the food and mark the order collected.
14. Review sales, demand, capacity utilization, and customer retention.

---

## 7. Application Screens and Modules

### Customer Interface

| Screen | Purpose |
|---|---|
| QR Landing Page | Identify the canteen and open the menu |
| Digital Menu | Browse food items, prices, and availability |
| Cart | Review quantities, customizations, and total price |
| Ordering Mode | Choose immediate order or pre-order |
| Pickup Scheduler | View and select eligible pickup slots |
| Checkout | Review the order and initiate payment |
| Payment Result | Display verified payment and order status |
| Order Confirmation | Display order ID and pickup credentials |
| Live Tracking | View preparation and collection progress |
| Secure Pickup | Present QR code or pickup token |
| Order History | Review previous orders |
| Rewards | View points and eligible redemptions |

### Vendor Dashboard

| Screen | Purpose |
|---|---|
| Vendor Login | Authenticate authorized staff |
| Dashboard Overview | Display orders and operational indicators |
| Live Order Queue | Manage incoming and active orders |
| Pre-Order Schedule | Review upcoming orders by pickup time |
| Kitchen Capacity | Configure workload limits and allocations |
| Menu Management | Edit items, prices, categories, and availability |
| Preparation Board | Organize work by preparation status |
| Pickup Verification | Validate credentials before handover |
| Payment Records | Review transaction and payment status |
| Analytics | View sales, rush periods, and operational trends |
| Loyalty Management | Configure eligible rewards and offers |
| Outlet Settings | Manage operating hours and outlet configuration |

### Administration

An optional platform administrator interface can manage vendor onboarding, subscriptions, outlet access, system-level settings, and operational support.

---

## 8. Core System Architecture

FlowBites consists of the following components:

### Frontend

A responsive web application or Progressive Web App provides the customer ordering interface and vendor dashboard.

### Backend

The backend validates requests, applies business rules, manages orders, allocates pickup capacity, verifies payments, and controls order state transitions.

### Database

A relational database stores:

- Users and roles.
- Vendors and outlets.
- Menus and menu items.
- Orders and order items.
- Payment records.
- Pickup slots and capacity reservations.
- Preparation status.
- Pickup credentials.
- Loyalty transactions.
- Operational analytics.

### Payment Gateway

A payment gateway processes customer transactions. The backend verifies payment outcomes using trusted server-to-server confirmation mechanisms.

### Real-Time Updates

Real-time database events or a suitable notification service keep customer and vendor interfaces synchronized.

### Media Storage

A media service stores menu images and other approved vendor assets.

### Security Layer

Authentication, role-based authorization, server-side validation, database constraints, secure credential handling, and audit logs protect critical operations.

---

## 9. Recommended Technology Stack

| Component | Suggested Technology |
|---|---|
| Frontend | Next.js or React |
| User Interface | Responsive web design and PWA support |
| Backend and Database | Supabase and PostgreSQL |
| Authentication | Supabase Auth or an equivalent service |
| Real-Time Updates | Supabase Realtime or an equivalent mechanism |
| Payments | Razorpay or another suitable payment gateway |
| Menu Extraction | OCR and AI-assisted structured extraction |
| Image Storage | Cloudinary or equivalent |
| Version Control | GitHub |
| Hosting | A suitable production web-hosting platform |
| Notifications | In-app notifications and supported browser notifications |

The stack can be adapted to the team's skills, deployment requirements, and payment-gateway eligibility.

---

## 10. Essential Database Entities

The following entities provide a starting point for implementation.

### Users

Stores customer and staff account information, authentication references, and account status.

### Vendors

Stores business information, subscription details, and vendor configuration.

### Outlets

Stores outlet-specific menus, operating hours, kitchen settings, and pickup rules.

### Menu Items

Stores names, descriptions, prices, categories, availability, and preparation attributes.

### Orders

Stores order ownership, outlet, order type, total amount, scheduled pickup time, current status, and creation timestamp.

### Order Items

Stores the items, quantities, customizations, and relevant pricing associated with each order.

### Payments

Stores payment references, amounts, verification status, gateway events, and refund information.

### Pickup Slots

Stores the outlet, interval, capacity limits, reserved workload, and availability status.

### Capacity Reservations

Associates confirmed orders with reserved capacity and supports safe capacity accounting.

### Pickup Credentials

Stores a secure reference to the pickup credential, its validity, expiry where applicable, and collection state.

### Loyalty Ledger

Stores reward credits, redemptions, adjustments, and transaction references.

### Audit Events

Records important actions such as payment verification, capacity changes, order cancellation, and pickup completion.

Sensitive payment credentials and passwords must not be stored in plaintext.

---

## 11. Core Business Rules

1. An order cannot enter the normal confirmed preparation queue until its payment requirements are satisfied.
2. Each confirmed order must be associated with a valid outlet.
3. The scheduler must not intentionally exceed configured capacity.
4. A confirmed pickup slot must be reserved atomically.
5. First-come, first-served priority applies within the eligible queue and scheduling rules.
6. Preparation workload and existing commitments must be considered when assigning pickup times.
7. Vendors must be able to control menu availability and pause new incoming orders.
8. Customers must not be able to modify authoritative payment or collection statuses.
9. A pickup credential must be checked against the current backend order record.
10. An order must not be collected twice.
11. Refunds and cancellations must update relevant order, payment, and capacity records consistently.
12. Existing confirmed orders must be protected when future capacity settings change.
13. Notifications must reflect valid backend state changes.
14. Loyalty points must not be credited more than once for the same qualifying transaction.

---

## 12. Scheduling and Order Allocation Logic

The scheduling engine is the central differentiator of FlowBites.

```text
FUNCTION submit_order(cart, order_type, requested_slot):

    Validate customer and outlet
    Validate menu items and quantities
    Calculate order total
    Calculate preparation workload

    Validate payment outcome

    IF payment is not confirmed:
        Keep order unconfirmed
        Handle temporary capacity reservation safely
        RETURN payment status

    IF order_type is PRE_ORDER:
        Validate requested slot
    ELSE:
        Find earliest eligible slot

    FOR each eligible slot in scheduling order:

        Check operating hours
        Check item availability
        Check existing confirmed commitments
        Check remaining kitchen capacity
        Check preparation requirements

        IF sufficient capacity exists:

            Atomically reserve capacity
            Assign pickup slot
            Confirm order
            Add order to scheduled queue
            Notify customer

            RETURN order confirmation

    Offer next suitable available slot
    OR reject the order if no valid slot exists
```

The production implementation must handle concurrent orders, payment retries, expired payment sessions, cancellations, refunds, and preparation delays. Capacity should be released or restored through consistent backend transactions rather than client-side updates.

---

## 13. Security and Reliability

Security is essential because FlowBites handles payments and the physical release of food.

### Security Measures

- Secure authentication for customers and vendors.
- Role-based authorization.
- Server-side payment verification.
- Verified payment-gateway webhooks.
- Idempotent payment and order processing.
- Server-side capacity reservation.
- Secure, unpredictable pickup credentials.
- Duplicate-collection prevention.
- Database access policies.
- Input validation.
- Audit logs for critical operations.
- Protection against unauthorized status changes.
- Secure handling of personal information.

The pickup interface should display only the information required to verify and release the correct order.

---

## 14. Business Model

FlowBites follows a business-to-business subscription model while providing a convenient ordering experience for customers.

### Starter Plan

- QR-based menu.
- Basic ordering.
- Payment integration.
- Basic order management.

### Standard Vendor Plan

- Pre-ordering.
- Capacity-based pickup scheduling.
- Live queue management.
- Pickup verification.
- Operational reports.

### Premium Plan

- Advanced analytics.
- Demand forecasting.
- Advanced verification options.
- Multi-outlet management.
- Enhanced reporting and support.

### Additional Revenue Opportunities

- Vendor onboarding and menu digitization.
- Optional setup and configuration services.
- Clearly labelled vendor-funded promotions.
- Institution-level deployments.

Pricing should be determined after pilot testing and validation with participating vendors.

---

## 15. Implementation Roadmap

### Phase 1 — Core MVP

- QR landing page.
- Digital menu.
- Cart and checkout.
- Payment verification.
- Order records.
- Basic vendor dashboard.
- Order status updates.

### Phase 2 — Smart Scheduling

- Pre-order functionality.
- Pickup-slot configuration.
- Kitchen capacity settings.
- Digital-order capacity allocation.
- Automatic slot assignment.
- Preparation scheduling.
- Capacity conflict prevention.

### Phase 3 — Secure Pickup

- Pickup tokens.
- QR verification.
- Authentication-code verification.
- Duplicate-collection prevention.
- Ready-for-pickup notifications.
- Collection audit records.

### Phase 4 — Vendor Intelligence

- Sales dashboard.
- Rush-hour analysis.
- Slot utilization reports.
- Popular-item analysis.
- Loyalty programme.
- Refund-aware reward ledger.

### Phase 5 — Advanced Features

- AI-assisted menu extraction.
- Demand forecasting.
- Preparation recommendations.
- Multi-outlet support.
- Advanced reporting.
- Configurable vendor subscriptions.

---

## 16. Expected Impact and Success Metrics

FlowBites should be evaluated through a pilot involving one or more campus canteens.

| Metric | Objective |
|---|---|
| Average order-to-ready time | Measure preparation efficiency |
| Average pickup waiting time | Measure collection efficiency |
| Slot utilization | Evaluate capacity allocation |
| Orders exceeding promised times | Assess scheduling accuracy |
| Orders per staff hour | Measure operational productivity |
| Payment disputes | Evaluate payment clarity |
| Incorrect or duplicate handovers | Evaluate pickup security |
| Pre-order adoption | Measure scheduled-order usage |
| Unsold food and waste cost | Evaluate demand-planning improvements |
| Repeat-order rate | Measure customer retention |

Actual improvements must be established through pilot measurements rather than assumed in advance.

---

## 17. Target Users

### Students and Employees

People who need convenient food ordering and predictable pickup times during short breaks.

### Campus Canteens

Food outlets that experience heavy demand during specific periods.

### Small Food Businesses

Stalls and small restaurants that need affordable digital ordering without dedicated ordering hardware.

### Institutions

Colleges and organizations seeking better visibility into canteen operations and vendor performance.

---

## 18. Future Enhancements

Potential future features include:

- Personalized food recommendations.
- Cross-vendor loyalty programmes.
- Demand forecasting using historical orders.
- Ingredient and inventory management.
- Automated alerts for potential stock shortages.
- Better preparation-time estimation.
- More flexible cancellation and rescheduling.
- Multi-campus support.
- Accessibility and multilingual interfaces.
- Advanced institution-level analytics.

These features can be added after the core ordering, scheduling, payment, and pickup workflows are validated.

---

## 19. Final Project Summary

FlowBites is a smart food ordering and canteen management platform that connects QR-based ordering, digital payments, kitchen capacity, pickup scheduling, preparation tracking, and verified collection.

Its primary innovation is **capacity-aware pickup scheduling**. Instead of allowing unrestricted orders to accumulate for the same pickup time, the system distributes eligible orders according to kitchen capacity and preparation requirements.

Its second key feature is **pre-ordering with secure counter pickup**, which allows customers to reserve food in advance and collect it through server-verified credentials.

The platform also supports vendor dashboards, menu management, AI-assisted menu setup, real-time status updates, loyalty rewards, operational analytics, and future demand forecasting.

FlowBites is designed to start with a small campus canteen and scale to multiple outlets without requiring expensive dedicated hardware.

### Final Value Proposition

**FlowBites does more than let customers order food online. It coordinates when orders are accepted, when food is prepared, how kitchen capacity is allocated, and how the correct customer receives the correct order.**

**FlowBites — Smart Ordering. Smarter Pickup.**
