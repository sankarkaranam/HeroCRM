# HeroCRM

* SaaS-level (your company) **Admin Dashboard & Management System**
* **Multi-tenant dealer model** with license/subscription control
* **Attractive UI/UX + modern frontend structure**
* **AI-driven insights** (leads, sales, issues, renewals, etc.)
* Full inclusion of **campaigns, customer reminders, and automation** (birthday, anniversary, vehicle service)
* **Support/bugs/ticket management**
* **Dealer → Supervisor → Staff** hierarchy
* **Scalable SaaS infra (auth, billing, analytics)**

Let’s rebuild this document as a **professional SaaS Product Specification**
for **“AutoServe 360”** — *(combined Honda CRM + POS Billing SaaS platform)*
that includes everything from the previous document plus the SaaS layer, user experience improvements, and automation logic.

---

# **AutoServe 360 — Complete SaaS Product Specification Document**

### **Product:**

**AutoServe 360** — Multi-Dealer CRM, Vehicle Service Manager, and POS SaaS Platform
(Modules: Biryani Billing, Honda CRM)

### **Version:** 1.0

### **Author:** Sankar Karanam

### **Date:** October 26, 2025

### **Purpose:**

This document defines every page, data structure, role, logic, automation, API, license, and UX rule for the **AutoServe 360 SaaS** — a cloud-based CRM + POS system for businesses like bike dealers and restaurants.

---

## **Table of Contents**

1. SaaS Overview
2. SaaS-Level Admin Panel (Main Dashboard)
3. Users, Roles, & Hierarchy
4. UI/UX Design Principles
5. Page-by-Page Modules

   * A. Global Dashboard (SaaS Super Admin)
   * B. Dealer Dashboard
   * C. POS / Billing
   * D. CRM / Leads
   * E. Vehicles & Service Jobs
   * F. Campaigns & Customer Engagement
   * G. Inventory & Stock
   * H. Reports & Analytics
   * I. Ticketing & Support
   * J. Settings & Licensing
   * K. Import / Data Mapping
6. AI & Automation Features
7. License, Subscription, & Payment Flow
8. Data Model (Core Tables)
9. API Endpoints
10. Validation Rules & Business Logic
11. Security, Backup, and Compliance
12. Deployment & Tech Stack
13. Deliverables & Next Steps

---

## **1. SaaS Overview**

### **Business Model**

AutoServe 360 operates as a **SaaS (Software-as-a-Service)** platform:

* Dealers or Businesses **subscribe online** to monthly/annual plans.
* After payment, a **License Key & Tenant Space** are auto-created.
* Each dealer operates independently under a secure tenant.
* SaaS Admin can view all dealers, revenue, usage, tickets, and analytics.

### **Subscription Plans**

| Plan           | Target                 | Features                                  | Price Range |
| -------------- | ---------------------- | ----------------------------------------- | ----------- |
| **Starter**    | Small outlets          | Basic Billing, Customer CRM               | ₹999/mo     |
| **Pro**        | Dealers (1–3 branches) | Full CRM + Campaigns + Service Tracking   | ₹2999/mo    |
| **Enterprise** | Multi-dealer           | Multi-branch, API Access, Custom Branding | ₹7999/mo    |

---

## **2. SaaS-Level Admin Panel (Main Dashboard)**

### **Purpose**

Used by your company (AutoServe 360 HQ) to monitor, control, and support all subscribed dealers.

### **Key Widgets**

| Widget                     | Description                                              |
| -------------------------- | -------------------------------------------------------- |
| **Active Dealers**         | Total number of registered dealers                       |
| **Active Licenses**        | Count, expiry summary (30d, 60d, expired)                |
| **Total Users**            | Across all dealers                                       |
| **Revenue Summary**        | Monthly Recurring Revenue (MRR), ARR, per-plan breakdown |
| **New Leads / Trials**     | Dealers who signed up but not activated                  |
| **Support Tickets**        | Open, in-progress, resolved                              |
| **System Errors / Bugs**   | Tracked by monitoring API                                |
| **WhatsApp Messages Sent** | Count, delivery rate, per dealer                         |
| **Storage Usage**          | Dealer-wise data & backup size                           |
| **Service Reminders Sent** | per day/week/month analytics                             |

### **Pages & Menus**

1. **Dashboard (Main)** — All widgets above
2. **Dealers Management**

   * List of all dealers: name, contact, license, plan, expiry, revenue, active users, storage used
   * Actions: Suspend / Extend / Upgrade / View Dealer Dashboard
3. **Revenue & Billing**

   * Total income by plan
   * Payment gateway integration summary (Stripe/Razorpay)
   * Renewals and overdue accounts
4. **Tickets / Support**

   * Support dashboard with issue category, dealer, priority
   * SLA tracking & auto-escalation
5. **Bug Tracker**

   * Error logs from backend, grouped by module
   * Assigned to dev teams
6. **Communication**

   * Send broadcast messages to all dealers (updates, downtime, offers)
