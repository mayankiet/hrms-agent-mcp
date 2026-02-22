# hrms-agent-mcp

A **Model Context Protocol (MCP)**-enabled Human Resource Management System (HRMS) project that exposes HR workflows as callable tools for agentic AI assistants like Claude Desktop.

This project implements an MCP server in Python that allows AI agents to manage employees, tickets, meetings, leave balances, and send emails — all through defined MCP tools.

---

## 🚀 Features

This HRMS MCP server supports the following tool calls:

### 👩‍💼 Employee Management
- `add_employee(emp_name, manager_id, email)` — Add a new employee
- `get_employee_details(name)` — Get employee details by name

### 📨 Communication
- `send_email(to_emails, subject, body, html)` — Send email notifications

### 🎟 Ticket System
- `create_ticket(emp_id, item, reason)` — Create a service/asset request
- `update_ticket_status(ticket_id, status)` — Update ticket status
- `list_tickets(employee_id, status)` — List employee tickets

### 📅 Meetings
- `schedule_meeting(employee_id, meeting_datetime, topic)` — Schedule a meeting
- `get_meetings(employee_id)` — Get employee meetings
- `cancel_meeting(employee_id, meeting_datetime, topic)` — Cancel a meeting

### 🌴 Leave & Time Off
- `get_employee_leave_balance(emp_id)` — Get leave balance
- `apply_leave(emp_id, leave_dates)` — Apply for leave
- `get_leave_history(emp_id)` — Get leave history

### 🧠 Onboarding Prompt
- `onboard_new_employee(employee_name, manager_name)` — A prompt definition to automate common onboarding steps

---

## 🧩 Project Structure


├── .env # Environment variables (not tracked)
├── hrms # HRMS business logic
├── emails.py # Email helper logic
├── server.py # MCP server and tool definitions
├── utils.py # Utility functions
├── main.py # Entry point example script
├── pyproject.toml # Python project config
├── README.md # Project documentation
└── uv.lock # uv dependency lock



---

## ⚙️ Setup

### 1. Clone the repository

```bash
git clone https://github.com/mayankiet/hrms-agent-mcp.git
cd hrms-agent-mcp

2. Install dependencies
uv init
uv install


3.  Create .env file

Create a .env with your email credentials:

CB_EMAIL=youremail@example.com
CB_EMAIL_PWD=yourpassword


Run MCP Server

To launch the MCP server:

uv run server.py



Connect to Claude Desktop

Open Claude Desktop

Go to Settings → Developer → Edit Config

Add:

{
  "mcpServers": {
    "hrms-agent-mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "/FULL/PATH/TO/hrms-agent-mcp",
        "run",
        "server.py"
      ],
      "env": {
        "CB_EMAIL": "youremail@example.com",
        "CB_EMAIL_PWD": "yourpassword"
      }
    }
  }
}

