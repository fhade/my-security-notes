# AI Security Best Practices Guide

> **Source:** Datadog — *AI Security Best Practices Guide* (Best Practice Series)  
> **Author:** Mallory Mooney  
> **Reference:** [datadog.com](https://datadog.com)

---

## Overview

The rapid adoption of generative AI (GenAI) has introduced new security challenges. This guide covers threats targeting three core components of AI applications, mapped to **MITRE ATLAS** (Adversarial Threat Landscape for Artificial Intelligence Systems) tactics and techniques:

| Component | Description |
|---|---|
| **Infrastructure** | Containers, databases, cloud storage, MCP servers |
| **Supply Chain** | Training datasets, pre-trained LLMs, third-party AI libraries |
| **AI Interfaces** | Chat interfaces, API endpoints, user-facing entry points |

---

## Part 1 — Abusing AI Infrastructure

### How It Happens

AI infrastructure combines established cloud services with emerging tools like MCP servers and RAG pipelines. Common weaknesses include:

- Overprivileged IAM roles
- Missing authentication, authorization, and logging controls
- Mismanaged credentials (leading cause of cloud incidents)

### Key Attack Tactics

**Initial Access** — Attackers use compromised credentials, API keys, or exploit public-facing applications. Example: prompt injection into M365 Copilot via a poisoned RAG database seeded through a malicious email.

**Credential Access** — Actively searching for and stealing improperly stored credentials. Real-world example: exposed Ray cluster (Python AI scaling framework) with leaked SSH keys, Kubernetes secrets, and cloud environment keys.

**Discovery (LLM Jacking)** — After gaining access, attackers probe cloud services (e.g., Amazon Bedrock) via legitimate API calls to find available LLMs, avoiding immediate detection.

**Reconnaissance** — Active scanning of infrastructure resources and networks.

**Resource Development** — Creating new cloud accounts to support future attack phases.

### Detection & Mitigation

- Monitor logs for compromised account keys (Datadog Cloud SIEM)
- Flag unusual `InvokeModel` calls to services like Amazon Bedrock
- Minimize use of long-lived credentials
- Scan for old/unused credentials regularly

---

## Part 2 — Abusing Supply Chains

### How It Happens

Supply chains deliver software and data to AI applications. Organizations often integrate third-party artifacts (models, datasets, libraries) with less visibility and control, creating opportunities for attackers to introduce malicious components.

### Key Attack Tactics

**Resource Development & Attack Staging** — Attackers publish poisoned datasets, models, or packages (e.g., under hallucinated names on PyPI). They may also train proxy models to test attacks before targeting real ones.

**Initial Access** — Example: a fake but believable organization account on a public model repository tricked employees into uploading private AI models, which were then backdoored with a C2 server.

**Defense Evasion** — Malicious models designed to bypass security scanners (e.g., exploiting Python pickle file vulnerabilities on Hugging Face).

### Detection & Mitigation

- Use vulnerability scanning tools (e.g., Datadog Code Security, GuardDog) to detect risks in third-party libraries
- Follow MITRE recommendations:
  - Create authorization controls for internal model registries and training data
  - Restrict public access to production model architecture details
  - Regularly sanitize training data before use
  - Routinely validate AI model behavior for signs of poisoning
  - Use **code signing** to verify supply chain artifacts with digital signatures

---

## Part 3 — Abusing AI Interfaces

### How It Happens

AI interfaces (chat UIs, API endpoints) rely on unpredictable natural language input. This makes them a prime target since malicious prompts can blend in with legitimate user interactions.

### Key Attack Tactics

**Execution via Prompt Injection** — Both direct and indirect injections hijack LLM behavior. Examples:
- SQL database tables leaked via prompt injection
- Indirect injection through poisoned RAG entries altering LLM responses for all subsequent users

**Persistence** — Attackers maintain influence by gradually manipulating model behavior through coordinated toxic prompts (e.g., corrupting a Twitter chatbot's responses over time).

**Data Exfiltration** — LLMs are manipulated into revealing sensitive memorized data or information accessible via API tools. Example: a self-replicating prompt used with a RAG assistant to extract sensitive user data.

### Detection & Mitigation

- Monitor for toxic prompts and unusual input patterns (Datadog LLM Observability)
- **Sanitize prompt inputs** before they reach the model
- Apply **rate limiting** to throttle high-volume prompt attacks
- Watch for injection patterns: long instructions, nested logic, out-of-scope queries
- Restrict model permissions — limit which APIs, tools, and data the model can access
- Implement **output filtering** to strip sensitive data before the model responds

---

## Quick Reference — Mitigation Checklist

### Infrastructure
- [ ] Minimize long-lived credentials
- [ ] Monitor cloud logs with SIEM for anomalous API calls
- [ ] Apply least-privilege IAM roles
- [ ] Enable logging on all AI-related cloud services

### Supply Chain
- [ ] Vet all third-party AI libraries and dependencies
- [ ] Use code signing for supply chain artifacts
- [ ] Sanitize training data regularly
- [ ] Set authorization controls on model registries
- [ ] Run vulnerability scanners on dependencies (Code Security, GuardDog)

### AI Interfaces
- [ ] Sanitize all user prompt inputs
- [ ] Rate limit API/chat endpoints
- [ ] Monitor for prompt injection patterns
- [ ] Restrict model access to APIs and sensitive data
- [ ] Implement output filtering on model responses
- [ ] Track patterns of toxic input over time, not just individual prompts

---

## Framework Reference

This guide maps all threats to **[MITRE ATLAS](https://atlas.mitre.org/)** — the Adversarial Threat Landscape for AI Systems — as well as the traditional **MITRE ATT&CK** framework for infrastructure-level techniques.

---

*Last reviewed: March 2026*
