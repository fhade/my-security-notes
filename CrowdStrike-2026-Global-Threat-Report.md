# CrowdStrike 2026 Global Threat Report
## *Year of the Evasive Adversary*

> **Source:** CrowdStrike 2026 Global Threat Report  
> **Publisher:** CrowdStrike (NASDAQ: CRWD)  
> **Coverage Period:** 2025 threat activity and 2026 outlook  
> **Reference:** [crowdstrike.com](https://www.crowdstrike.com)

---

## Key Statistics at a Glance

| Metric | Value |
|---|---|
| AI-enabled adversary attacks (YoY increase) | **+89%** |
| Average eCrime breakout time | **29 minutes** (down from 48 min in 2024) |
| Fastest recorded breakout time | **27 seconds** |
| Malware-free detections | **82%** (up from 51% in 2020) |
| Zero-day exploitation (YoY increase) | **+42%** |
| Cloud-conscious intrusions (YoY increase) | **+37%** |
| Cloud intrusions by state-nexus actors | **+266%** |
| Valid account abuse in cloud incidents | **35%** |
| China-nexus activity increase | **+38%** |
| Total adversaries tracked by CrowdStrike | **281** |
| New adversaries named in 2025 | **24** |
| Fake CAPTCHA lure incidents (YoY increase) | **+563%** |

---

## Overarching Theme: The Evasive Adversary

2025 was defined by adversaries exploiting **trust** rather than technical vulnerabilities. Threat actors moved through valid credentials, trusted identity flows, approved SaaS integrations, and legitimate software supply chains — blending seamlessly into normal activity. Speed, legitimacy, and low-visibility access paths are the hallmarks of modern evasive tradecraft.

---

## Key Adversary Themes

### 1. AI-Enhanced Attacks

Adversaries at all skill levels integrated AI into their operations in 2025, primarily to **accelerate and enhance existing techniques** rather than create entirely novel attack vectors.

**Social Engineering**
- Chinese intelligence services used AI to create fake consulting firms targeting former U.S. government employees on job recruitment platforms
- RENAISSANCE SPIDER used AI to translate phishing lures into Ukrainian, significantly increasing credibility
- FAMOUS CHOLLIMA (North Korea) incorporated ChatGPT, Gemini, GitHub Copilot, and VSCodium into fraudulent employment operations, using AI image manipulation to create fake personas

**Information Operations**
- A pro-Russia propagandist used AI to generate fake media websites and videos targeting U.S. and German elections
- State-nexus actors deployed AI-generated deepfake videos, fake social media networks, and targeted propaganda

**Technical / Malware Development**
- FANCY BEAR deployed *LAMEHUG* malware — the first observed instance of LLM prompting embedded directly in malware — to automate reconnaissance against Ukrainian government entities using the Hugging Face API
- PUNK SPIDER used Gemini-generated scripts for credential dumping from Veeam Backup & Replication databases
- Two ransomware variants (*FunkLocker* and *RALord*) shared encryption flaws traceable to the unrestricted AI model WormGPT
- In August 2025, malicious npm packages used victims' own local AI CLI tools (Claude, Gemini) to steal authentication materials and cryptocurrency

**Threats TO AI Systems**
- Cerber ransomware operators exploited CVE-2025-3248 in Langflow (a low-code AI platform) to deploy ransomware
- A malicious MCP server (*postmark-mcp*) impersonated a legitimate server to forward users' emails to attackers
- Threat actors distributed malware by impersonating popular AI models (DeepSeek, ChatGPT)

**2026 Outlook:** More sophisticated actors will likely operationalize **agentic AI** for minimally supervised attacks. AI's integration into business processes expands the attack surface to include AI models, training data, and agents themselves.

---

### 2. Ransomware — Cross-Domain Tradecraft

Big Game Hunting (BGH) adversaries dominated eCrime in 2025, evolving tactics to exploit security blind spots across multiple domains simultaneously.

**Core Evasion Techniques in 2025:**
- Initial access via **vishing** (voice phishing) to help desk personnel
- Targeting **cloud-based SaaS** for data discovery and exfiltration
- Deploying ransomware exclusively on **VMware ESXi** infrastructure (avoiding monitored endpoints)
- **Remote encryption via SMB shares** from unmanaged hosts

**Notable Adversaries:**

| Adversary | Highlights |
|---|---|
| **PUNK SPIDER** | Most active BGH adversary — 198 intrusions (↑134% YoY). Remotely encrypts via SMB from unmanaged hosts; even used an unpatched webcam to execute Akira ransomware |
| **SCATTERED SPIDER** | Targets aviation, insurance, retail. Uses social engineering on help desks; exploits unmanaged VMs to dump Active Directory credentials (NTDS) |
| **BLOCKADE SPIDER** | Embargo ransomware; uses cross-domain tradecraft spanning edge devices → identity → cloud → VMware ESXi; mirrors many SCATTERED SPIDER techniques |

**2026 Outlook:** Ransomware remains highly resilient. Cross-domain techniques (unmanaged systems + remote encryption + cloud identity abuse) will continue to outpace traditional endpoint-centric defenses.

---

### 3. China-Nexus Threat Actors — Edge Device Targeting

China-nexus adversaries demonstrated a **systematic preference for network perimeter and edge devices** as initial access vectors in 2025, with a 38% overall increase in activity.

**Sectors Most Targeted:**
- Logistics (+85%), Telecommunications (+30%), Financial Services (+20%)
- Also: legal, technology, manufacturing, government, aviation, biomedical

**Key Tactics:**
- Exploited VPN appliances, firewalls, gateways, and routers
- **67%** of exploited vulnerabilities provided immediate Remote Code Execution (RCE)
- **40%** of exploited vulnerabilities targeted internet-facing edge devices
- Weaponized newly disclosed CVEs within **2–6 days** of public release

**Rapid Weaponization Examples in 2025:**

| CVE | Days to Exploit | Adversary |
|---|---|---|
| CVE-2025-31324 (file upload) | 3 days | PHANTOM PANDA |
| CVE-2025-25257 (SQL injection) | 6 days | OPERATOR PANDA |
| CVE-2025-55182 (React2Shell RCE) | 2 days | VAULT PANDA / GENESIS PANDA |

**Post-Access Tactics:** Deploy custom malware (BRICKSTORM, ShadowPad, TetanusStorm), use ORB relay networks for anonymity, and establish long-term persistence (one WARP PANDA intrusion lasted 22 months undetected).

**2026 Outlook:** China-nexus actors will continue prioritizing edge device exploitation. Organizations should patch critical edge devices within **72 hours** of vulnerability disclosure.

---

### 4. Supply Chain Attacks

Supply chain compromises allow adversaries to exploit **trusted update mechanisms and software dependencies**, bypassing traditional security controls entirely.

**Key 2025 Incidents:**

**PRESSURE CHOLLIMA / Bybit ($1.46B theft)**
The largest cryptocurrency theft in history. The adversary compromised Safe{Wallet} via a trojanized Python project sent to a developer, inserted malicious JavaScript into the frontend, and silently redirected a $1.46 billion transaction to an attacker-controlled wallet — then restored the original code to avoid detection.

**ShaiHulud npm Malware**
A self-propagating information stealer distributed via the npm ecosystem. Initially downloaded over 2 million times; capable of infecting further npm packages it finds authentication tokens for. In November 2025, updated to include remote execution and destructive payload delivery.

**FAMOUS CHOLLIMA npm Packages**
Deployed 30+ malicious packages between January–May 2025 by posing as job recruiters and asking developers to run the packages as part of a fake employment assessment. Packages downloaded 8,000+ times.

**Notepad++ Supply Chain Attack**
In late October 2025, CrowdStrike OverWatch identified a legitimate Notepad++ update process delivering malicious RAT payloads. Targeted only ~0.1% of organizations updating — highly selective.

**2026 Outlook:** Supply chain attacks will increase, with attackers refining self-replication capabilities and targeting SaaS providers to compromise downstream customers via stolen OAuth tokens.

---

### 5. Zero-Day Exploit Escalation

Zero-day exploitation increased **42% year-over-year** in 2025, continuing a multi-year upward trend.

**Targeted Intrusion Actors** prioritize zero-days in internet-exposed edge devices (VPNs, mail servers, firewalls) for stealthy persistent access.

**eCrime Actors** use zero-days primarily for **local privilege escalation (LPE)** on Windows operating systems, selecting exploits based on reliability and ease of acquisition (brokers, public repos, or in-house development). GRACEFUL SPIDER stands out by repeatedly using zero-days in internet-facing enterprise products for mass data exfiltration.

**2026 Outlook:** Zero-day trends will persist. Sophisticated adversaries may begin targeting lower-profile **defense evasion** vulnerabilities that allow them to remain undetected long-term without triggering widespread patching.

---

### 6. Cloud Platform Abuse

Cloud-conscious intrusions rose **37%** in 2025, with state-nexus actors showing a **266%** increase.

**Core Technique: Subverting Trust in Identity Systems**

Adversaries targeted identity and cloud platforms at three layers:

| Trust Layer | Technique | Key Adversaries |
|---|---|---|
| Organization-level | Abusing Entra ID partner connections / B2B relationships | MURKY PANDA |
| Tenant identity-level | Hybrid identity sync (Entra Connect, AD FS), token-signing cert abuse | SCATTERED SPIDER, BLOCKADE SPIDER |
| User-level | OAuth 2.0 phishing flows, device code auth, AiTM kits | COZY BEAR, IMPERIAL KITTEN |

**Notable Cloud Attack Examples:**

**COZY BEAR (Russia)** — Conducted multi-day, multi-channel social engineering campaigns (instant messaging + email + video calls) impersonating trusted contacts, then phished victims via legitimate Microsoft OAuth pages — no suspicious domains involved, making detection extremely difficult.

**MURKY PANDA (China)** — Specialized in abusing Entra ID partner connections to silently access downstream victim data via the ORB28 relay network.

**ShinyHunters** — Used AiTM phishing to capture Microsoft Entra ID credentials, then pivoted to SharePoint and CRM instances to exfiltrate high-value data.

**2026 Outlook:** SaaS targeting will increase as organizations continue migrating to cloud. CRM instances are emerging as a prime target via stolen OAuth tokens and non-human identity abuse.

---

## Interactive Intrusions — Breakdown

Adversaries increasingly prefer **direct, human-driven intrusions** using legitimate tools and credentials over malware, making detection with traditional controls extremely difficult.

**By Region (2025):**
North America 55% | Europe 15% | East Asia 12% | South Asia 9% | Southeast Asia 7% | Others <6%

**By Industry (Top 5):**
Technology 23% | Manufacturing 15% | Retail 12% | Financial Services 11% | Healthcare 10%

---

## Recommendations

**1. Secure AI Systems**
Monitor employee AI tool usage, enforce access controls, secure AI workloads against prompt injection, assess vendor AI security, and develop AI-specific incident response plans.

**2. Treat Identity and SaaS as Primary Attack Surfaces**
Strengthen phishing-resistant MFA, enforce least-privilege access for service and non-human accounts, and monitor for anomalous SaaS and token activity.

**3. Eliminate Cross-Domain Blind Spots**
Consolidate telemetry, apply cross-domain correlation via XDR and next-gen SIEM, and automate enrichment with threat intelligence.

**4. Secure the Software Supply Chain**
Harden developer environments, enforce code signing and dependency validation, scan repositories for anomalies, and assess third-party risk continuously.

**5. Prioritize Edge Device Patching**
Patch internet-facing appliances within 72 hours of critical CVE disclosure. Enable logging on VPNs, firewalls, and virtualization platforms. Apply network segmentation.

**6. Proactive Threat Intelligence and Hunting**
Adopt an intelligence-driven approach to understand which adversaries are targeting your sector. Use AI agents to accelerate triage and response.

**7. Strengthen Human Resilience**
Run regular tabletop exercises and red/blue team operations. Train employees to recognize vishing, phishing, and trust abuse tactics that bypass technical controls.

---

## CrowdStrike Adversary Naming Conventions

| Suffix | Nation/Category |
|---|---|
| BEAR | Russia |
| PANDA | People's Republic of China |
| CHOLLIMA | DPRK (North Korea) |
| KITTEN | Iran |
| SPIDER | eCrime |
| JACKAL | Hacktivist |
| WOLF | Türkiye |
| LEOPARD | Pakistan |
| TIGER | India |
| BISON | Belarus |
| LYNX | Georgia |

---

## Notable Adversaries Referenced

| Adversary | Type | Notable 2025 Activity |
|---|---|---|
| PUNK SPIDER | eCrime | Most active BGH actor; 198 intrusions; Akira ransomware via unmanaged devices |
| SCATTERED SPIDER | eCrime | High-profile retail/aviation attacks; VMware credential dumping |
| BLOCKADE SPIDER | eCrime | Embargo ransomware; cross-domain Entra ID abuse |
| FAMOUS CHOLLIMA | DPRK | Fraudulent IT employment; npm supply chain attacks; activity doubled YoY |
| PRESSURE CHOLLIMA | DPRK | $1.46B Bybit cryptocurrency theft |
| FANCY BEAR | Russia | LAMEHUG LLM-enabled malware against Ukrainian government |
| COZY BEAR | Russia | Multi-layered Microsoft OAuth phishing against U.S. NGOs |
| MURKY PANDA | China | Entra ID partner connection abuse; ORB28 network |
| GRACEFUL SPIDER | eCrime | Repeated zero-day exploitation of internet-facing enterprise products |
| CHATTY SPIDER | eCrime | Law firm targeting; initial access to data exfiltration in 4 minutes |

---

## 2026 Forward-Looking Assessments

**Russia-nexus** — Will continue aggressive intelligence collection against Ukrainian targets and NATO member states.

**China-nexus** — Will maintain high operational tempo with increased stealth; continued targeting of telecom, logistics, and financial services aligned with CCP strategic objectives.

**DPRK-nexus** — Acute threat to fintech, technology, and Western defense entities; continued cryptocurrency theft and fraudulent IT employment schemes.

**eCrime/Ransomware** — BGH will remain resilient. Cross-domain tradecraft, SaaS-focused initial access, and AI-assisted operations will define 2026.

**AI Threats** — Agentic AI attacks requiring minimal human oversight are emerging. The AI attack surface (models, training data, supply chains) will grow significantly.

---

*Last reviewed: March 2026*
