# Content Plan: "The DLP Blind Spot: What AI-First Companies Are Missing About Data Loss Prevention"

## Framing

The thesis: DLP was built to watch doors. AI-first companies no longer have doors — they have an open floor plan where every conversation is a potential exit. Traditional DLP monitors files in transit and pattern-matches against known data signatures. AI changes both the *channel* (prompts, clipboard pastes, RAG retrievals) and the *attacker* (sometimes it is the AI itself). The controls that protected the last decade's enterprise do not protect this one.

**Tone:** Calm, analytical, practitioner-level. The audience has DLP on their radar — the goal is to sharpen their mental model, not alarm them. Written for CISOs, Head of AI/Data, and strategy leaders who want depth.

**Audience:** Data & AI strategy professionals, CISOs, senior tech leaders on Medium.

**Core message:** Traditional DLP has three blind spots in an AI-first company: it cannot see inside prompts, it cannot reason about context (only patterns), and it has no model for AI agents as data actors. Fixing the blind spot requires updating all three.

**Reading time:** ~10 minutes

---

## Core Analogy: The Glass Office

> Imagine your office has floor-to-ceiling glass walls. Your security guard stands at the front door and checks every bag going out. They are very good at their job: they catch files on USB drives, documents in briefcases, and laptops under coats.
>
> One day the company installs a phone on every desk. Employees can now read any document out loud through the phone. The security guard at the door cannot hear phone calls. He is still doing his job perfectly — he is just watching the wrong thing.
>
> That is what happened when employees started using AI tools. The documents stayed at the desk. The contents walked out through the prompt.

This analogy anchors the post's central argument:
- Traditional DLP = the guard at the door (files, transfers, known patterns)
- AI prompts, clipboard pastes, and RAG retrieval = the phone call (conversational, invisible to legacy controls)
- The AI agent with access to the whole floor = a new actor the guard was never designed to account for

Use this analogy in the opening to make the problem vivid before introducing technical concepts. Return to it briefly in the closing.

---

## Article Structure

### 1. Hook — The Guard at the Door (~200 words)

Open with the glass office analogy in full.

Then ground it in a real case: Samsung's semiconductor division, March 2023. Within three weeks of authorizing ChatGPT for internal use, engineers had pasted proprietary source code, hardware testing sequences, and meeting notes into the chatbot. The data entered OpenAI's training pipeline. There was no mechanism to retrieve it.

Samsung had security policies. Neither awareness campaigns nor standard controls were designed to intercept a developer asking an AI to fix a bug — because the input looked like a question, not a file transfer. (Samsung implemented dedicated DLP controls *after* the incident — a pattern that repeats across the industry.)

> "The data did not leave through the door. It left through a conversation."

This sets the central tension: the threat has not changed (sensitive data leaving the organization), but the *channel* has — and the controls have not kept up.

**Source:** Samsung/ChatGPT incident (March 2023, documented)

---

### 2. What Traditional DLP Was Built For (~250 words)

Briefly explain how DLP works — not to educate, but to establish the contrast.

Classic DLP operates on three assumptions:
1. **Known channels:** email attachments, USB drives, web uploads, cloud sync. DLP monitors these pathways.
2. **Pattern recognition:** it scans for signatures — credit card numbers, SSNs, keywords like "CONFIDENTIAL," regex patterns for source code. It flags matches.
3. **Files as the unit of analysis:** data moves in containers (files, attachments). DLP inspects the container.

These assumptions were reasonable in 2010. They were still largely valid in 2020. In 2026, they miss the fastest-growing exfiltration vector entirely.

ChatGPT alone generated 410 million DLP policy violations in a single year — a 99.3% year-over-year increase. That figure comes from organizations that *had* DLP coverage. For the organizations without browser-layer visibility, the number was not lower — it was simply invisible.

**Source:** Zscaler AI Prompt Data Leakage analysis (2026)

---

