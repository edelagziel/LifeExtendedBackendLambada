:

---

# ☁️ AWS Lambda Functions (Serverless Backend)

This directory contains the **serverless business logic** for the **LifeExtended Voting App**.
The backend is built using **Node.js** and **AWS SDK v3**, interacting directly with **DynamoDB** to ensure high performance and scalability.

---

## 📂 Core Functions

### `delete-poll`

**System Reset & Cleanup**
Handles the complete removal of a poll instance.
Acts as a **"hard reset"** mechanism by cleaning up multiple database tables simultaneously to prepare the system for a new cycle.

**Key Operations:**

* Deletes active poll config from `PollConfig`
* Scans and deletes all user records from `Votes`
* Resets counters in `Stats`

---

### `create-poll`

**Poll Initialization**
Sets up a new voting session. Validates the input and creates the initial configuration in the database.

**Key Operations:**

* Writes a new item to `PollConfig`
* Initializes vote counters to `0`

---

### `submit-vote`

**Real-Time Vote Processing**
Handles the user voting logic, ensuring **data integrity** and preventing **double-voting**.

**Key Operations:**

* Checks if user already voted *(idempotency)*
* Atomically increments vote count using `UpdateItem`
* Logs user participation

---

### `get-active-poll`

**Data Fetching**
Retrieves the current active poll status and details for the frontend application.

**Key Operations:**

* Fetches data from `PollConfig`

---

## 🛠️ Tech Stack & Libraries

* **Runtime:** Node.js 18.x / 20.x
* **Database:** AWS DynamoDB (NoSQL)
* **SDK:** `@aws-sdk/client-dynamodb`, `@aws-sdk/lib-dynamodb`
* **Architecture:** Event-driven architecture triggered via **API Gateway**

---

מוכן להדבקה ישר ל-README 👍
