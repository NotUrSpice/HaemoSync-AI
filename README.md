# HaemoSync AI 🩸
### Strategic Autonomous Pipeline for Emergency Blood Logistics

> **IBM SkillsBuild × AICTE Internship Project**
> Developed by **Akshay V Sarma** | B.Tech Industrial Engineering, College of Engineering Trivandrum (CET)

---

## The Problem

In high-stress medical environments like Thiruvananthapuram's hospital network, blood bank inventory is critically **siloed**.

- **Hospital A** may have 1 unit of O-Negative — a life-threatening shortage.
- **Hospital B**, just 5 km away, may have 18 units sitting idle.
- The current system relies on **manual phone calls, WhatsApp messages, and human auditing** to bridge this gap — introducing dangerous lead-time when every minute counts.

HaemoSync AI eliminates this delay entirely.

---

## What It Does

HaemoSync AI is a **Proof-of-Concept Agentic Pipeline** that:

1. **Reads** real-time blood inventory data from a centralized Google Sheets database
2. **Aggregates** regional hospital data into a structured payload
3. **Reasons** over the data using a Greedy Transshipment Algorithm powered by Google Gemini 2.5 Flash
4. **Acts** by autonomously dispatching a high-priority transfer alert email to hospital administrators — with zero human intervention

---

## System Architecture

```
[Trigger] → [Google Sheets] → [Aggregate] → [Gemini 2.5 Flash] → [Gmail Dispatch]
              (Inventory DB)   (n8n layer)    (OR Reasoning)       (Alert Email)
```

| Layer | Tool | Role |
|---|---|---|
| Data Layer | Google Sheets | Centralized real-time inventory database |
| Orchestration Layer | n8n | Aggregates and routes data between nodes |
| Reasoning Layer | Google Gemini 2.5 Flash | Autonomous decision engine (Greedy Algorithm) |
| Action Layer | Gmail (SMTP) | Structured emergency dispatch to administrators |

---

## Operations Research Foundation

This project applies classical OR principles to modern AI — making HaemoSync AI an **engineering solution**, not just an AI demo.

### Greedy Transshipment Algorithm

The LLM is not used for creative generation. It executes a deterministic heuristic:

- **RULE 1 — Minimum Scan:** Identify the hospital with the lowest O-Negative units → **Demand Node (Recipient)**
- **RULE 2 — Maximum Scan:** Identify the hospital with the highest O-Negative units → **Supply Node (Provider)**
- **RULE 3 — Transshipment Constraint:** Fixed transfer of 5 units. Post-transfer provider stock is verified to remain above zero, preventing a new shortage from being created.

This is a direct application of:
- **Inter-hospital Transshipment Problem** — redistributing existing stock across a network to meet demand nodes
- **Network Resilience Optimization** — eliminating single points of failure in the regional blood grid
- **Decision Support Systems (DSS)** — using AI as a structured reasoning engine, not a generative tool

---

## Tech Stack

- **n8n** — Workflow automation and orchestration
- **Google Sheets** — Inventory data layer
- **Google Gemini 2.5 Flash** — LLM reasoning engine
- **Gmail API (SMTP)** — Automated alert dispatch

---

## Sample Output

The system produces a structured emergency email like:

```
Subject: [URGENT] Emergency O-Negative Blood Transfer Required

Dear Administrator,

This is an automated critical alert from HaemoSync AI.

A life-threatening O-Negative shortage has been detected in the regional network.

Current Status:
- Critical Shortage: KIMS Hospital — 1 unit remaining
- Available Surplus: Medical College — 18 units available
- Post-Transfer Provider Stock: 13 units (verified safe)

ACTION REQUIRED: Transfer 5 units of O-Negative from Medical College 
to KIMS Hospital immediately.

Please coordinate with your logistics team and confirm receipt of this 
transfer within 30 minutes.

This alert was generated autonomously by a Greedy Transshipment Algorithm. 
No human delay has occurred.

HaemoSync AI | Emergency Blood Logistics System
Thiruvananthapuram Regional Network
```

---

## Current Limitations (PoC Scope)

- The system uses a cloud-based API key for Gemini — subject to rate limits and occasional hallucination under quota pressure
- Google Sheets acts as a mock database; not connected to live Hospital Information Systems (HIS)
- Transfer quantity is fixed at 5 units (not dynamically calculated based on shortage severity)

---

## Future Roadmap

| Phase | Feature |
|---|---|
| v2.0 | **Real-time HIS Integration** — Direct API connection to Hospital Information Systems |
| v2.1 | **IoT Triggers** — Panic buttons in ERs and automated refrigerator threshold alerts |
| v3.0 | **Sovereign AI Deployment** — Local open-source LLMs (Llama 3) for 100% patient data privacy |
| v3.1 | **Geospatial Optimization** — Google Maps API for shortest-path courier routing with real-time traffic |


## Author

**Akshay V Sarma**
B.Tech Industrial Engineering | College of Engineering Trivandrum (CET) | Batch of 2029
IBM SkillsBuild × AICTE Virtual Internship — AI Strategy And Business Intelligence Internship
