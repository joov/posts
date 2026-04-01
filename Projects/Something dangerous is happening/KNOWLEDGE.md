# Knowledge Sources: "Something Dangerous Is Happening"

Collected: 2026-03-28

---

## 1. Adversarial Attacks on AI Agents / Prompt Injection

### Unit 42 – Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild
**URL:** https://unit42.paloaltonetworks.com/ai-agent-prompt-injection/
**Published:** March 3, 2026 | Palo Alto Networks Unit 42
**Authors:** Beliz Kaleli, Shehroze Farooqi, Oleksii Starov, Nabeel Mohamed

**Summary:** First large-scale, in-the-wild documentation of indirect prompt injection (IDPI) attacks against AI agents. Attackers embed hidden instructions in web content consumed by LLMs to trigger unauthorized actions — from ad review evasion to data destruction, unauthorized transactions, and system prompt leakage. Presents a full taxonomy of attacker intents (low/medium/high/critical) and 22 payload engineering techniques (visual concealment, obfuscation, dynamic execution, jailbreak methods). Key finding: 85% of in-the-wild jailbreaks use social engineering. The web has become an LLM prompt delivery mechanism.

**Key quotes/data points:**
- "IDPI is no longer merely theoretical but is being actively weaponized."
- 22 distinct techniques observed; top delivery method: visible plaintext (37.8%); top jailbreak: social engineering (85.2%)
- Attack intents include: SEO poisoning, data destruction, unauthorized transactions, sensitive data leakage, DoS

---

### AI Agent Security 2026: Google's Forecast And How To Fix The Gaps
**URL:** https://agatsoftware.com/blog/ai-agent-security-2026-google-forecast/
**Published:** March 26, 2026 | AGAT Software

**Summary:** Overview of Google's security forecast for the AI agent landscape and where defenses currently fall short. Covers the expanded attack surface introduced by autonomous agents operating at scale in enterprise environments.

---

## 2. AI-Enhanced Social Engineering

### AI-Powered Social Engineering: How LLMs Are Revolutionizing Phishing and Vishing Attacks
**URL:** https://notchrisgroves.com/ai-powered-social-engineering/
**Published:** March 14, 2026

**Summary:** Argues that around 2024 the economics of social engineering fundamentally changed. LLMs enable hyper-personalized, scalable phishing and vishing at near-zero marginal cost. Most organizations are still defending against the old threat model. Covers how LLMs lower the skill barrier for attackers and enable real-time adaptive attacks.

**Key insight:** "Somewhere around 2024, the economics of social engineering fundamentally changed — but we're still defending against attacks as if nothing happened."

---

### Phishing 2.0: Exploring the Capabilities and Risks of Agentic AI-Enabled Attacks
**URL:** https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1795045/full
**Published:** March 25, 2026 | Frontiers in Computer Science (peer-reviewed)

**Summary:** Academic research exploring agentic AI as an attack enabler for phishing. Examines capabilities that autonomous AI agents bring to phishing campaigns — including target profiling, multi-channel execution, and adaptive response — and the risk amplification this creates. Part of a research topic on ethical and explainable AI for cognitive computing.

---

## 3. AI Governance Gaps / AI Agents as Employees

### Securing AI Agents: The Defining Cybersecurity Challenge of 2026
**URL:** https://www.bvp.com/atlas/securing-ai-agents-the-defining-cybersecurity-challenge-of-2026
**Published:** March 24, 2026 | Bessemer Venture Partners (Christine Deakers)

**Summary:** CISOs are having to fundamentally reimagine the security stack as AI agents become a de facto workforce. Covers the control gaps that emerge when autonomous agents act with employee-level privileges — access to data, systems, and external services — but without the established HR, legal, and compliance controls that govern human employees. Frames this as the defining security challenge of 2026.

---

### Agentic AI Governance: The Enterprise Guide for 2026
**URL:** https://ienable.ai/blog/agentic-ai-governance-enterprise-guide-2026.html
**Published:** March 15, 2026 | iEnable

**Summary:** Seven agentic AI governance controls every CISO needs before deploying autonomous agents. Uses concrete failure examples: an agent sending 4,000 incorrect customer emails, another approving $12,000 in ad spend without review. Highlights the gap between operational AI capability and governance maturity. Practical controls around scope limitation, audit logging, and human-in-the-loop checkpoints.

**Key data:** Real-world incidents from deployed enterprise agents already causing measurable business damage.

---

## 4. ISMS and Risk Frameworks for AI

### Is an Agentic AI Security Breach Inevitable in 2026?
**URL:** https://www.isms.online/information-security/is-an-agentic-ai-security-breach-inevitable-in-2026/
**Published:** December 11, 2025 | ISMS.online (Phil Muncaster)

**Summary:** Examines whether the architecture of agentic AI systems makes a serious security breach statistically inevitable in 2026. Covers the limitations of existing ISO 27001 controls when applied to autonomous AI, the new threat categories not addressed by traditional ISMS scope, and what updated frameworks (e.g., ISO 42001) do and don't cover. Argues for a fundamental rethink rather than incremental extension of existing controls.

