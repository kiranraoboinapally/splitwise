<h3>This is to be built!!!</h4>

---

# Splitwise Clone –  Java Full-Stack Project

## Overview

Thank you for your interest in Neurix! In this assignment, we want to evaluate your creativity, coding skills, and ability to build a full-stack application. You’ll be building a simplified **Splitwise Clone** that helps users track shared expenses and determine who owes whom. The core features include group creation, expense splitting, and balance tracking.

## Core Requirements

### 1. Backend (Spring Boot + MySQL)

The backend will manage group creation, expense tracking, and balance calculation.

#### **Group Management**

* **POST /groups**: Create a new group with a name and a list of user IDs.
* **GET /groups/{group\_id}**: Retrieve details of a group (name, users, total expenses).

#### **Expense Management**

* **POST /groups/{group\_id}/expenses**: Add a new expense to a group.

  * **Input:** description, amount, paid\_by (user\_id), split\_type (equal or percentage), splits.
  * Support two split types:

    * **Equal**: Split the amount equally among group members.
    * **Percentage**: Split the amount based on the percentages provided for each member.

#### **Balance Tracking**

* **GET /groups/{group\_id}/balances**: View who owes whom in a group.
* **GET /users/{user\_id}/balances**: View the balance summary for a specific user across all groups.

#### **Notes:**

* **No authentication/authorization required.**
* **No payment/settlement functionality.**
* Use **MySQL** as the database for persistence.
* Use **Spring Data JPA** or any other ORM of your choice to interact with the database.

---

### 2. Frontend (React + TailwindCSS)

The frontend will interact with the backend APIs to provide a clean, user-friendly interface.

#### **Key Features:**

* Create a group with a list of users.
* Add expenses to the group with equal or percentage-based splits.
* View a summary of group balances (who owes whom).
* View a personal balance summary for a user.

The UI should be designed with **TailwindCSS** and should interact with the backend APIs to fetch and display the relevant data.

---

### 3. Bonus (Optional): LLM-Powered Chatbot

Enhance the user experience by adding an AI chatbot that can interpret natural language queries related to expenses and balances.

#### **Example Queries:**

* “How much does Alice owe in group *Goa Trip*?”
* “Show me my latest 3 expenses.”
* “Who paid the most in *Weekend Trip*?”

#### **Implementation Tips:**

* Integrate with an LLM (e.g., OpenAI or HuggingFace API).
* Send user queries along with relevant data from the database to the LLM.
* Display the chatbot’s response cleanly within the app.

---

## Deliverables

1. **GitHub Repository** with the following structure:

   * **backend/**: Spring Boot application.
   * **frontend/**: React application.
   * **docker-compose.yml**: To set up and run the full stack locally.

2. **README.md** with:

   * Detailed setup and run instructions.
   * API documentation (either OpenAPI or manually listed endpoints).
   * Any assumptions or decisions made during development.

---

## Setup Instructions

### Backend Setup (Spring Boot)

1. Clone the repository.
2. Navigate to the **backend/** directory.
3. Build the Spring Boot project using Maven or Gradle:

   ```bash
   mvn clean install
   ```
4. Configure your **application.properties** or **application.yml** with MySQL connection details.
5. Run the Spring Boot app:

   ```bash
   mvn spring-boot:run
   ```
6. The backend will be available at **[http://localhost:8080](http://localhost:8080)**.

### Frontend Setup (React)

1. Clone the repository.
2. Navigate to the **frontend/** directory.
3. Install dependencies:

   ```bash
   npm install
   ```
4. Start the React app:

   ```bash
   npm start
   ```
5. The frontend will be available at **[http://localhost:3000](http://localhost:3000)**.

### Full Stack Setup with Docker

1. Ensure Docker is installed and running on your machine.
2. Clone the repository.
3. Run the following command to set up the full stack:

   ```bash
   docker-compose up
   ```
4. The full stack will be available at:

   * Backend: **[http://localhost:8080](http://localhost:8080)**
   * Frontend: **[http://localhost:3000](http://localhost:3000)**

---

## API Documentation

### **Group Management**

* **POST /groups**
  **Body:**

  ```json
  {
    "name": "Group Name",
    "users": [1, 2, 3]
  }
  ```

  **Response:**

  ```json
  {
    "group_id": 1,
    "name": "Group Name",
    "users": [1, 2, 3],
    "total_expenses": 0
  }
  ```

* **GET /groups/{group\_id}**
  **Response:**

  ```json
  {
    "group_id": 1,
    "name": "Group Name",
    "users": [1, 2, 3],
    "total_expenses": 100
  }
  ```

### **Expense Management**

* **POST /groups/{group\_id}/expenses**
  **Body:**

  ```json
  {
    "description": "Dinner",
    "amount": 100,
    "paid_by": 1,
    "split_type": "equal",
    "splits": [33, 33, 34]
  }
  ```

  **Response:**

  ```json
  {
    "expense_id": 1,
    "group_id": 1,
    "description": "Dinner",
    "amount": 100,
    "paid_by": 1,
    "splits": [33, 33, 34]
  }
  ```

### **Balance Tracking**

* **GET /groups/{group\_id}/balances**
  **Response:**

  ```json
  {
    "balances": [
      {"user_id": 1, "amount": 33},
      {"user_id": 2, "amount": -33},
      {"user_id": 3, "amount": 0}
    ]
  }
  ```

* **GET /users/{user\_id}/balances**
  **Response:**

  ```json
  {
    "balances": [
      {"group_id": 1, "amount": 33},
      {"group_id": 2, "amount": -20}
    ]
  }
  ```

---

## Assumptions and Considerations

* **No authentication/authorization**: The system does not require user login or security, as it’s meant to focus purely on expense tracking.
* **No real-time updates**: The system does not implement WebSocket or any real-time mechanisms for instant balance updates.
* **No payment gateway integration**: This clone focuses only on expense tracking; no actual payment or settlement is involved.

---