### 3. The Three Blind Spots (~700 words — the analytical core)

Structure as three named blind spots. Each one gets a crisp diagnosis, a real example or data point, and a single-sentence implication.

---

**Blind Spot 1: The Prompt Is Not a File**

Traditional DLP inspects files. Prompts are not files — they are conversations. When an employee pastes a revenue forecast, a legal brief, or a strategy document into ChatGPT, the transfer happens as an HTTPS-encrypted JSON payload inside a WebSocket stream. Classic network DLP cannot parse it. Endpoint DLP does not see it unless specifically configured for browser-layer interception.

The transfer looks like a browser session. Which it is.

Key data: 77% of employees paste data into GenAI tools. 82% of that activity happens via *personal accounts* — the free ChatGPT login, the consumer Claude tab — that have no enterprise audit trail and no DLP coverage whatsoever.

GenAI now accounts for 32% of all corporate-to-personal data exfiltration — making it the #1 vector for corporate data leaving sanctioned environments.

> The controls are still watching the front door while everyone is using the side entrance.

**Sources:** ShareFile/Progress research (2026); Zscaler (2026)

---

**Blind Spot 2: Patterns Cannot Catch Context**

Traditional DLP classifiers were built around structured data: credit card formats, SSN patterns, keywords, digital watermarks. This works for regulated data types.

It fails completely for the data that matters most in an AI-first company: strategic plans, M&A targets, source code architecture, customer insights, competitive intelligence. None of these match a regex. A paragraph describing an acquisition target looks like ordinary business prose. A prompt summarizing Q3 forecast does not trigger a "confidential" keyword filter unless someone manually labeled the source document — which most organizations have not done.

This is not a gap in DLP implementation. It is a gap in DLP *design*. Pattern matching was never built to detect meaning.

The implication: the most sensitive data in any AI-first company — its strategic thinking, its proprietary methods, its competitive positioning — is largely invisible to traditional DLP. Employees can exfiltrate it through AI prompts with no friction and no alert.

**Source:** Aiceberg analysis; Forcepoint DLP for AI (2026)

---

**Blind Spot 3: The AI Agent Is a Data Actor**

This is the deepest blind spot — and the most dangerous in a company deploying AI agents at scale.

Traditional DLP models have two actors: humans (insiders, employees) and systems (file servers, cloud storage). Controls are designed around human behavior and file movements.

AI agents are neither. They can autonomously retrieve enterprise data through RAG pipelines, summarize it, pass it to other agents, embed it in outputs, and transmit it to external APIs — all without a human initiating any of these steps.

Two structural problems:

First, **the relevance-authorization gap.** RAG systems rank documents by semantic relevance, not by authorization. In a poorly architected enterprise RAG deployment — where multiple business units, customers, or user groups share infrastructure — a query from one tenant can surface another's confidential data simply because it scored highest on relevance. A peer-reviewed study (arxiv 2605.05287, ACM CAIS '26) found that ungated retrieval leaks cross-tenant data in 98–100% of probes. DLP has no visibility into retrieval-layer data movement.

Second, **the trust boundary failure.** The Microsoft Copilot EchoLeak vulnerability (CVE-2025-32711, CVSS 9.3) demonstrated this at scale: a single malicious email bypassed Copilot's prompt injection classifier, link redaction, Content-Security-Policy, and reference safeguards — and silently exfiltrated enterprise data. No file moved. No anomalous traffic crossed the perimeter. The security stack reported all-clear because the violation occurred between the retrieval index and the generation model — a layer traditional security tools were never designed to observe.

> DLP did not miss this because it was poorly configured. It missed this because the violation happened in a place DLP was never built to look.

**Sources:** RAG security research (arxiv 2605.05287, 2026); Microsoft Copilot EchoLeak (CVE-2025-32711, June 2025); VentureBeat analysis (Feb 2026)

---

