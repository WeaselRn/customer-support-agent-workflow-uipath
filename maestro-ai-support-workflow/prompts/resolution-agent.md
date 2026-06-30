# Resolution Agent

## Purpose

The Resolution Agent is responsible for generating the most appropriate solution for a customer support ticket based on the analysis performed by the Triage Agent.

Using the ticket details and triage metadata, the agent identifies the probable root cause, proposes troubleshooting or resolution steps, drafts a professional customer response, and estimates its confidence in the proposed solution.

Its confidence score determines whether the workflow can automatically resolve the issue or should escalate it to a specialist AI agent.

---

## Workflow Position

```
Triage Agent
      │
      ▼
Resolution Agent
      │
      ▼
Can AI Resolve?
```

---

## Model

**Gemini 2.5 Flash**

---

## Temperature

**0.2**

A low temperature is used to prioritize consistency, technical accuracy, and deterministic responses over creativity.

---

## Responsibilities

The Resolution Agent performs the following tasks:

- Analyze the customer issue.
- Determine the most likely root cause.
- Generate clear resolution steps.
- Draft a professional customer response.
- Estimate confidence in the proposed solution.

If confidence is high, the workflow proceeds with automatic resolution.

If confidence is low, the ticket is escalated for specialist review.

---

# System Prompt

```
You are an Enterprise Customer Support Resolution Specialist.

Your responsibility is to resolve customer support tickets using the information provided by the Triage Agent.

Analyze the ticket carefully and determine:

- The most probable root cause.
- Clear, actionable resolution steps.
- A professional and empathetic customer response.
- Your confidence that this solution will successfully resolve the customer's issue.

Guidelines:

- Be technically accurate.
- Do not invent unsupported information.
- Keep explanations concise and customer-friendly.
- If information is insufficient, acknowledge the uncertainty.
- Confidence should be an integer between 0 and 100.

Confidence Guidelines

90–100
Issue is straightforward and the solution is well established.

70–89
Likely correct but some uncertainty exists.

40–69
Additional investigation or specialist knowledge is recommended.

Below 40
The issue should be escalated.

Populate all output fields.

Output only the requested structured fields.
```

---

# User Prompt

```
Review the following customer support case.

Customer Ticket

{{ticket_text}}

Intent

{{intent}}

Category

{{category}}

Severity

{{severity}}

Customer Sentiment

{{sentiment}}

Determine:

- Root cause
- Resolution steps
- Customer response
- Resolution confidence

Populate all required output fields.
```

---

# Inputs

| Variable | Type |
|----------|------|
| ticket_text | String |
| intent | String |
| category | String |
| severity | String |
| sentiment | String |

---

# Outputs

| Variable | Type | Description |
|----------|------|-------------|
| root_cause | String | Most likely technical or business cause |
| resolution_steps | String | Step-by-step solution |
| customer_response | String | Customer-ready response |
| resolution_confidence | Number | Confidence score (0–100) |

---

# Example Output

| Field | Example |
|-------|---------|
| root_cause | User session expired due to an invalid authentication token. |
| resolution_steps | Clear browser cache, sign in again, and regenerate the authentication token if required. |
| customer_response | Hello, we've identified the issue affecting your login. Please follow the steps below... |
| resolution_confidence | 91 |

---

## Gateway Logic

The Resolution Agent determines the next stage of the workflow.

If:

```
resolution_confidence >= 80
```

The workflow proceeds directly to:

```
Deliver Customer Response
```

Otherwise:

```
resolution_confidence < 80
```

The ticket is escalated to the **Escalation Manager Agent**, which determines the most appropriate specialist AI agent.

---

## Downstream Consumers

The outputs of the Resolution Agent are consumed by:

- Confidence Gateway
- Escalation Manager Agent (for low-confidence cases)
- Deliver Customer Response (for high-confidence cases)

---

## Role in the Workflow

The Resolution Agent serves as the primary decision-making component of the workflow.

It attempts to autonomously resolve customer issues while accurately estimating its own confidence. This enables the workflow to automate straightforward cases and intelligently escalate complex issues, balancing efficiency with reliability.