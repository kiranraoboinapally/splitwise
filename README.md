<h3>This is to be built!!!</h4>

---

# Splitwise Clone –  Java Full-Stack Project

## Overview

I’ll be building a simplified **Splitwise Clone** that helps users track shared expenses and determine who owes whom. The core features include group creation, expense splitting, and balance tracking.

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

   * **back/SplitWise**: Spring Boot application.
   * **front/**: React application.
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

## **Contributing to Splitwise Clone**

We appreciate your interest in contributing to the **Splitwise Clone** project! Here's how you can contribute:

### **Steps to Contribute:**

1. **Fork and Clone the Repository**

   * Fork the repository by clicking the **Fork** button on the top right of the repository page on GitHub.
   * Clone your forked repository to your local machine using:

     ```bash
     git clone https://github.com/kiranraoboinapally/splitwise.git
     ```

2. **Create a New Branch**

   * After cloning, navigate into the project directory:

     ```bash
     cd splitwise
     ```

   * **Create a new branch** for your changes:

     ```bash
     git checkout -b mod
     ```

3. **Make Your Changes**

   * Implement the desired features or fixes in the backend (Spring Boot + MySQL) or frontend (React + TailwindCSS).

4. **Stage and Commit Your Changes**

   * After making changes, stage and commit them:

     ```bash
     git add .
     git commit -m "Added feature for group creation"
     ```

5. **Push Changes to Your Fork**

   * Push your changes to your forked repository:

     ```bash
     git push origin mod
     ```

6. **Create a Pull Request (PR)**

   * Go to your forked repository on GitHub and click **Compare & Pull Request**.
   * In your PR description, include what you’ve done and link to any related issues (e.g., `Closes #2`).

7. **Wait for Review and Merge**

   * After submitting the PR, it will be reviewed and merged if everything looks good.

---

## **Assumptions and Considerations**

* **No authentication/authorization**: This project does not require user login or security.
* **No real-time updates**: The system doesn’t implement WebSocket or any real-time mechanisms.
* **No payment gateway integration**: This project is focused only on tracking shared expenses.

---

### **Thank You for Contributing!**

We appreciate your help in improving the **Splitwise Clone** project! If you have any questions or need assistance, please feel free to open an issue or contact us directly.

---