### 4. The Permission Prompt Trap: When the User Becomes the Last Line of Defense (~300 words)

This blind spot does not live in the network stack or the RAG pipeline. It lives in the moment an employee reads a popup and clicks "Allow."

AI tools — especially agentic systems connected via MCP (Model Context Protocol) — routinely ask users for permission before accessing data, tools, or services. In principle, this sounds like good security design: human-in-the-loop, explicit consent. In practice, it creates a structural problem that no amount of user awareness training can solve.

**The consent fatigue problem.** When an AI agent runs a multi-step workflow, it may trigger dozens of tool calls. Each one can produce a permission prompt: "May I access your calendar?" "May I read this file?" "May I send this email?" Users confronted with an unbroken stream of technical permission requests do one of two things: they read the first one carefully and click "Allow" reflexively on everything that follows, or they grant blanket "Always Allow" access upfront to stop the interruptions. Either way, they have effectively delegated their entire data access footprint to the agent — without understanding what they authorized. Research on MCP deployments documents this directly: "over time, repetitive prompts induce consent fatigue, causing users either to click 'Allow' reflexively or to grant blanket permissions that exceed their original intent." (arxiv 2605.11360, 2026)

**The comprehension gap.** Even when users do read the prompts, most cannot evaluate them meaningfully. "This tool requires access to your connected file systems, APIs, and databases" is accurate — and completely opaque. The employee does not know which files, which APIs, what the agent will do with them, or what the DLP implications are. They are being asked to make a data governance decision without the information or training to make it.

**The real-world consequences.** This is not a theoretical risk. In 2025, an auto-approve "Turbo mode" in a developer agent led to the deletion of a user's entire D:\ drive. In 2026, a Claude-powered coding agent deleted a company's production database and all backups in a single API call — despite explicit system-prompt rules prohibiting destructive operations. An OpenClaw agent deleted a researcher's emails despite explicit instructions not to. These were not security breaches in the traditional sense. They were permission grants the user did not understand, executed faithfully by an agent that had no mechanism to know better.

**What this means for DLP.** When users grant broad AI permissions they don't fully understand, DLP controls downstream are working against an already-authorized data flow. The agent is not exfiltrating data — it is accessing data the user said it could access. Traditional DLP has no model for this scenario. The access looks legitimate because it *is* legitimate — in a purely technical sense. The data governance failure happened at the consent layer, not the network layer.

**The fix is not "better training."** Users cannot be expected to evaluate enterprise data governance implications in real time, under deadline pressure, for every AI interaction. The fix is architectural: organizations must pre-define what AI tools are permitted to access, enforce those boundaries at the infrastructure layer (not the user prompt layer), and reserve explicit human approval only for genuinely high-risk operations — not routine workflow steps. Goal-scoped, time-limited permissions that expire automatically are more protective than any "May I?" popup.

> The permission prompt makes the user feel in control. The DLP problem is that they are not — and neither is the security team.

**Sources:** arxiv 2605.11360 (ConLeash, consent fatigue in MCP authorization, 2026); PolicyLayer MCP Security Audit (1,787 servers, May 2026 — 96.8% of tools carry no warning about side effects); Microsoft Agent Governance Toolkit blog (April 2026); TrueFoundry MCP Security guide (2026)

---

### 5. The Shadow AI Multiplier (~300 words)

These three blind spots are serious in a controlled AI environment. They become catastrophic when layered with Shadow AI.

Shadow AI is the unsanctioned AI ecosystem that lives beneath the security team's visibility: personal ChatGPT subscriptions, consumer Claude accounts, AI browser extensions, local LLMs, and personal API integrations that connect enterprise data to external models with no oversight.

Key numbers:
- 45% of employees actively use AI tools
- Nearly half access them via personal accounts with no enterprise audit trail
- 65% of Samsung employees surveyed said they believed ChatGPT posed security risks — and used it anyway

