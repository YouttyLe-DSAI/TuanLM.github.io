---
title: "Event 1"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Vietnam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders

> **Time:** Thursday, September 18, 2025, 9:00 – 17:30 <br>
> **Location:** Amazon Web Services Vietnam, 36th Floor, 2 Hai Trieu, Ben Nghe Ward, District 1, Ho Chi Minh City <br>
> **Role:** Attendee

### Event Objectives

- Update on top strategic technology trends: **Agentic AI**.
- Learn about Data Foundation solutions to address the "Data Silos" problem that 52% of CDOs are facing.
- Approach the new software development process: **AI-Driven Development Lifecycle (AI-DLC)**.
- Grasp security standards for GenAI (MITRE ATLAS, OWASP, NIST) and risk layers.

### Speakers

- Eric Yeo - Country General Manager, AWS Vietnam
- Dr. Jens Lottner - CEO, Techcombank
- Ms. Trang Phung - CEO & Co-Founder, U2U Network
- Jaime Valles - VP, GM Asia Pacific and Japan, AWS
- Jeff Johnson - Managing Director, ASEAN, AWS
- Vu Van - Co-founder & CEO, ELSA Corp
- Nguyen Hoa Binh - Chairman, Nexttech Group
- Dieter Botha - CEO, TymeX
- Jun Kai Loke - AI/ML Specialist SA, AWS
- Kien Nguyen - Solutions Architect, AWS
- Tamelly Lim - Storage Specialist SA, AWS
- Binh Tran - Senior Solutions Architect, AWS
- Taiki Dang - Solutions Architect, AWS
- Michael Armentano - Principal WW GTM Specialist, AWS
- Hung Nguyen Gia - Head of Solutions Architect, AWS
- Son Do - Technical Account Manager, AWS
- Nguyen Van Hai - Director of Software Engineering, Techcombank
- Phuc Nguyen - Solutions Architect, AWS
- Alex Tran - AI Director, OCB
- Nguyen Minh Ngan - AI Specialist, OCB
- Nguyen Manh Tuyen - Head of Data Application, LPBank Securities
- Vinh Nguyen - Co-Founder & CTO, Ninety Eight
- Hung Hoang - Customer Solutions Manager, AWS
- Christal Poon - Specialist Solutions Architect, AWS

### Key Highlights

#### 1. Agentic AI & Data Strategy Trends
- **Current State:** 88% of CDOs are moving forward with GenAI, yet 52% state their data foundation is not ready.
- **Challenges:** Businesses are held back by 3 types of "Silos": Data Silos, People Silos, and Business Silos.
- **Data Strategy:** End-to-end model from Producers → Foundations → Consumers.
    - **Infrastructure:** Amazon S3 (Data Lakes), Amazon Redshift (Data Warehouses), supporting open standard Apache Iceberg.
    - **Governance:** Amazon DataZone assists with Data & AI Governance.
    - **New Tools:** Introduction of **Unified Studio** integrating analytics and AI tools.

#### 2. AI-Driven Development Lifecycle (AI-DLC)
Speaker **Binh Tran** introduced the shift from *AI-Assisted* to *AI-Driven Development*.
The AI-DLC process consists of 3 main phases:
1.  **Inception:** Build Context on existing code, clarify intent (User Stories), plan (Units of Work), and Domain Modeling.
2.  **Construction:** AI generates code & Tests, adds architectural components.
3.  **Operation:** Deploy with IaC & tests, incident management.

#### 3. Security for GenAI
Speaker **Taiki Dang** emphasized that security must run in parallel with Generative AI.
- **Risk Layers:**
    - *Top layer (Consumer):* Risks regarding IP, legal, hallucinations, safety.
    - *Middle layer (Tuner):* Risks from Managed services, data retention policies.
    - *Bottom layer (Provider):* Risks from training data.
- **Frameworks & Standards:** Apply MITRE ATLAS, OWASP Top 10 for LLM, NIST AI RMF, ISO 42001.
- **Solutions:** Use **Amazon Bedrock Guardrails** to prevent and mitigate risks (such as toxicity, PII leaks).

#### 4. Analytics & Business Intelligence
Speaker **Christal Poon** presented the transition from Amazon QuickSight to **Amazon Q**.
- Features for creating Dashboards, reports, and Data QA using natural language.
- **Coming soon to Vietnam:** Amazon Agentic AI Workbench (Quick Suite) with Quick Researcher and Quick Automate capabilities, keeping humans in the loop for control.

### Key Takeaways

- **Agent Mindset:** Clearly understand the structure of an AI Agent: Goals → Observation → Tools → Context → Action.
- **Agent Core Architecture:** Ensure all components are present: Runtime, Gateway, Memory, Observability, and Identity to deploy Agents to production safely and scalably.
- **Multi-layer Security:** Security extends beyond the application; it must control risks from training data and fine-tuning processes down to end-users (Consumer risks).

### Applying to Work

- **Implement AI-DLC:** Pilot the 7-step AI-DLC process in a new project, starting with using AI to "Build Context" and "Domain Modeling".
- **Enhance Security:** Review current GenAI applications against the **OWASP Top 10 for LLM** checklist and integrate **Bedrock Guardrails** to filter harmful content.
- **Modernize Data Stack:** Evaluate the feasibility of migrating the current Data Warehouse to a **Lakehouse** architecture with Apache Iceberg on AWS to break down Data Silos.

### Personal Experience

This event went much deeper technically (deep-dive) than I expected, providing significant practical value:
- I was very impressed by the sharing on **AI-DLC** by Mr. Binh Tran. It completely changed my perspective on coding: developers are no longer just writing code but becoming "architects" and "reviewers" for AI execution.
- The **Scoping Matrix** slide and the risk layers in GenAI gave me a more systematic view to justify new AI project deployments to the company's Security department.
- I am very excited about the news that **Amazon Agentic AI Workbench** is coming to Vietnam, promising to solve the problem of automating market research processes (Quick Researcher) that the business team currently needs.

### Event Photos

![event1-1](/images/4-event/event1-1.png)

![event1-2](/images/4-event/event1-2.png)

> Summary: A "must-attend" event for Builders. Knowledge about Agentic AI and AI-DLC will be the compass for my technical development roadmap in the coming year.