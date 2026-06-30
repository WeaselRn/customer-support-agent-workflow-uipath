# Learning Agent

## Purpose

The Learning Agent is the final component of the AI-powered customer support workflow.

Its responsibility is to transform every successfully resolved customer support ticket into structured organizational knowledge. By capturing verified resolutions as reusable knowledge base articles, the Learning Agent enables continuous learning, improves future support quality, and reduces resolution time for similar issues.

This agent ensures that every completed support interaction contributes to a growing enterprise knowledge repository.

---

## Workflow Position

```
Deliver Customer Response
          │
          ▼
     Learning Agent
          │
          ▼
         End
```

---

## Model

**Gemini 2.5 Flash**

---

## Temperature

**0.3**

A slightly higher temperature is used to generate well-structured, readable documentation while maintaining factual consistency.

---

## Responsibilities

The Learning Agent performs the following tasks:

- Analyze the resolved customer support ticket.
- Summarize the problem.
- Identify the verified root cause.
- Capture the final resolution.
- Generate searchable keywords.
- Produce a structured knowledge base article in Markdown format.

The Learning Agent does not interact with customers. Its purpose is to improve organizational knowledge and support future automation.

---

# System Prompt

```
You are an Enterprise Knowledge Management Specialist.

Your responsibility is to convert successfully resolved customer support tickets into high-quality knowledge base articles.

Analyze the complete support case and generate reusable documentation that can help resolve similar issues in the future.

The knowledge article should include:

- A concise and descriptive title.
- A summary of the customer's problem.
- The verified root cause.
- The confirmed resolution.
- Relevant search keywords.
- A well-structured Markdown knowledge base article.

The article should be clear, technically accurate, and easy for support engineers to search and understand.

Do not invent information that is not supported by the resolved case.

Populate all output fields.

Output only the requested structured fields.
```

---

# User Prompt

```
Review the completed customer support case.

Customer Ticket

{{ticket_text}}

Final Customer Response

{{final_response}}

Generate a reusable knowledge base article based on this resolved issue.

Populate all required output fields.
```

---

# Inputs

| Variable | Type |
|----------|------|
| ticket_text | String |
| final_response | String |

---

# Outputs

| Variable | Type | Description |
|----------|------|-------------|
| kb_title | String | Knowledge base article title |
| problem_summary | String | Summary of the customer issue |
| root_cause | String | Verified root cause |
| resolution | String | Final verified resolution |
| keywords | String | Search keywords |
| article_markdown | String | Complete knowledge base article |

---

# Example Output

| Field | Example |
|-------|---------|
| kb_title | Resolving Expired Authentication Token Login Failures |
| problem_summary | Customers were unable to log in due to expired authentication tokens. |
| root_cause | Authentication session expired because of an invalid access token. |
| resolution | Clear cached credentials, reauthenticate the user, and issue a new authentication token. |
| keywords | authentication, login, token, expired session, account access |
| article_markdown | # Resolving Expired Authentication Token Login Failures... |

---

## Downstream Consumers

The outputs of the Learning Agent are intended for:

- Enterprise Knowledge Base
- Internal Support Documentation
- Future AI-assisted support workflows
- Organizational knowledge repositories

Although the current implementation generates the knowledge article, future versions of the solution can automatically store and retrieve these articles to improve AI-assisted resolution of similar tickets.

---

## Role in the Workflow

The Learning Agent enables continuous organizational learning by converting every resolved customer support interaction into reusable knowledge.

Instead of ending the workflow after resolving a ticket, the solution captures verified resolutions as structured knowledge base articles. This creates a growing repository of institutional knowledge that can improve future support operations, increase automation accuracy, and reduce resolution times over time.