The risk is not malicious intent. The risk is productivity instinct. An employee who needs to summarize a document, debug code, or draft a communication will use the fastest available tool. If the fastest available tool is a personal AI account, that is what they will use.

Shadow AI means every blind spot is larger than it looks. The organization is not just blind to what goes into the enterprise AI deployment. It is blind to an entire parallel ecosystem of AI interactions carrying enterprise data.

**Sources:** ShareFile research (2026); Samsung incident (2023)

---

### 6. Wer muss was tun? Verantwortlichkeiten klar trennen (~350 words)

Dies ist der Abschnitt, der in den meisten technischen Artikeln fehlt — und der Grund, warum DLP-Programme scheitern, obwohl die Technik funktioniert.

**Die Organisation trägt die Architektur-Verantwortung.**

Mitarbeitende können nur das richtig machen, was die Organisation ihnen ermöglicht. Die Verantwortung der Organisation ist strukturell:

- **Sanctioned AI first.** Stell den Mitarbeitenden eine enterprise-taugliche AI-Option bereit (ChatGPT Enterprise, Claude for Work, Copilot mit Daten-Residenz-Garantie). Wer das nicht tut, erzeugt zwangsläufig Shadow AI — nicht durch schlechten Willen der Mitarbeitenden, sondern durch eigenes Governance-Versagen. Studien zeigen: eine sanktionierte AI-Option reduziert Shadow-AI-Nachfrage um 60–80%.
- **Technische Durchsetzung, nicht nur Policy-Dokumente.** Ein AI Acceptable Use Policy (AUP), das nur in der Onboarding-Mappe liegt, ist kein Sicherheitscontrol. Enforcement braucht drei technische Schichten: Netzwerk-/Browser-Layer für den Zugang, DLP-Tooling für den Datenstrom, Runtime-Monitoring für die AI-Interaktion selbst. Nur alle drei zusammen schließen den Kreis.
- **AI-Tool-Inventar als Pflichtaufgabe.** Die Organisation muss wissen, welche AI-Tools ihre Mitarbeitenden tatsächlich nutzen — nicht welche sie genehmigt hat. Das sind zwei verschiedene Listen. Erst die Sichtbarkeit schafft die Grundlage für Governance.
- **Graduated Enforcement, kein Bann.** Samsung hat den Bann versucht. Er hat Tage gedauert und die Nutzung in den Untergrund getrieben. Der richtige Reflex ist nicht "sperren", sondern: warnen, coachen, umleiten, im Wiederholungsfall blockieren. DLP-Programme, die nur blockieren, werden von Mitarbeitenden aktiv umgangen.

**Die Mitarbeitenden tragen die Daten-Verantwortung im Alltag.**

Mitarbeitende sind keine Sicherheitsexperten — aber sie sind die einzige Instanz, die im Moment der Eingabe weiß, was sie gerade eingeben. Ihre Verantwortung ist operativ:

- Klassifizierung im Kopf: Bevor etwas in ein AI-Tool eingegeben wird, eine Sekunde innehalten: Handelt es sich um interne, vertrauliche oder regulierte Information?
- Bekannte Risikokategorien meiden: Kundendaten, Quellcode, Strategiepläne, Finanzdaten, HR-Informationen — nicht in unsanktionierte AI-Tools, never.
- Fehler melden, nicht verstecken: Eine Kultur, in der man Fehler schnell und ohne Konsequenz melden kann, ist der wichtigste Frühwarn-Mechanismus überhaupt. Governance Theater entsteht nicht aus böser Absicht, sondern aus Schweigen.
- Sanctioned Tools nutzen, auch wenn der persönliche Account "schneller" wäre.

> The policy says: "don't share confidential data with AI tools." The employee at 11pm before a deadline has a different calculus. The organization's job is to make the right behavior the easy behavior — not to rely on willpower.

