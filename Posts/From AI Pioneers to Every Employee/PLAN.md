# PLAN.md — From AI Pioneers to Every Employee

## Meta

- **Title:** From AI Pioneers to Every Employee
- **Subtitle:** Why today's agentic tools are built for individuals — and what that means for your organization
- **Target audience:** Enterprise leaders, transformation managers, CIOs, CDOs — anyone responsible for getting AI to work *across* their organization, not just for their best individuals
- **Author voice:** Strategic, analytical, from behind the scenes. Concrete observations from practice. Cuts through the hype.
- **Target reading time:** 7–8 minutes
- **Core argument:** The most powerful AI tools available today — OpenCode, Claude Desktop, Hermes, Claude Code — are architected for individual power users. They optimize *one person's* workflow brilliantly. But they have a structural problem: the knowledge and capability they build up cannot be transferred to colleagues. There are no methods, no shared workflows, no governance, and the required skills effectively limit access to developers and technical users. This is not a training gap. It is an architectural gap. And solving it requires a different kind of thinking.

---

## The Four Hypotheses (from the author)

These are the core observations that drive the post — stated as hypotheses to be examined, supported, and developed into recommendations:

1. **Individual optimization trap:** Agentic tools (OpenCode, Claude Desktop, Hermes) are designed to make *one person* more powerful. Their architecture — local context, personal sessions, individual configurations — is optimized for personal productivity, not organizational capability.

2. **Knowledge stays trapped:** What a power user builds up inside an agentic tool — their prompts, their workflows, their context files, their agent configurations — cannot be meaningfully transferred to a colleague. There are no standard methods, procedures, or handoff formats for this. The knowledge evaporates when the person logs off or changes roles.

3. **No governance, no structure:** Usage of these tools is highly individual, varies from person to person, and operates largely without governance. There are no shared standards for how tasks should be approached, what outputs look like, or how quality is assured. Every user is their own island.

4. **Developer skills required:** Using these tools effectively requires skills that are close to software development — configuring agents, writing context files, managing MCPs, understanding model behavior. This works fine if all your users are developers. For most enterprise workforces, it creates a hard barrier.

---

## Vivid Analogy

**The Craftsman's Workshop**

Imagine a master craftsman who has, over thirty years, built up the most extraordinary workshop in the city. Every tool is perfectly placed. Every jig is custom-made for his specific way of working. Every drawer is labeled in a system only he understands. When he works in that shop, he is formidably fast and precise — he can produce in one day what would take another craftsman a week.

Now his company needs to scale. They hire ten more craftsmen and build ten new workshops.

Each craftsman arrives and... starts from scratch. The master's jigs don't fit their grip. His labels don't match their mental model. His tool placement makes no sense to them. Worst of all, the master himself struggles to explain why things are where they are — it has become tacit knowledge, embedded in decades of practice, inseparable from his specific hands.

**This is the state of enterprise AI today.** The masters are the AI pioneers — the developers and power users who have built extraordinary personal setups with Claude Desktop, OpenCode, or Hermes. Their productivity is real. Their results are visible. But their workshop cannot be replicated. Their knowledge cannot be transferred. And the ten new craftsmen hired to "scale AI" are starting from scratch, often with tools that weren't designed for their hands.

---

## Structure

### 1. Opening — The Invisible Architecture Problem (≈300 words)

Start with an observation: organizations are watching their AI pioneers achieve remarkable results — 5x productivity, hours of work done in minutes, capabilities that look almost like magic to colleagues. Leadership concludes: "We need more of this. Let's roll it out to everyone."

And then it doesn't work.

Not because the tools aren't good. The tools are extraordinary. But because the architecture that makes them powerful for an individual is precisely what makes them hard to scale across an organization.

Introduce the core tension: the most capable agentic tools — OpenCode, Claude Desktop, Claude Code, Hermes — were built for individual empowerment. That is a design choice, not an oversight. But it has organizational consequences that most leaders haven't fully reckoned with.

**Key frame:** This is not about motivation, training hours, or change management resistance. It is about architecture.

---

### 2. How Agentic Tools Actually Work — and Why That Matters (≈400 words)

Explain, accessibly, what makes agentic tools different from earlier AI tools — and what their architectural choices reveal about who they were designed for.

