# airbnb-clone-project 

---

# 🏡 Airbnb Clone Backend

The **Airbnb Clone Backend** is designed to provide a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. This backend system powers the core functionalities of an Airbnb-like platform, ensuring seamless and secure operations for both users and hosts.

---

## 🏆 Project Goals

* **User Management:** Implement secure user registration, authentication, and profile management.
* **Property Management:** Enable creation, updating, and retrieval of property listings.
* **Booking System:** Allow users to book and manage property reservations.
* **Payment Processing:** Integrate secure payment transactions and record management.
* **Review System:** Provide functionality for users to rate and review properties.
* **Data Optimization:** Ensure efficient data retrieval and storage through database optimizations.

---

## ⚙️ Technology Stack

* **Django** – High-level Python framework for backend development.
* **Django REST Framework** – For building robust RESTful APIs.
* **PostgreSQL** – Reliable relational database for data storage.
* **GraphQL** – Flexible query language for efficient data interaction.
* **Celery** – Handles asynchronous tasks like notifications and payment processing.
* **Redis** – Caching and session management for performance optimization.
* **Docker** – Ensures consistent environments for development and deployment.
* **CI/CD Pipelines** – Automates testing and deployment of backend updates.

---


**Team Roles** 
| Role                       | Responsibilities in this Project                                                                                                                                                                                                                                                                                                    |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Backend Developer**      | Responsible for implementing the API endpoints (users, properties, bookings, payments, reviews), writing business logic, integrating authentication, and ensuring that the backend of the system works smoothly and securely.                                                                                                       |
| **Database Administrator** | Manages the design of the database schema (for example in PostgreSQL), implements indexing and optimization strategies, ensures data integrity, handles migrations and performance tuning.                                                                                                                                          |
| **DevOps Engineer**        | Handles containerisation (via Docker), deployment pipelines (CI/CD), automates infrastructure, monitoring, and ensures the backend service is scalable, reliable and maintainable (includes tasks like caching with Redis, setting up asynchronous tasks with Celery).                                                              |
| **QA Engineer**            | Ensures all backend features work as specified: tests API endpoints, validates edge-cases (bookings, payments, reviews), ensures quality and reliability of the system. This role “makes sure an application performs according to requirements… spots functional and non-functional defects.

**Technology Stack**
| Technology                      | Purpose in the Project                                                                                                                    |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Django**                      | A high-level Python web framework used to build and manage the backend logic, ensuring rapid development, security, and scalability.      |
| **Django REST Framework (DRF)** | Provides tools for creating and managing RESTful APIs that handle CRUD operations for users, properties, bookings, payments, and reviews. |
| **PostgreSQL**                  | A powerful relational database used for structured data storage, supporting advanced queries and ensuring data integrity.                 |
| **GraphQL**                     | Offers a flexible and efficient way to query and manipulate data, allowing clients to request exactly the information they need.          |
| **Celery**                      | Used for handling asynchronous and background tasks such as sending notifications, processing payments, and scheduling automated jobs.    |
| **Redis**                       | An in-memory data store used for caching, session management, and as a message broker for Celery tasks to improve performance.            |
| **Docker**                      | Containerization platform that ensures consistent environments for development, testing, and deployment across systems.                   |
| **CI/CD Pipelines**             | Automates code testing, integration, and deployment processes to maintain code quality and streamline updates to production.              |


---

## 🗄️ Database Design

The database for the **Airbnb Clone Backend** is structured to efficiently manage users, property listings, bookings, reviews, and payments. It follows a **relational model** using **PostgreSQL**, ensuring data consistency, integrity, and easy retrieval through optimized queries.

---

### 🧑‍💻 Users

**Description:** Represents both guests and hosts who interact with the platform.
**Key Fields:**

* `id` – Unique identifier for each user.
* `username` – User’s chosen display name.
* `email` – Used for authentication and communication.
* `password_hash` – Securely stored password.
* `is_host` – Boolean flag indicating if the user can list properties.

**Relationships:**

* A **user** can own multiple **properties**.
* A **user** can make multiple **bookings**.
* A **user** can write multiple **reviews**.

---

### 🏠 Properties

**Description:** Represents homes, apartments, or rooms listed by hosts.
**Key Fields:**

* `id` – Unique property identifier.
* `title` – Property name or short description.
* `description` – Detailed information about the property.
* `price_per_night` – Rental price per night.
* `host_id` – Foreign key linking to the **Users** table.

**Relationships:**

* A **property** belongs to one **user (host)**.
* A **property** can have multiple **bookings**.
* A **property** can have multiple **reviews**.

---

### 📅 Bookings

**Description:** Records reservations made by users for specific properties.
**Key Fields:**

* `id` – Unique booking identifier.
* `user_id` – References the **User** who made the booking.
* `property_id` – References the **Property** being booked.
* `check_in_date` – Start date of the booking.
* `check_out_date` – End date of the booking.
* `status` – Indicates whether the booking is confirmed, pending, or canceled.

**Relationships:**

* A **booking** belongs to one **user**.
* A **booking** belongs to one **property**.
* A **booking** can have one **payment** record.

---

### 💳 Payments

**Description:** Stores details of payments made for bookings.
**Key Fields:**

* `id` – Unique payment identifier.
* `booking_id` – Foreign key linking to the **Bookings** table.
* `amount` – Total payment amount.
* `payment_method` – e.g., credit card, PayPal, etc.
* `payment_status` – Indicates whether the payment was successful or failed.

**Relationships:**

* A **payment** belongs to one **booking**.
* Each **booking** has one corresponding **payment** record.

---

### ⭐ Reviews

**Description:** Contains user feedback and ratings for properties.
**Key Fields:**

* `id` – Unique review identifier.
* `user_id` – References the **User** who wrote the review.
* `property_id` – References the **Property** being reviewed.
* `rating` – Numeric score (e.g., 1–5).
* `comment` – Text feedback from the user.

**Relationships:**

* A **review** belongs to one **user**.
* A **review** belongs to one **property**.

---

### 🔗 Entity Relationships Summary

* **User ⇄ Property:** One-to-Many (A host can have many properties).
* **User ⇄ Booking:** One-to-Many (A user can make many bookings).
* **User ⇄ Review:** One-to-Many (A user can write many reviews).
* **Property ⇄ Booking:** One-to-Many (A property can be booked many times).
* **Property ⇄ Review:** One-to-Many (A property can have many reviews).
* **Booking ⇄ Payment:** One-to-One (Each booking has one payment record).

---