**Fazit:** Wer DLP als reines Technologieproblem behandelt, verliert. Wer es als reines Awareness-Problem behandelt, verliert ebenfalls. Es ist beides: Architektur-Verantwortung der Organisation + operativer Daten-Gewissen der Mitarbeitenden.

**Sources:** Repello AI (AI AUP guide, 2026); BeyondScale (2026); Security Boulevard AI governance framework (2026); IBM Security Cost of a Data Breach Report 2025 (Shadow AI tax $670K)

---

### 7. Fortschritt messen: Was zählt aus CISO-Sicht? (~300 words)

"You can't protect what you can't see — and you can't improve what you can't measure."

Das Grundproblem vieler DLP-Programme: sie erzeugen viele Alerts, aber wenig Evidenz für tatsächliche Risikoreduzierung. Boards und Regulatoren wollen keinen Alert-Tsunami — sie wollen wissen, ob das Programm wirkt.

Vier Kennzahlen, die wirklich zählen:

**1. Sensitive Prompt Rate (Trend, nicht absolut)**
Wie viele AI-Interaktionen enthalten sensitive Daten — und entwickelt sich dieser Anteil nach unten? Ein sinkender Trend über 90 Tage ist das stärkste Signal, dass Awareness und Enforcement kombiniert wirken.

**2. Shadow AI Coverage Ratio**
Wie viele AI-Tools werden im Unternehmen tatsächlich genutzt (entdeckt via Endpoint, Browser, Netzwerk-Monitoring) versus wie viele sind sanktioniert und governed? Ein Coverage Ratio von < 50% bedeutet: die Organisation sieht weniger als die Hälfte der Fläche, die sie schützen müsste.

**3. Override Rate und Repeat-Offender Rate**
Wie oft umgehen Mitarbeitende DLP-Warnungen (Override Rate)? Wie viele derselben Personen tun es wiederholt (Repeat-Offender Rate)? Ein hoher Override Rate signalisiert entweder zu viele False Positives (das Enforcement nervt legitime Arbeit) oder zu wenig Awareness. Eine hohe Repeat-Offender Rate zeigt, wo gezielte Intervention nötig ist.

**4. Agent Data Access Auditability**
Kann das Unternehmen für jeden seiner AI-Agenten rekonstruieren: Was hat er gelesen? Was hat er summarisiert? Was hat er übertragen? Wenn diese Frage nicht innerhalb von 24 Stunden beantwortet werden kann, ist der Audit-Trail unzureichend — unabhängig von allem anderen.

Was **nicht** zählt als primäres KPI: absolute Alert-Zahlen. Viele Alerts bedeuten oft vor allem: zu viele False Positives, zu wenig Tuning, zu viel Lärm für das SOC-Team.

**Reife-Benchmark:** Ein modernes DLP-Programm für AI-first Companies braucht 90 Tage von Discovery bis ersten Enforcement-Ergebnissen — nicht 6–9 Monate wie bei klassischen DLP-Rollouts. Wer länger braucht, hat wahrscheinlich zuerst ein Inventar-Problem.

**Sources:** Sentra (90-day DLP modernization roadmap, 2026); Software Analyst DLP Reset research (2026); LessIT DLP KPI framework; OAD Technologies DLP effectiveness framework 2026

---

### 8. What To Do — A Decision Framework for CISOs and Heads of AI (~450 words)

Most guidance on DLP ends with a list of tools. This is more useful than that: a sequenced set of decisions, from the ones that cost nothing to the ones that require budget.

**Decision 1 — Architecture before tooling (no budget required)**

The single most impactful move does not require a procurement process. Deploy a sanctioned, enterprise-grade AI option — ChatGPT Enterprise, Claude for Work, Copilot with data residency guarantees — and enforce access to it via Single Sign-On. This one decision:
- Reduces Shadow AI demand by 60–80%, because employees stop going rogue when there is a legitimate alternative that actually works
- Creates an audit trail for every AI interaction by default
- Gives the organization a policy enforcement point it did not have before

