# Master README for Banking Microservices

# Microservices Banking System

## Overview

This project implements a banking system using microservices architecture with Spring Boot. It includes separate services for users, accounts, transactions, notifications, API Gateway, and service discovery.

## Microservices

1. **User Service** → Handles authentication, registration, roles, and email notifications.
2. **Account Service** → Manages bank accounts and balances.
3. **Transaction Service** → Handles deposits, withdrawals, transfers, and transaction logs.
4. **Notification Service** → Sends email notifications for transactions and login attempts.
5. **API Gateway** → Routes requests to the correct microservice and performs JWT authentication.
6. **Discovery Server** → Registers all services for dynamic service discovery.

## Technologies Used

* Java 17, Spring Boot
* Spring Security with JWT
* Spring Data JPA, PostgreSQL
* Spring Boot Starter Mail
* Spring Cloud Gateway, Eureka Server
* RabbitMQ (optional for async notifications)
* Maven

## Features

* JWT-based authentication
* Role-based access (ADMIN / USER)
* CRUD operations for accounts and transactions
* Transaction history retrieval
* Email notifications on transactions and login events
* API Gateway for centralized routing
* Service discovery via Eureka
* Optional async messaging via RabbitMQ

## Architecture Diagram

```
Client → API Gateway → [User, Account, Transaction, Notification Services] → PostgreSQL
                          ↑
                   Eureka Discovery
```

## Deployment

* Each microservice can be **dockerized**.
* Services can run independently and scale horizontally.
* API Gateway and Discovery Server must run before other services.

## Repository Structure (if using monorepo)

```
banking-system/
├─ user-service/
├─ account-service/
├─ transaction-service/
├─ notification-service/
├─ api-gateway/
└─ discovery-server/
```

* Each service has its **own README**, database, and configuration.

## Getting Started

1. Clone each repository (or monorepo).
2. Configure database settings in `application.yml`.
3. Start Eureka Discovery Server.
4. Start API Gateway.
5. Start all microservices.
6. Use Postman to test endpoints or implement a front-end UI.

---

# Individual Service READMEs

## 1. User Service

### Description

Handles user registration, login, authentication, and role management (USER/ADMIN).

### Technologies

* Java 17, Spring Boot
* Spring Security (JWT)
* Spring Data JPA
* PostgreSQL
* Spring Boot Starter Mail
* Maven

### Features

* Register new users
* Login with JWT token
* Role-based access control (ADMIN/USER)
* Email notifications for registration and login alerts

### Endpoints

* `POST /auth/register` → Register user
* `POST /auth/login` → Login and get JWT token

### Database Schema

* **users**

  * id: UUID
  * username: String
  * password: String (hashed)
  * role: String
  * email: String

## 2. Account Service

### Description

Manages bank accounts and balances linked to users.

### Technologies

* Java 17, Spring Boot
* Spring Data JPA
* PostgreSQL
* Maven

### Features

* Create, update, delete accounts
* Fetch account details
* Manage balance per user

### Endpoints

* `POST /accounts` → Create account
* `GET /accounts/{id}` → Get account details
* `PUT /accounts/{id}` → Update account
* `DELETE /accounts/{id}` → Delete account

### Database Schema

* **accounts**

  * id: UUID
  * userId: UUID
  * accountNumber: String
  * balance: Decimal

## 3. Transaction Service

### Description

Handles deposits, withdrawals, and transfers between accounts.

### Technologies

* Java 17, Spring Boot
* Spring Data JPA
* PostgreSQL
* RabbitMQ (optional)
* Maven

### Features

* Deposit funds
* Withdraw funds
* Transfer funds between accounts
* Fetch transaction history
* Event publishing for notifications

### Endpoints

* `POST /transactions/deposit`
* `POST /transactions/withdraw`
* `POST /transactions/transfer`
* `GET /transactions/{accountId}` → Transaction history

### Database Schema

* **transactions**

  * id: UUID
  * accountId: UUID
  * type: ENUM (DEPOSIT, WITHDRAW, TRANSFER)
  * amount: Decimal
  * timestamp: DateTime

## 4. Notification Service

### Description

Sends email and optional SMS notifications for account and transaction events.

### Technologies

* Java 17, Spring Boot
* Spring Boot Starter Mail
* Maven

### Features

* Send email on successful transaction
* Send email on failed login attempts
* Send email after multiple failed login attempts
* Can extend to SMS notifications

### Endpoints

* `POST /notifications/email`

## 5. API Gateway

### Description

Routes all incoming requests to the appropriate microservice and handles authentication.

### Technologies

* Java 17, Spring Boot
* Spring Cloud Gateway
* Eureka Discovery Client
* Maven

### Features

* Central entry point for all client requests
* JWT validation filter
* Route requests to respective microservices
* Can implement rate limiting or throttling

## 6. Eureka Discovery Server

### Description

Service registry for microservices. All services register here for discovery.

### Technologies

* Java 17, Spring Boot
* Eureka Server
* Maven

### Features

* Service registration and discovery
* Helps API Gateway and other microservices locate each other

### Setup

* Annotate main class with `@EnableEurekaServer`
* Configure `application.yml` with service port and Eureka settings