---

## 5. Defensive Measures for AI Agents

### SPIFFE – Secure Production Identity Framework for Everyone
**URL:** https://spiffe.io
**Maintained by:** CNCF (Cloud Native Computing Foundation) — graduated project
**Adopted by:** Google, Netflix, Uber, Amazon, Bloomberg, Intel, SAP, IBM, Cisco and others

**Summary:** SPIFFE defines an open standard for workload identity in distributed systems. Instead of static API keys or long-lived credentials, SPIFFE issues short-lived, cryptographically attested X.509 certificates (SVIDs — SPIFFE Verifiable Identity Documents) to workloads, automatically rotated. SPIRE is the reference runtime implementation. The framework eliminates the long-lived credential problem at the architectural level — directly addressing the 99%-over-permissioned-identity finding from Unit 42. For AI agents specifically, SPIFFE/SPIRE enables every agent to have a verified, time-bounded identity that is automatically revoked when the workload stops.

**Key relevance for this post:**
- Provides the structural/architectural answer to "how do you give AI agents proper identity without relying on static tokens?"
- Vendor-neutral, open standard — not a product pitch
- Already deployed at hyperscale; this is proven infrastructure, not experimental
- Directly maps to the governance gap: AI agents currently have no verified identity — SPIFFE closes that at the infrastructure layer

---

### Securing AI Agents in 2026: How Enterprises Can Stop Prompt Injection, Model Poisoning, and Agentic AI Exploitation at Scale
**URL:** https://hive-project.com/blog/securing-ai-agents-in-2026-how-enterprises-can-stop-prompt-injection-model-poisoning-and-agentic-ai-exploitation-at-scale/
**Published:** March 23, 2026 | Reflex AI

**Summary:** Practical enterprise guide to defending against the three primary AI agent attack vectors: prompt injection, model poisoning, and agentic exploitation at scale. Covers detection approaches, architectural controls, and how to layer defenses without crippling agent utility. Useful for the tactical/operational section of the post.

---

## 6. Threat Intelligence / Incident Response Data

### 2026 Unit 42 Global Incident Response Report
**URL:** https://www.paloaltonetworks.com/resources/research/unit-42-incident-response-report
**Published:** 2026 | Palo Alto Networks Unit 42 (Sam Rubin, SVP Consulting & Threat Intelligence)
**Based on:** 750+ major IR engagements, 50+ countries

**Summary:** Landmark annual IR report documenting how AI has become a force multiplier for threat actors in 2025/2026. Organized around four major trends: (1) AI accelerates attacks; (2) identity is now the primary attack path; (3) software supply chain risk has expanded to SaaS and trusted connectivity; (4) nation-state actors are adapting with deepfakes and AI-enabled tradecraft. Critically, 90%+ of breaches were enabled by preventable gaps, not attacker sophistication.

**Key data points:**
- AI compressed time-to-exfiltration: fastest 25% of attacks reached exfiltration in 72 minutes in 2025, down from 285 minutes in 2024
- Identity weaknesses played a material role in **~90% of all Unit 42 investigations**
- 87% of intrusions involved activity across multiple attack surfaces simultaneously
- 48% of incidents involved browser-based activity (up from 44% in 2024)
- Phishing and vulnerability exploitation each accounted for **22%** of initial access
- AI enables "hyper-personalized social engineering" — past "phishing with better grammar"
- Nation-state actors using AI-generated deepfakes for synthetic employment personas (North Korea's Wagemole campaign); LLM-generated C2 instructions (Russia's LAMEHUG/APT28)
- "Vibe extortion" case: unsophisticated actor used LLM to script professional extortion strategy
- AI-assisted insider threat: insider used company AI assistant to research systems, generate DoS script, troubleshoot in real time
- LOTAIL ("Living Off the AI Land"): attackers misuse enterprise AI platforms with valid credentials for privilege escalation and environment reconnaissance
- 99% of cloud identities had excessive permissions (analysis of 680,000 identities)
- Encryption in ransomware declined from ~90% to 78% — shift toward data theft and extortion without encryption

**Most relevant angles for this post:**
- AI as attack force multiplier (speed, scale, quality of lures)
- AI-enabled social engineering: deepfakes, synthetic personas, automated extortion
- LOTAIL: the enterprise AI platform as an attack tool
- Identity as the new perimeter — and why AI agents amplify this risk
- The 90% preventable-gaps finding: existing controls fail not because they are wrong but because AI changes the speed equation

---

## Notes

- The Unit 42 IDPI research is the single strongest anchor source for the adversarial/technical threat angle.
- The Unit 42 IR Report 2026 is the strongest data-backed anchor for the broader threat landscape shift.
- The BVP and iEnable governance sources together build the "AI agents as employees without controls" argument.