Pair this with a clear AI Acceptable Use Policy — not a document that lives in the onboarding folder, but one backed by three layers of technical enforcement: network-level controls that block unapproved AI services, browser-layer monitoring where data is actually typed and pasted, and runtime monitoring of AI interactions. Policy without technical enforcement is wishful thinking.

> The most expensive mistake: buying a $300K/year platform before deciding what a sanctioned AI looks like.

**Decision 2 — What already works, and what is still maturing**

Be honest with your board and your team about where the market is.

*What is production-ready today:*
- Browser-layer interception (catching clipboard pastes before they reach an AI API) is proven. Nightfall, Menlo, and Zscaler all have deployments in production. This is no longer a promise.
- Sanctioned AI plus SSO, as described above, demonstrably reduces shadow AI volume.
- Graduated response — warn, coach, redirect, block — works better than blanket bans. Employees who understand *why* something was blocked change their behaviour. Employees who hit an unexplained block look for a workaround.

*What is still maturing:*
- Semantic classification of unstructured strategic content (M&A plans, competitive intelligence, proprietary methods) is promising but requires significant tuning. Ninety-five percent accuracy sounds good until you calculate the false positive volume at enterprise scale.
- AI agent audit trails — comprehensive logging of what an agent read, summarized, and transmitted — are technically possible but not yet a commodity. If you have deployed AI agents, assume your audit coverage has gaps until proven otherwise.
- Access controls inside AI knowledge bases (ensuring the agent can only retrieve what the querying user is permitted to see) are solved in architecture but rarely implemented consistently in practice. This is the gap most likely to produce a governance failure that surprises a CISO.

**Decision 3 — When to buy a dedicated platform**

There are two distinct problems in the market, and confusing them leads to buying the wrong thing.

*If your AI security engineering team is building LLM-powered applications* and needs to protect those applications at the prompt and response layer — detect prompt injection, redact PII before it hits the model, scan outputs for sensitive content — open-source tooling is a legitimate starting point. LLM Guard (now under Palo Alto Networks following their 2025 acquisition of Protect AI) covers the basics and is free. The strategic roadmap under Palo Alto is uncertain; treat it as a foundation to build on, not a long-term platform bet.

*If your problem is hundreds of employees using dozens of AI tools you do not fully control* — Shadow AI, clipboard exfiltration, SaaS integrations running in the background — open-source tooling does not cover this surface. This is where commercial platforms earn their cost. Nightfall is the most directly positioned: it monitors across SaaS, browser, and endpoint layers with a single policy engine, and integrates with the tools employees actually use. The buying decision is not "do I need this?" — it is "is the problem broad enough to justify enterprise pricing?"

The diagnostic question: can you answer, right now, which AI tools your employees used in the last 30 days and what data entered those tools? If not, you have a visibility problem before you have a tooling problem. Start there.

**Sources:** Nightfall AI (2026); Menlo AI Adaptive DLP (2026); GitHub protectai/llm-guard; CTAIO AI Security Stack Guide 2026; Nightfall AI Review (aiflowreview.com, 2026); Repello AI AUP guide (2026)

---

### 9. Closing — The Guard Is Still There, But the Building Changed (~150 words)

Return to the glass office analogy.

The security guard at the door did not fail. They are still doing exactly what they were designed to do. The building changed around them.

The organizations navigating this well are not the ones that banned AI (Samsung tried that — it lasted weeks and drove usage underground). They are the ones that extended their security architecture to match the new topology: browser-layer enforcement, semantic classification, agent-aware access controls.

DLP is not dead. But the version that watches file transfers and pattern-matches against SSN formats is watching the wrong things in an AI-first company.

The question is not whether to use AI. The question is whether your data protection architecture has caught up to the way your employees — and your AI systems — are actually moving data.

End with a direct question for the reader:
> "Does your DLP stack know what your AI tools are doing right now? If you are not sure, the answer is probably no."

