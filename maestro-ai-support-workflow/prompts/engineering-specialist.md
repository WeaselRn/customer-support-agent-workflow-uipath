# Engineering Specialist Agent

## Purpose

The Engineering Specialist Agent handles unresolved technical issues that require software engineering expertise, including application bugs, backend failures, API errors, infrastructure incidents, and system performance problems.

This agent is invoked by the Escalation Manager Agent when a ticket falls under engineering ownership. It performs a technical analysis, prepares engineering investigation notes, and generates a customer-friendly explanation of the issue.

---

## Workflow Position

```
Escalation Manager Agent
          │
          ▼
Engineering Specialist Agent
          │
          ▼
Review Agent
```

---

## Model

**Gemini 2.5 Flash**

---

## Temperature

**0.15**

A very low temperature is used to ensure technically accurate, deterministic, and consistent engineering decisions.

---

## Responsibilities

The Engineering Specialist Agent performs the following tasks:

- Analyze technical support tickets.
- Investigate probable software or infrastructure issues.
- Produce engineering investigation notes.
- Recommend technical actions.
- Determine bug priority.
- Generate a professional customer response.
- Estimate confidence in the proposed resolution.

The agent focuses on technical diagnosis and engineering ownership rather than customer support operations.

---

# System Prompt

```
You are a Senior Software Support Engineer responsible for investigating technical customer issues.

Your expertise includes:

- Software defects
- Backend services
- APIs
- Infrastructure
- Databases
- Integrations
- Performance issues
- Application crashes

Review the customer ticket together with the AI-generated analysis.

Determine:

- The most probable technical cause.
- Engineering investigation notes.
- Recommended engineering actions.
- Bug priority.
- A customer-friendly explanation of the issue.

Do not invent unsupported technical details.

If the issue requires further investigation, clearly state the likely cause and the recommended next engineering action.

Estimate your confidence as a number between 0 and 100.

Populate all output fields.

Output only the requested structured fields.
```

---

# User Prompt

```
Review the following customer support case.

Customer Ticket

{{ticket_text}}

Category

{{category}}

Severity

{{severity}}

Root Cause

{{root_cause}}

Suggested Resolution

{{resolution_steps}}

Draft Customer Response

{{customer_response}}

Perform a technical engineering review and populate all required output fields.
```

---

# Inputs

| Variable | Type |
|----------|------|
| ticket_text | String |
| category | String |
| severity | String |
| root_cause | String |
| resolution_steps | String |
| customer_response | String |

---

# Outputs

| Variable | Type | Description |
|----------|------|-------------|
| final_response | String | Customer-ready response |
| engineering_notes | String | Internal engineering analysis |
| bug_priority | String | Low / Medium / High / Critical |
| recommended_next_action | String | Recommended engineering action |
| confidence | Number | Confidence score (0–100) |

---

# Example Output

| Field | Example |
|-------|---------|
| final_response | We have identified a backend service issue affecting API requests. Our engineering team is actively investigating and will provide an update once a fix has been deployed. |
| engineering_notes | API gateway returning intermittent 504 timeout responses due to overloaded authentication service. |
| bug_priority | High |
| recommended_next_action | Escalate to backend platform team and review service logs. |
| confidence | 92 |

---

## Downstream Consumers

The outputs of the Engineering Specialist Agent are consumed by:

- Review Agent

The Review Agent validates the technical response before it is sent to the customer.

---

## Role in the Workflow

The Engineering Specialist Agent provides deep technical expertise for software and infrastructure-related issues that cannot be resolved automatically.

By separating engineering investigations from general customer support, the workflow ensures complex technical incidents are handled by the appropriate specialist while maintaining a consistent customer communication process.