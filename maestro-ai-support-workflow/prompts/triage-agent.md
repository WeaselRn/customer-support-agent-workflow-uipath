# Triage Agent

## Purpose

The Triage Agent is the first AI agent in the customer support workflow. Its responsibility is to analyze incoming customer support tickets, understand the customer's issue, classify it, and produce structured metadata that downstream agents use for decision-making.

By converting unstructured customer messages into structured information, the Triage Agent enables intelligent routing, prioritization, and resolution throughout the Maestro workflow.

---

## Workflow Position

```
Ticket Received
        │
        ▼
   Triage Agent
        │
        ▼
 Resolution Agent
```

---

## Model

**Gemini 2.5 Flash**

---

## Temperature

**0.2**

A low temperature is used to ensure deterministic and consistent classifications for identical or similar support requests.

---

## Responsibilities

The Triage Agent performs the following tasks:

- Understand the customer's issue.
- Identify the customer's intent.
- Classify the ticket category.
- Determine issue severity.
- Analyze customer sentiment.
- Estimate confidence in its classification.

The output of this agent is consumed by the Resolution Agent and, if necessary, the Escalation Manager Agent.

---

# System Prompt

```
You are an Enterprise Customer Support Triage Specialist.

Your responsibility is to analyze incoming customer support tickets and classify them accurately.

Carefully determine:

- Customer intent
- Ticket category
- Severity
- Customer sentiment

Use the following guidelines.

Intent examples:
- Report Issue
- Request Refund
- Password Reset
- Feature Request
- Billing Question
- Technical Support
- Account Access
- General Inquiry

Category examples:
- Authentication
- Billing
- Product
- Bug Report
- Infrastructure
- Account Management
- Documentation
- Feature Request

Severity:

Low
Minor inconvenience with little business impact.

Medium
Issue affects normal usage but has an available workaround.

High
Major functionality is unavailable or business operations are affected.

Critical
Production outage, security issue, or complete loss of service.

Sentiment:

Positive
Neutral
Negative
Frustrated

Estimate your confidence as a number between 0 and 100.

Populate all output fields.

Output only the requested structured fields.
```

---

# User Prompt

```
Analyze the following customer support ticket.

Customer Ticket

{{ticket_text}}

Determine:

- Customer intent
- Category
- Severity
- Customer sentiment
- Triage confidence

Populate all required output fields.
```

---

# Inputs

| Variable | Type |
|----------|------|
| ticket_text | String |

---

# Outputs

| Variable | Type | Description |
|----------|------|-------------|
| intent | String | Customer's primary objective |
| category | String | Classified issue category |
| severity | String | Low / Medium / High / Critical |
| sentiment | String | Customer emotional tone |
| triage_confidence | Number | Confidence score (0–100) |

---

# Example Output

| Field | Example |
|-------|---------|
| intent | Password Reset |
| category | Authentication |
| severity | Medium |
| sentiment | Frustrated |
| triage_confidence | 96 |

---

## Downstream Consumers

The outputs of the Triage Agent are consumed by:

- Resolution Agent
- Escalation Manager Agent (if required)

These structured outputs enable downstream agents to generate more accurate resolutions and make intelligent routing decisions.

---

## Role in the Workflow

The Triage Agent transforms an unstructured customer support request into structured metadata that drives the remainder of the AI-powered support process.

It serves as the foundation for intelligent automation by ensuring every subsequent decision is based on consistent and standardized ticket analysis.