**Key points:**
- Agentic tools like OpenCode or Claude Desktop work by combining a powerful model with *context* — files, instructions, prior conversations, custom configurations
- That context is built up by the individual user over time: their AGENTS.md files, their MCP configurations, their prompt libraries, their knowledge files
- This personal context is what makes these tools feel powerful — the AI "knows" the user's domain, preferences, and workflows
- But this context lives on the individual's machine or account. It is not shared. It is not versioned for teams. It is not transferable without significant effort
- The Enterprise AI Show (episode 1034) put it directly: *"the way that people are interacting with AI for the most part is very individualistic... it's very hard to share a chatbot session... agents are still sort of in the building phase"*

**Introduce the craftsman analogy here.** (Full text as written above.)

---

### 3. The Four Structural Gaps (≈600 words — the analytical core)

Examine each of the four hypotheses as a concrete structural gap:

#### Gap 1 — Individual Optimization Trap
- Tools like Claude Desktop, OpenCode, and Hermes are architected around single-user sessions
- Their power comes from personal context accumulation — which is, by design, personal
- Goldman Sachs CIO Marco Argenti called 2026 the era of "personal agents" — this framing is revealing: the agent serves *you*, not your team
- Contrast: enterprise software (CRM, ERP, project management) is explicitly multi-user from the start. Agentic tools are not. They are closer to personal productivity software — Excel, not SAP.
- The gap: individual gains do not compound into organizational capability