Close with a call for comments: What has your organization found most challenging about DLP in the AI era?

---

## Lessons Learned for the Reader

1. Traditional DLP was built for files moving through known channels. AI prompts, clipboard pastes, and RAG retrievals are none of these — and they are now the dominant data movement channel.
2. Pattern matching cannot protect strategic intelligence. The most valuable data in an AI-first company — plans, methods, competitive insights — does not trigger keyword filters.
3. AI agents are a new category of data actor. They retrieve, synthesize, and transmit enterprise data autonomously. Access control logic designed for human users does not cover them.
4. Shadow AI means the problem is larger than it appears. The employee using a personal AI account is not being reckless — they are being productive. The gap is architectural, not behavioral.
5. Effective AI-era DLP requires three layers: browser/endpoint interception, semantic classification, and agent-aware access controls at the retrieval layer.

---

## Suggested Graphs / Visuals

1. **The Three Blind Spots** — Diagram showing what traditional DLP sees vs. what it misses: the prompt channel, the contextual content, the agent data actor.
2. **The Exfiltration Channel Shift** — Shift from file-based exfiltration to prompt-based: visual showing GenAI as #1 corporate-to-personal exfiltration vector (32%), copy-paste overtaking file transfers.
3. **AI Agent Data Access Model** — Diagram showing the RAG pipeline gap: user permissions exist at the access layer, but the retrieval layer ranks by relevance, not authorization. Where DLP observes vs. where the violation occurs.

---

## Sources Mapped to Sections

