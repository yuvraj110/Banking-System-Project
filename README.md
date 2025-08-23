# 🏦 Banking System Project

## 📌 Overview

A **Banking System** backend built with **Java Spring Boot** that demonstrates enterprise-level architecture, including **ACID transactions**, **JWT authentication**, **cloud integrations** (Blob Storage + Service Bus), and **advanced backend features** like pagination, filtering, file handling, and Excel export.

This project is designed to showcase **real-world backend engineering skills** for interviews and portfolio building.

---

## ⚙️ Tech Stack

* **Backend:** Java 17, Spring Boot
* **Database:** PostgreSQL/MySQL (ACID compliance)
* **ORM:** Hibernate/JPA
* **Authentication:** Spring Security with JWT
* **File Handling:** Apache POI (Excel), Multipart Upload
* **Cloud:**

  * Blob Storage (AWS S3 / Azure Blob)
  * Service Bus / Queue (AWS SQS / Azure Service Bus / RabbitMQ)
* **Deployment:** AWS Free Tier (Elastic Beanstalk / EC2 + RDS + S3)
* **Version Control:** GitHub/GitLab

---

## 🔑 Features

* **User Management** → Registration, Login, JWT Auth, Roles (Admin, Teller, Customer).
* **Account Management** → Create, Update, Delete, View Accounts.
* **Transactions** → Deposit, Withdraw, Transfer (ACID guarantees).
* **Filtering & Pagination** → On transactions and accounts.
* **Excel Export (Apache POI)** → Download transaction history.
* **File Upload** → KYC documents and bulk transaction Excel files.
* **Event-driven Architecture** → Service Bus integration for async processing.
* **Cloud Storage Integration** → Upload & retrieve files from Blob.

---

## 📂 File Handling with Blob + Service Bus

1. **File Upload to Blob Storage**

   * Users upload files (e.g., KYC docs, transaction batches).
   * Files are stored securely in **Blob Storage (S3/Azure Blob)**.

2. **Trigger + Service Bus**

   * Once uploaded, a **Service Bus / Queue event** is generated.
   * A background service listens to this event.

3. **Processing**

   * The background service fetches the file from **Blob**.
   * Runs a small **validation check** (e.g., format, fields, size).

4. **File Download**

   * After validation, users can **download the processed file**.
   * Ensures **asynchronous & reliable processing**.

---

## 📊 ACID Demonstration

* **Atomicity** → Transactions roll back on failure.
* **Consistency** → Balance never goes negative unless overdraft enabled.
* **Isolation** → Two concurrent transfers don’t interfere.
* **Durability** → Committed data persists even after crash.

---

## 🔗 UI Template

For frontend, we’ll use a **free banking dashboard template**:
👉 [Free Banking Dashboard UI](https://www.creative-tim.com/templates/react) (or similar React template).

---

## 📌 API Endpoints (Sample)

### Auth

* `POST /auth/register`
* `POST /auth/login`

### Accounts

* `POST /accounts`
* `GET /accounts/{id}`
* `GET /accounts?page=&size=` (pagination)

### Transactions

* `POST /transactions/deposit`
* `POST /transactions/withdraw`
* `POST /transactions/transfer`
* `GET /transactions/filter?fromDate=&toDate=&type=`

### File Handling

* `POST /files/upload` → Upload to Blob
* `GET /files/{id}/download` → Download from Blob after validation

---

## 🚀 Deployment Plan

1. Local development with PostgreSQL/MySQL.
2. Containerize (Docker).
3. Deploy to AWS Free Tier:

   * Backend → Elastic Beanstalk / EC2
   * Database → RDS
   * File Storage → S3
   * Queue → SQS

---

## 🏆 Why This Project?

✔️ Demonstrates **real-world enterprise design**.
✔️ Covers **backend + cloud + security**.
✔️ Uses **ACID principles** with SQL.
✔️ Shows **resume-ready advanced features** like event-driven design, blob storage, and file handling.

---