#### Gap 2 — Knowledge Trapped in the Session
- When an AI pioneer figures out the best way to structure a research task, write a complex document, or manage a multi-step workflow, that knowledge lives in their head and their personal config files
- There are no standard formats for exporting "how I use AI" in a way colleagues can import and use
- Brian Gracely (Enterprise AI Show #1034): *"It's very hard to share... a chatbot session. There's very hard to sort of share agents... the sharing piece, the collaboration piece, is sort of an afterthought that people are figuring out ways to hack around"*
- Docsie's analysis is sharp: general-purpose AI tools "assume single user, single session. There is no concept of organizational ownership."
- The gap: tacit knowledge stays tacit. The pioneer's expertise doesn't diffuse into the organization

#### Gap 3 — No Governance, No Shared Standards
- In most organizations, AI tool usage is "a chaotic free-for-all" (Writer 2026: 55% describe it this way)
- Different people use different tools, different prompts, different quality standards — with no way to know if two people doing the "same" task with AI are producing comparable outputs
- The Enterprise AI Show (episode 1034) identifies the core tension: *"without some sort of centralized enterprise harness around all the tools... if they're not consistent, building consistency, building repeatable processes [is] difficult"*
- 67% of executives believe their company has already suffered a data breach from unapproved AI tool use (Writer 2026)
- The gap: individual freedom creates organizational risk and inconsistency. You cannot build a process on a foundation that varies person by person.

#### Gap 4 — Developer Skills Required
- Effective use of the most powerful agentic tools requires capabilities close to software development: configuring JSON files, writing markdown instruction sets, managing MCPs, understanding context windows and model behavior
- OpenCode's own documentation assumes terminal access, shell familiarity, API key management, and Git workflows
- This is fine for a development team. It is a hard barrier for most enterprise employees: finance professionals, HR teams, operations managers, legal staff
- The gap: the tools that produce the best results require skills that most non-technical employees don't have and shouldn't need

---

### 4. What This Means for Organizations Right Now (≈300 words)

Draw out the organizational consequence: the AI capability gap is not closing on its own. It is widening — precisely because the tools that produce the best individual results are the least accessible to non-technical employees.

**Key points:**
- 92% of C-suites are cultivating an "AI elite" (Writer 2026) — in part because the tools themselves drive elite formation
- The tools reward investment of time, technical skill, and personal configuration — which self-selects for the technically capable
- Meanwhile, the 80% of the workforce that cannot configure an MCP server is being offered a chatbot interface and told to "use AI"
- The result is not democratization. It is stratification.

**The uncomfortable question for leaders:** Are you planning to make *everyone* an AI power user — with all the skill requirements that entails? Or do you need a different model?

---

### 4b. The Pioneer's Dilemma — Speed vs. Compliance (≈350 words)

There is a fifth tension that deserves its own treatment, because it directly affects the people organizations most need to retain: the pioneers themselves.

The standard enterprise response to the governance and skills gaps is to standardize on a managed platform: Microsoft Copilot, a corporate ChatGPT deployment, a locked-down Copilot Studio instance. These platforms are real solutions to real problems — they provide governance, shared access, audit trails, and a learning curve most employees can manage.

But for the AI pioneer, they represent a step backward.

**Key points:**
- Microsoft Copilot's actual enterprise penetration tells the story: despite M365 having ~450 million paid seats, Copilot penetration hovers around 3% (Xenoss/Creati.ai, 2026). Only 5% of enterprises moved from pilot to larger deployment (Gartner). The reasons cited are not just cost — they include the tool feeling constrained compared to direct model access.
- The pioneer using OpenCode or Claude Desktop can iterate in seconds, configure custom agents, access the full capability of frontier models, and work in the terminal environment they already know. The enterprise Copilot user has guardrails, approval flows, and a restricted interface.
- Forcing the pioneer onto the enterprise platform to achieve consistency is not free. It costs the organization its fastest and most capable AI users — the very people it needs to generate the knowledge worth spreading.
- Brian Gracely (Enterprise AI Show #1034) names the incentive problem directly: if pioneers feel that sharing or conforming to an enterprise standard reduces their individual advantage, they won't do it. The system has to make contributing to the collective worthwhile.

**The real tension:** Governance tools slow pioneers down. Ungoverned individual tools don't scale. This is not a solvable problem with a policy memo. It requires a structural answer.

---

### 5. What a Different Model Looks Like (≈500 words)

Constructive and practical. This is where the post earns its place.

**Three directions worth watching:**

#### Direction 1 — Enterprise-Native Agentic Platforms
Tools like Dust, Microsoft Copilot Studio, and similar platforms are explicitly designed for multi-user, governed, enterprise deployment. They trade some of the raw power of individual agentic tools for shareability: shared agent spaces, permission-controlled knowledge bases, collaborative workflows. The pioneer's setup can become a team's setup.
- Dust's explicit pitch: "Most teams are stuck in single-player AI mode. Dust changes that with a multiplayer AI workspace."

#### Direction 2 — Making Knowledge Portable
The missing piece is not more training — it is infrastructure for making AI-generated knowledge and workflows portable between people. This means: shared prompt libraries, documented agent configurations, team-level context files, and explicit "AI handoff" formats. Some organizations are building this informally; it needs to become a standard practice.

#### Direction 3 — Role-Appropriate Access Layers
Not everyone needs the full power — and full complexity — of an agentic coding tool. The answer is not dumbing AI down but layering it appropriately: build governance-wrapped, role-specific AI capabilities for non-technical employees on top of the same powerful foundations. The power user configures the tool; the rest of the organization uses the result.

#### Direction 4 — The Translation Layer: Frontend Engineers as AI Democratizers
This is the most underexplored — and potentially the most powerful — answer to the pioneer's dilemma. Instead of forcing pioneers onto slower enterprise tools, or leaving the rest of the workforce with no access to pioneer-grade capabilities, a third path exists: **use engineers to translate pioneer achievements into enterprise-accessible tooling.**

The model works like this:
- The AI pioneer builds something extraordinary in OpenCode or Claude Desktop — a research workflow, a document analysis pipeline, a complex multi-step agent for a specific business task
- A **frontend or internal tooling engineer** takes that workflow and wraps it in a clean, simple UI — a form, a button, a Slack command — that any employee can use without understanding the underlying agent architecture
- The pioneer keeps their fast, powerful environment. The rest of the organization gets the *result* of that environment, packaged accessibly.

This is not a new concept — it mirrors the **internal tools movement** that has been running in software-forward companies for years. Platforms like Retool, ToolJet, and Superblocks exist precisely for this: letting a small engineering team build internal applications that expose complex backend capabilities through simple frontends. What is new is the AI layer.

The emerging role here could be called an **"AI Product Engineer"** or **"AI Translator"** — someone who understands both the agentic tooling landscape and enough frontend/product craft to turn a pioneer's working setup into something deployable at scale. Northflank has already framed the problem this way: *"The code generation problem is largely solved. Non-technical employees can describe what they need and have working code in minutes. The infrastructure gap is what prevents those apps from shipping securely."*

This direction also dissolves the pioneer's dilemma: the pioneer doesn't lose speed. They work the way they always have. The engineer handles the translation. Governance gets applied at the interface layer, not the exploration layer.

The challenge: this requires deliberately hiring or growing this translation capability — and most organizations haven't yet recognized it as a distinct role.

---

### 6. Takeaway and Call for Discussion (≈200 words)

The tools that make AI pioneers powerful are not the same tools that will make an entire organization capable. Recognizing that distinction is the first step.

The question is not "how do we get everyone using Claude Desktop?" — and it is equally not "how do we force the pioneer onto Copilot?" Both framings lead somewhere worse than where you started.

The real question is: **how do you build a system where the pioneer's speed is preserved, their achievements are translated into accessible form, and the rest of the organization benefits — without anyone having to sacrifice what makes them effective?**

That requires thinking about AI capability as a product — not a training program. It requires translation-layer engineers. It requires governance applied at the interface, not the exploration. And it requires letting go of the idea that enterprise AI means everyone using the same tool.

**Call for comments:** Is anyone in your organization playing the "translation" role — taking what a power user has built and making it accessible to the rest of the team? What does that look like in practice? I'd genuinely like to know.

---

## Proposed Graphics

One graph. As Mermaid `.mmd` files.

---

### Graph 1 — The Four Structural Gaps (place at start of Section 3)
**File:** `graph-1-four-gaps.mmd`

**Type:** Mindmap or flowchart with four branches

**Purpose:** Give the reader a visual map of the four gaps before diving into each. Serves as a navigation anchor for the analytical core of the post.

**Content:** Four nodes radiating from a central problem statement:
1. Individual Optimization Trap → knowledge and config optimized for one person
2. Knowledge Trapped in the Session → no transfer format, evaporates on logout
3. No Governance, No Standards → chaotic free-for-all, breach risk
4. Developer Skills Required → hard barrier for non-technical employees

---


| Ref | Source | Key Claim/Use |
|-----|--------|---------------|
| Primary | Enterprise AI Show #1034 (Brian Gracely) | Core hypotheses; tools are "very individualistic"; sharing is "an afterthought"; incentive problem for pioneers |
| F2 | Writer Enterprise AI Adoption 2026 | 55% "chaotic free-for-all"; 67% data breach risk; 92% cultivating AI elite |
| New | Xenoss / Creati.ai: Microsoft Copilot Enterprise Limitations | Copilot penetration ~3% of M365 seats; only 5% of enterprises scaled past pilot; $30/user/month cost barrier |
| New | Docsie: General AI Won't Replace Enterprise Knowledge | "Single user, single session. No concept of organizational ownership." |
| New | Dust.tt | "Most teams stuck in single-player AI mode" — solution direction 1 |
| New | Northflank: Non-technical employees building internal apps | "The code generation problem is largely solved... The infrastructure gap is what prevents apps from shipping securely." — evidence for translation-layer approach |
| New | Goldman Sachs / Marco Argenti (Jan 2026) | 2026 as era of "personal agents" — individual-centric design is deliberate |
| New | OpenCode/Claude Code documentation | Developer-level skills required (terminal, shell, API keys, MCP config) |
| Retained | BCG AI Radar 2026 | 10-20-70 principle; <1/3 upskilled 25%+ of workforce |
| Retained | Deloitte AI Pulse 2026 | 48% deployed AI without redesigning workflows |

---

## Source Verification Notes

- **Enterprise AI Show #1034** — CONFIRMED. Full transcript fetched and read. URL: https://docs.google.com/document/d/1I3fcQSpc6ALdt3bs8KnUEqmcn5R0qhHysHxn6BX6CRc
- **Writer 2026** — CONFIRMED (vendor research — attribute accordingly).
- **Xenoss / Creati.ai Copilot** — CONFIRMED with note. Copilot ~3% penetration and $30/seat price confirmed in search excerpts from xenoss.io and creati.ai. Gartner 5% scaling figure confirmed. Attribute as "Xenoss analysis citing Gartner" and "Creati.ai citing Bloomberg/Gartner."
- **Docsie** — CONFIRMED. URL: https://www.docsie.io/blog/articles/why-general-ai-wont-replace-enterprise-knowledge-systems/
- **Dust.tt** — CONFIRMED. URL: https://dust.tt
- **Northflank** — CONFIRMED. Quote verified in search excerpt. URL: https://northflank.com/blog/how-non-technical-employees-can-build-and-ship-internal-apps-with-ai-securely
- **Goldman Sachs / Marco Argenti** — UNVERIFIED. Appeared in search excerpt. Verify before quoting directly.
- **OpenCode documentation** — CONFIRMED. URL: https://opencode.ai/docs
- **BCG AI Radar** — CONFIRMED (verified previously).
- **Deloitte AI Pulse** — CONFIRMED with note (48% figure from search excerpt; verify exact wording before quoting).