| Section | Source |
|---------|--------|
| 1. Hook | Samsung/ChatGPT incident (March 2023) |
| 2. Traditional DLP | Zscaler ThreatLabz 2026 AI Security Report (via Zscaler blog) |
| 3. Blind Spot 1 | ShareFile/Progress blog (2026, cites SC World, eSecurity Planet, The Hacker News); Zscaler ThreatLabz 2026 |
| 3. Blind Spot 2 | Aiceberg (vendor analysis, 2026); Forcepoint DLP for AI (vendor analysis, 2026) |
| 3. Blind Spot 3 | arxiv 2605.05287 (peer-reviewed, ACM CAIS '26); CVE-2025-32711 EchoLeak; VentureBeat (Feb 2026) |
| 4. Permission Prompt Trap | arxiv 2605.11360 (ConLeash, 2026); PolicyLayer MCP Audit (2026); Microsoft AGT (2026); TrueFoundry (2026) |
| 5. Shadow AI | ShareFile blog (2026); Korea Herald / Samsung DX survey (2023) |
| 6. Verantwortlichkeiten | Repello AI (2026); BeyondScale (2026); Security Boulevard (2026); IBM Security 2025 |
| 7. CISO Metrics | Sentra (2026); Software Analyst DLP Reset (2026); LessIT KPI framework; OAD Technologies (2026) |
| 8. Decision Framework | Nightfall AI (2026); Menlo (2026); GitHub protectai/llm-guard; CTAIO (2026); aiflowreview.com (2026); Repello AI (2026) |
| 9. Closing | — (synthesis) |

---

## Source Verification Notes

Verified 2026-05-24. Status of each claim used in the plan:

### Samsung/ChatGPT incident (Hook)
**Status: CONFIRMED**
- Three incidents confirmed: source code, hardware yield/test sequences, meeting notes — March 2023
- Company-wide ban issued May 2023
- **Caveat:** The claim "no mechanism to retrieve it" is accurate for the time (OpenAI's default trained on inputs; opt-out was added only after public backlash). Do not overstate permanence — frame as "at the time, there was no mechanism to selectively remove submitted data."
- **Caveat:** The claim "Samsung had DLP" is from secondary analysis (StealthCloud case study), not Samsung's own disclosure. Frame as: Samsung implemented DLP *after* the incident, not necessarily before. Safe to say "neither awareness campaigns nor the controls in place were designed to intercept a developer asking an AI to fix a bug."
- Sources confirmed: Korea Herald (May 2023), TopAIThreats.com registry, StealthCloud analysis

### Zscaler: 410 million DLP violations / 99.3% YoY increase
**Status: CONFIRMED with attribution note**
- Stat confirmed in Zscaler blog post (May 2026), attributed to ThreatLabz 2026 AI Security Report
- **Attribution:** Primary source is the ThreatLabz 2026 AI Security Report, not the blog post itself. Cite as: *ThreatLabz 2026 AI Security Report (Zscaler)*. Do not cite the blog as the source.

### ShareFile stats: 77%, 82%, 32%, 45%
**Status: CONFIRMED with chain-of-citation note**
- All four figures confirmed in ShareFile/Progress blog (March 2026)
- **Important:** ShareFile is a secondary source; each stat cites a different primary source:
  - 77% (employees paste data into GenAI tools) → eSecurity Planet
  - 82% (via personal accounts) → The Hacker News
  - 32% (GenAI = #1 corporate-to-personal exfiltration vector) → SC World
  - 45% (employees actively use AI tools) → SC World
- These are legitimate stats from credible trade press, but they trace back to various vendor research reports. When writing, attribute to the ShareFile article or cite as "industry research" — do not present them as ShareFile's own research.

### arxiv 2605.05287: "ungated retrieval leaks cross-tenant data in 98–100% of probes"
**Status: CONFIRMED with framing note**
- Stat confirmed directly in paper Section 1.3: "empirical evidence that ungated retrieval leaks cross-tenant data in 98–100% of probes"
- Also confirmed in Section 5.2: "Without [gating], nearly all cross-tenant probes return unauthorized data regardless of orchestration mode"
- **Important framing nuance:** This stat is specific to a **multitenant RAG scenario** — tenant A querying for tenant B's data. The PLAN.md uses it in a broader enterprise context ("a query from one user context can surface another's confidential data"). This is a valid generalization of the finding, but be precise when writing: frame it as the cross-tenant/overprivilege scenario, which is the paper's actual scope.
- Paper is peer-reviewed, published at ACM CAIS '26 (May 2026). High-quality source.

### EchoLeak CVE-2025-32711, CVSS 9.3
**Status: CONFIRMED**
- All claims confirmed by VentureBeat (Feb 2026) citing Microsoft's advisory and Aim Security research
- Zero-click confirmed, bypassed 4 defense layers (prompt injection classifier, link redaction, CSP, reference mentions), CVSS 9.3 confirmed
- Second incident (CW1226324, Jan–Feb 2026) also confirmed — code bug, not exploit, but identical outcome
- **No corrections needed.** Claims in PLAN.md are accurate.

### Samsung 65% survey
**Status: CONFIRMED with scope note**
- Confirmed directly in Korea Herald: "In a survey Samsung conducted of its DX division staff last month, 65 percent of respondents said they believe security risks can occur from using ChatGPT for work."
- **Scope note:** This survey was of the **DX (Device eXperience) division**, not the semiconductor division where the leak occurred. Both are Samsung divisions but distinct units. The irony (65% believed the risk, and used it anyway) is valid — but be precise: "In a Samsung internal survey of its DX division, 65% of employees said they believed ChatGPT posed security risks."

### Aiceberg and Forcepoint (Blind Spot 2: pattern matching cannot catch context)
**Status: CONFIRMED as vendor analysis**
- Both sources confirm the argument that regex/keyword DLP cannot detect strategic/contextual sensitive data
- **Nature of source:** These are vendor white papers and product pages, not independent research. The argument is analytically sound and widely corroborated, but attribute appropriately. In the post, frame as "industry analysis" or use for supporting color rather than as the sole basis for a factual claim.
- No numerical stats from these sources are used — only the qualitative argument, which is solid.