7. **Analytics**

   * Heatmaps: active time, page usage, message delivery performance
   * Retention reports: trial → paid conversions, churn analysis

### **SaaS Admin Actions**

* Generate License
* Assign Plans
* Suspend Dealer
* Send Global Notification
* Manage API Keys
* Download System Reports

---

## **3. Users, Roles & Hierarchy**

### **Top Hierarchy**

```
SaaS Super Admin (Your Company)
     ↳ Dealers (each with unique license)
          ↳ Dealer Admin
               ↳ Supervisors (limited)
                    ↳ Cashiers / Technicians / Sales Execs
                         ↳ Customers (external)
```

### **New Roles**

| Role                     | Description                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| **Supervisor**           | Dealer-assigned limited access user (view dashboards, manage team) |
| **Ticket Agent**         | Can handle dealer support queries                                  |
| **Developer (internal)** | Access bug logs, API monitoring                                    |
| **Customer (portal)**    | Can view their invoices, reminders, vehicle service history        |

---

## **4. UI / UX Design Principles**

* **Frontend Framework:** React + Tailwind CSS + Framer Motion
* **Design Approach:** Modern, clean, minimal with rounded cards and consistent spacing
* **Theme:** Dark-light toggle, dealer branding (logo, colors)
* **Key Traits:**

  * Zero learning curve UX
  * Smooth animations for transitions
  * Dashboard cards with real-time numbers
  * Mobile-responsive (PWA support)
  * Accessibility-friendly (WCAG AA)
* **Core Pages Shared Layout:**
  Header → Sidebar Navigation → Content Cards → Right Drawer (Quick Actions)

---

## **5. Page-by-Page Modules**

Below is the modular breakdown for both **SaaS Dashboard** and **Dealer Dashboards**.

---

### **A. Global Dashboard (SaaS Super Admin)**

**KPIs:**

* Total Dealers: 128
* Active Users: 4,521
* Total Revenue (MTD): ₹7.4L
* Expiring Licenses: 23
* Trial Conversions: 42%
* Open Tickets: 17

**Graphs:**

* MRR / ARR Trend
* Dealer Signups by Month
* Ticket Volume by Module
* Feature Usage Analytics (e.g., % of dealers using Campaigns)

**Actions:**

* Add Dealer
* Send Notification
* Extend License
* Export Revenue Report

---

### **B. Dealer Dashboard**

**KPIs:**

* Today’s Sales, Today’s Jobs, Pending Payments
* Total Customers, Active Vehicles
* Upcoming Reminders (Birthdays, Service Due)
* WhatsApp Delivery Summary
* Open Jobs by Technician

**Widgets:**

* Bar: Monthly Sales Trend
* Pie: Service vs Parts Revenue
* Line: Customer Growth over time
* Alerts: License expiry, stock low, pending renewals

---

### **C. POS / Billing (Dealer Module)**

*(Same as before, with improved visuals and shortcut keys)*

Additions:

* Customer loyalty points
* Auto-whatsapp invoice
* QR-based payment
* Integration with printer APIs

---

### **D. CRM / Leads**

Enhancements:

* AI-based lead scoring
* Smart follow-up suggestions
* Lead source tracking (campaign, website, referral)
* WhatsApp button integration for quick contact

---

### **E. Vehicles & Service Jobs**

Added automation:

* Smart reminder logic (km or months)
* Customer receives auto message:
  “Your vehicle {reg_no} is due for service on {date}”
* Service History Portal (with public link + QR code on invoice)
* Predictive Maintenance Alerts (AI-based on usage patterns)

---

### **F. Campaigns & Customer Engagement**

**Automatic Messages**

* Birthdays 🎂
* Anniversaries 💍
* Vehicle Purchase Anniversary 🚗
* Festivals 🎉 (Deepavali, Ugadi, Pongal, etc.)
* Service Reminders 🔧
* Feedback after service ⭐

**Campaign Dashboard:**

* Message Queue Stats
* Click-through rate
* Auto Scheduling Templates
* WhatsApp message preview

**Smart Filters:**

* “Customers not visited in 90 days”
* “Vehicles due for service this week”
* “Customers with same model”

---

### **G. Inventory & Stock**

Additions:

* Barcode / QR-based stock adjustments
* Multi-warehouse support for multi-branch dealers
* AI reorder suggestions (based on usage rate)

---

### **H. Reports & Analytics**

New reports for SaaS level:

* Dealer Revenue Summary
* Dealer Usage (API, storage, messages)
* License Expiry Heatmap
* Feature Adoption Report

Dealer level:

* MTD/YTD sales
* Service turnaround time
* Campaign ROI

---

### **I. Ticketing & Support**

**Purpose:** Dealers can report issues, feature requests, and bugs.

**Modules:**

* Create Ticket (category: bug/feature/billing)
* Priority: Low/Med/High
* Auto-assign to internal agent
* Attach screenshots or logs
* Comment thread + internal notes

