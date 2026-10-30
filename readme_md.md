# AI-Powered Appointment Booking System

An end-to-end automated appointment scheduling and management system built using **n8n workflow automation**, **Google Gemini AI**, **Google Calendar API**, **PostgreSQL**, and **Gmail**.

This solution enables users to interact via natural language to check live calendar availability, book appointments, save structured database records, receive confirmation emails, and receive automated 24-hour advance reminders.

---

## 🛠️ System Architecture & Workflow Components

The project consists of two core n8n workflows and a PostgreSQL relational schema:

1. **`ai_appointment_assistant.json` (Main AI Agent Workflow)**
   * **Chat Trigger:** Listens for incoming natural language queries.
   * **Google Gemini AI Model:** Parses intent, extracts date/time slots, and handles multi-turn conversation memory (`Window Buffer Memory`).
   * **Google Calendar Tools:** Real-time event creation and availability checking.
   * **PostgreSQL Integration:** Stores customer records, appointment details, and unique reference codes.
   * **Gmail Notifications:** Sends instant confirmation messages to clients.

2. **`appointment_reminder_cron.json` (Background Cron Service)**
   * **Schedule Trigger:** Runs automatically on an hourly schedule.
   * **Query Engine:** Identifies confirmed appointments starting within the next 24 hours.
   * **Notification Engine:** Dispatches reminder emails via Gmail and logs activity in `notification_logs` to prevent duplicate messaging.

3. **`schema.sql` (Database Setup)**
   * Configures relational tables for `customers`, `appointments`, and `notification_logs`.

---

## 📁 Repository File Structure

```text
.
├── README.md                       # Project documentation
├── ai_appointment_assistant.json   # Primary AI agent workflow
```

---

## 🚀 Setup & Installation

### 1. Database Configuration
Execute `schema.sql` on your target PostgreSQL instance to construct the database schema:

```bash
psql -h <host> -U <user> -d <database_name> -f schema.sql
```

### 2. Workflow Import
1. Log into your **n8n** instance.
2. Navigate to **Workflows** > **Import from File**.
3. Import `ai_appointment_assistant.json` and `appointment_reminder_cron.json`.

### 3. Credential Setup
Attach your API keys and OAuth2 tokens in n8n for:
* **Google Gemini Chat Model** (Gemini API Key)
* **Google Calendar API** (OAuth2 Credentials)
* **Gmail API** (OAuth2 Credentials)
* **PostgreSQL** (Host, Database, User, Password, Port)

### 4. Activation
Toggle both imported workflows to **Published / Active** in the top right of the n8n canvas.

---

## 💬 Example Usage Prompts

* **Checking Availability:**
  > *"Hi! Are there any available slots next Friday between 10:00 AM and 2:00 PM?"*
* **Booking an Appointment:**
  > *"Book a 30-minute Web Development Consultation for Syed Rehman at example@email.com for tomorrow at 3 PM."*
* **Cancelling an Appointment:**
  > *"I need to cancel my appointment scheduled for tomorrow."*

---

## 👤 Author

**Syed Md Attah ur Rehman**
* **GitHub:** [@smattah420](https://github.com/smattah420)
* **LinkedIn:** [Syed Md Attah ur Rehman](https://www.linkedin.com/in/syed-md-attah-ur-rehman-7b7138322)

---

## 📄 License
This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).
