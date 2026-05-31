# Goals

## Metrics I Care About

- Posts shoud be readable by a technical interested but not very deeply involved person
- Posts should be readable within 5 to 10 minutes
- Post should contain at least one "Aha"-Moment
- Post's title should be catchy without sounding like click-baiting

## Current Posts (Q1 2026)

<!-- TODO: Update quarter and year -->

### Post 1: From Prompt Engineering to Context Engineering
Describe the transition from Prompt Engineering to Context Engineering
- Why it is important
- How it works
- What to keep in mind


### Post 2: Something dangerous is happening

Transfer of Matt Shumers post "Something big is happening" to the bad side.

- AI inherent threats, e.g. from MITRE ATLAS
- Threats from AI enhanced social engineering, e.g. from "The Economist": Slautering the pig
- Threats from internal AI Agents which act like "employees", but without established governance processes that exist for normal employees (they increasingly get access to ressources)
- Cases studies from Palo Alto's Unit 42 Global Incident Response Report 2026
- Rising scale and sophistication of attacs and Shorter time to react
- AI Threats and AI Agent security cannot be managed by conventional methods 
  - due to fast changing AI world
  - indeterministic behaviour that can lead to unexpected actions
  - (add other AI specific aspects)
- Do ISMS implementations still work for AI threats? (ISO 27001 or BSI Grundschutz)? ==> Answer this
- Does a risk-based approach (identifying risks and acting then) still hold? ==> Answer this
- New emerging ways to deal with these threats:
  - decrease response time by automation
  - decrease exposure, e.g. by removing unneeded roles / rights automatically
  - enhance monitoring to detect unwanted behavior (e.g. watch all kerberos activities)
  - adapt authorization to agentic environments (is SPIFFE a small or large part of it?)
  - monitor all agent activities
  - train agents to withstand pishing and other attacs
  - Introcude watchdog agents
  - plan pathes for an agent to gain increasing trust (e.g. by adding guardrails, ...)
- Call To Action

The two graphics should be

1. external threat actor attacking AI agent which then is a launchpad to the companies infrastructure
2. Layers of defensive measures against AI

### Post 3: Data Loss Prevention in an AI-first company

- DLP in most companies not completely solved
- AI brings new challenges to DLP
  - Data loss through prompts (e.g. when used for training)
  - Data loss through web fetch, agent interaction
  - Loss of confidentiality markers in RAG
  - AI as "context mixer"
  - Data loss through malicious AI exploits (see also previous article)
- A new separation is needed
  - What is in human responsibility
  - What can be achieved by labelling and automation
  - Where can AI help
- Reactions have to become much faster and focused to get good results
- What does that mean for:
  - laptops?
  - used SaaS offerings?
  - interaction with customer's and supplier's systems?

### Post 4: Is something big really happening
Critical analysis of Matt Shumers post "Something big is happening"
- What he says
- What is hype and what is reality
- What to do as a company and an indiviual



## Notes

<!-- TODO: Any other context that's helpful for Claude to know -->