**Workflow:**
Dealer → Ticket → Agent → Resolution → Dealer Feedback

---

### **J. Settings & Licensing**

**For Dealers:**

* Profile (GST, address, logo)
* Subscription plan details
* License key & expiry
* Payment history
* API keys
* Dealer user management (Admin → Supervisor → Staff)

**For SaaS Admin:**

* Issue new license
* Upgrade plan
* Disable dealer
* Monitor API calls
* View payment gateway logs

---

### **K. Import / Data Mapping**

(As previously detailed — includes AI mapping & validation UI)

Enhancement:
Add **Dealer-to-SaaS import** — SaaS Admin can bulk import dealer records or migrate from Excel/legacy systems.

---

## **6. AI & Automation Features**

| Feature                      | Description                                          |
| ---------------------------- | ---------------------------------------------------- |
| **AI Column Mapping**        | Auto-recognize Excel import fields                   |
| **Predictive Maintenance**   | Suggest next service dates using previous kms        |
| **Lead Scoring**             | Rank leads using activity + engagement data          |
| **Sentiment Tracking**       | Analyze feedback and complaints                      |
| **Auto Campaign Generation** | Recommend best time to send birthday/offers          |
| **Anomaly Detection**        | Alert when sales drop or stock depletes unexpectedly |

---

## **7. License, Subscription & Payment Flow**

### **Flow**

1. Dealer signs up → chooses plan → pays via Stripe/Razorpay
2. System creates:

   * Dealer record
   * License key (auto-expiry)
   * Activation email with credentials
3. Dealer activates → assigns users → starts using app
4. Renewal reminders: 30, 15, 7 days before expiry

### **License Table**

| Field         | Description            |
| ------------- | ---------------------- |
| key           | Encrypted string       |
| dealer_id     | Link to dealer         |
| plan          | Starter/Pro/Enterprise |
| expires_on    | Expiry date            |
| allowed_users | Limit                  |
| status        | active/suspended       |
| storage_limit | in MB                  |

---

## **8. Data Model (Extended)**

Additions:

* **tickets** (id, dealer_id, subject, priority, status, assigned_to, comments[])
* **payments** (id, dealer_id, amount, currency, mode, invoice_url, paid_on)
* **plans** (id, name, price, features[])
* **dealer_metrics** (dealer_id, total_sales, total_messages, uptime, storage_used)
* **saas_notifications** (id, title, message, target_audience, created_at)

---

## **9. API Endpoints (SaaS Additions)**

```
POST /api/saas/dealers       # Create dealer
GET  /api/saas/dealers       # List all dealers
GET  /api/saas/dealers/{id}  # Dealer details + license info
POST /api/saas/licenses      # Issue new license
GET  /api/saas/revenue       # Revenue analytics
GET  /api/saas/tickets       # All tickets across dealers
POST /api/saas/notifications # Send broadcast
```

---

## **10. Validation Rules & Business Logic (Additions)**

* Dealer must have valid license token before API access.
* License verification cached locally (renew every 24h).
* Supervisor cannot delete records or modify license.
* Customers auto-added from POS can’t be deleted if linked to vehicles.
* System auto-sends campaign only if consent=true.
* For expired license → show grace notice (read-only mode).

---

## **11. Security, Backup & Compliance**

* Multi-tenant DB with tenant_id isolation.
* Encryption (AES-256) for sensitive data.
* RBAC enforced via middleware.
* Daily encrypted backups.
* 2FA for Admin users.
* Activity audit trail for every CRUD action.
* GDPR/DPDP compliance for Indian users (data deletion/export support).

---

## **12. Deployment & Tech Stack**

| Layer      | Tech                                           |
| ---------- | ---------------------------------------------- |
| Frontend   | React + Tailwind + Recharts + Framer Motion    |
| Backend    | Node.js (NestJS / Express) or Python (FastAPI) |
| DB         | PostgreSQL + Redis (cache)                     |
| Queue      | BullMQ (Redis)                                 |
| Storage    | AWS S3 / DigitalOcean Spaces                   |
| Auth       | JWT + Refresh Tokens                           |
| Payments   | Razorpay / Stripe                              |
| Monitoring | Prometheus + Grafana                           |
| CI/CD      | GitHub Actions + Docker                        |
| Hosting    | AWS ECS / Vercel / Render                      |

---

## **13. Deliverables & Next Steps**

✅ Full SaaS Spec — *This Document*
⬜ OpenAPI Spec for APIs
⬜ Database Migrations
⬜ React Wireframes (SaaS & Dealer dashboards)
⬜ License Microservice Implementation
⬜ Campaign Automation Worker
⬜ Import/AI Mapping UI
⬜ QA Checklist
⬜ Deployment Architecture Diagram

---

Would you like me to now:

1. **Generate the SaaS Admin Dashboard UI wireframe (React + Tailwind component layout)**,
2. Or **create database schema SQL (PostgreSQL)** for all SaaS + Dealer tables?

You can pick one and I’ll build it next.
