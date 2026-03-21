# Knowledge: From Prompt Engineering to Context Engineering

## Source 1: Anthropic -- Effective Context Engineering for AI Agents

- **URL:** https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- **Published:** September 29, 2025
- **Authors:** Anthropic Applied AI team (Prithvi Rajasekaran, Ethan Dixon, Carly Ryan, Jeremy Hadfield)

### Summary

Anthropic's official engineering blog post that established context engineering as a recognized discipline. The article frames context engineering as the natural progression of prompt engineering -- moving from "finding the right words" to "what configuration of context is most likely to generate the model's desired behavior."

### Key Concepts

- **Context as finite resource:** LLMs suffer from "context rot" -- as token count increases, ability to recall information decreases. Context must be treated like a finite budget with diminishing marginal returns.
- **Attention scarcity:** Transformer architecture creates n-squared pairwise relationships for n tokens. Longer contexts stretch the model's attention thin.
- **Guiding principle:** Find the *smallest possible* set of high-signal tokens that maximize the likelihood of a desired outcome.

### Components of Effective Context

1. **System prompts:** Find the "right altitude" -- specific enough to guide behavior, flexible enough for heuristics. Avoid brittle hardcoded logic on one extreme and vague guidance on the other.
2. **Tools:** Should be self-contained, robust to error, clear in intended use. Avoid bloated tool sets with overlapping functionality.
3. **Examples:** Curate diverse, canonical examples rather than stuffing edge cases.
4. **Context retrieval:** Shift from pre-computed retrieval to "just in time" context strategies -- lightweight identifiers that dynamically load data at runtime.

### Techniques for Long-Horizon Tasks

- **Compaction:** Summarize conversation nearing context limit, reinitiate with compressed summary. Art lies in what to keep vs. discard.
- **Structured note-taking:** Agent writes notes persisted outside context window, pulls back when needed (like a to-do list or NOTES.md).
- **Sub-agent architectures:** Specialized sub-agents handle focused tasks with clean context windows. Each explores extensively but returns condensed summary (1,000-2,000 tokens).

### Notable Quotes

> "Context engineering represents a fundamental shift in how we build with LLMs."

> "As models become more capable, the challenge isn't just crafting the perfect prompt -- it's thoughtfully curating what information enters the model's limited attention budget at each step."

---

## Source 2: Rephrase -- 7 Steps to Context Engineering (2026)

- **URL:** https://rephrase-it.com/blog/7-steps-to-context-engineering-2026
- **Published:** March 12, 2026
- **Author:** Ilia Ilinskii

### Summary

A practical migration guide from prompt engineering to context engineering. Based on the academic paper "Context Engineering: From Prompts to Corporate Multi-Agent Architecture" (arXiv, March 2026) and Google ADK documentation. Provides a concrete 7-step migration path.

### Key Insight

Prompt engineering breaks in agent workflows because the failure mode shifts from **bad wording** to **bad state**. Once AI uses tools, memory, and multi-step planning, output quality depends on whether the right information is selected, structured, refreshed, and constrained -- not on the initial prompt.

### The 7-Step Migration Path

1. **Context audit:** List every input the model receives (system prompt, user message, retrieved docs, memory, tool outputs, policies, metadata). Question what doesn't measurably improve output.
2. **Separate stable from volatile context:** Business rules/tone/policies vs. fresh tool results. Stable = compact and persistent. Volatile = time-scoped and replaceable.
3. **Introduce memory tiers:** Working context, recent compressed history, durable facts -- should not compete equally for tokens.
4. **Compress before you append:** More context is not automatically better. Focus on decision relevance, not token bulk.
5. **Isolate sub-agents and tools:** If every component sees everything, errors spread.
6. **Add quality gates:** Verify output answered the question, stayed grounded, used authorized data paths.
7. **Instrument the whole thing:** Monitor cost, latency, tool calls, failure patterns.

### Prompt-Era vs. Context-Era Questions

| Prompt-era question | Context-era question |
|---|---|
| "How do we phrase this better?" | "What should the agent know right now?" |
| "Should we add role prompting?" | "Which context sources should be included or excluded?" |
| "Can we make the prompt longer?" | "Can we compress, isolate, and refresh state?" |
| "Why did the model ignore the instruction?" | "What conflicting context overrode or diluted it?" |

### Five Questions for Good Context

1. Is this context **relevant**?
2. Is it **sufficient**?
3. Is it **isolated**?
4. Is it **economical**?
5. Can we **trace where it came from** (provenance)?

### Notable Quote

> "Prompt engineering isn't dead. It got promoted. It's now one layer in a bigger stack."

### References from this article

- arXiv: Context Engineering: From Prompts to Corporate Multi-Agent Architecture (https://arxiv.org/abs/2603.09619)
- Google Cloud: Monitoring ADK agentic applications with Datadog LLM Observability
- arXiv: Authenticated Workflows: A Systems Approach to Protecting Agentic AI (https://arxiv.org/abs/2602.10465)

---

## Source 3: Wikipedia (de) -- Context Engineering

- **URL:** https://de.wikipedia.org/wiki/Context_Engineering
- **Published:** March 17, 2026 (last edit)

### Summary

Deutscher Wikipedia-Artikel, der Context Engineering als systematische Gestaltung der Informationsumgebung definiert, in der ein LLM arbeitet. Bietet guten historischen Ueberblick ueber Begriffsgeschichte, technische Grundlagen und das Konzept des "Knowledge Operating System".

### Begriffsgeschichte

- **Tobi Luetke** (Shopify CEO, Juni 2025): Praegte den Begriff. Definition: "Die Kunst, saemtlichen Kontext bereitzustellen, damit eine Aufgabe vom LLM plausibel loesbar wird."
- **Simon Willison** (Django-Mitschoepfer, Juni 2025): Erklaerte, der Begriff werde sich durchsetzen, da "Prompt Engineering" falsche Assoziationen wecke.
- **Philipp Schmid** (Google DeepMind): Formalisierte den Begriff als Disziplin. Zentrale These: "Die Mehrheit der Fehler in KI-Agentensystemen seien keine Modellfehler mehr, sondern Kontextfehler."
- **Andrej Karpathy** (ex-Tesla, OpenAI): Ordnete CE in "Software 3.0" ein -- natuerliche Sprache als Programmiersprache.

### Abgrenzung Prompt Engineering vs. Context Engineering

| Merkmal | Prompt Engineering | Context Engineering |
|---|---|---|
| Gegenstand | Einzelne Eingabe | Gesamte Informationsumgebung |
| Zeithorizont | Pro Interaktion | Session- und projektueberdauernd |
| Persistenz | Keine (fluechtig) | Versioniert, strukturiert |
| Komplexitaet | Textoptimierung | Systemarchitektur |
| Analogie | Einen Brief formulieren | Ein Buero einrichten |

### Geschichteter Kontext (Layered Context)

| Ebene | Inhalt | Lebensdauer | Beispiel |
|---|---|---|---|
| Global | Identitaet, Konventionen, Arbeitsstil | Dauerhaft | CLAUDE.md, Systemdateien |
| Projekt | Domaenenkontext, Projektstatus | Projektdauer | README.md, Statusdateien |
| Aufgabe | Spezifische Dateien, Werkzeuge | Sitzungsdauer | Einzelne Dokumente, Skills |

Parallelen zum Drei-Speicher-Modell der Kognitionspsychologie (Arbeitsgedaechtnis, episodisches Gedaechtnis, semantisches Gedaechtnis nach Tulving).

### Knowledge Operating System

Strukturiertes, versioniertes Wissens-Repository fuer Mensch UND LLM. Unterscheidet sich von klassischem PKM (Zettelkasten, GTD, Second Brain) durch:
1. **Duale Leserschaft** -- Inhalte fuer Mensch und Maschine optimiert
2. **Kontextarchitektur** -- Struktur folgt einer Ladestrategie: welcher Kontext wird wann in welcher Granularitaet dem LLM bereitgestellt

### Herausforderungen

- Kontextueberlastung -- mehr Kontext verbessert nicht linear
- Wartungsschulden -- veralteter Kontext fuehrt LLM in die Irre
- Automatisierungsparadox -- zeitsparendes System erfordert zunaechst Zeitaufwand
- Transfergrenzen -- persoenliche Systeme nicht ohne Weiteres uebertragbar

---

## Source 4: Tobi Luetke -- Original Tweet (Begrifspraegung)

- **URL:** https://x.com/tobi/status/1935533422589399127
- **Published:** June 18, 2025

### Summary

Der Tweet, der den Begriff "Context Engineering" populaer machte. Shopify CEO Tobi Luetke schlug vor, "Prompt Engineering" durch "Context Engineering" zu ersetzen.

### Zitat

> "I really like the term 'context engineering' over prompt engineering. It describes the core skill better: the art of providing all the context for the task to be plausibly solvable by the LLM."

---

## Source 5: Simon Willison -- Context Engineering

- **URL:** https://simonwillison.net/2025/jun/27/context-engineering/
- **Published:** June 27, 2025
- **Author:** Simon Willison (Django-Mitschoepfer, KI-Blogger)

### Summary

Willison erklaert, warum "Context Engineering" als Begriff Bestand haben wird: Die inferierte Definition von "Prompt Engineering" -- naemlich "pretentioeser Ausdruck fuer Tippen in einen Chatbot" -- sei zu weit vom eigentlichen Inhalt entfernt. "Context Engineering" transportiere die Komplexitaet besser.

### Key Insight

> "It turns out that inferred definitions are the ones that stick. I think the inferred definition of 'context engineering' is likely to be much closer to the intended meaning."

Willison verweist auf Karpathys Definition: Context Engineering sei "the delicate art and science of filling the context window with just the right information for the next step" -- einschliesslich task descriptions, few-shot examples, RAG, multimodal data, tools, state, history, und compaction.

---

## Source 6: Andrej Karpathy -- Software 3.0 (YC AI Startup School)

- **URL:** https://www.latent.space/p/s3
- **Published:** June 17, 2025
- **Source:** Latent Space Podcast / YC AI Startup School Talk

### Summary

Karpathy stellt sein Konzept "Software 3.0" vor: Natuerliche Sprache wird zur Programmiersprache fuer LLMs, und die Gestaltung des Kontexts ist die zentrale Ingenieursaufgabe. LLMs sind "the new computers" -- vergleichbar mit Utilities, Fabs, und Betriebssystemen.

### Key Concepts

- **Software 1.0/2.0/3.0:** Software 3.0 (natuerlichsprachliche Programmierung) frisst Software 1.0 (klassischer Code) und 2.0 (neuronale Netze). "A huge amount of software will be rewritten."
- **LLM Psychology:** LLMs sind "people spirits" -- stochastische Simulationen von Menschen mit emergenter Psychologie. Zwei Probleme: "Jagged Intelligence" (unvorhersehbare Staerken/Schwaechen) und "Anterograde Amnesia" (kein Langzeitgedaechtnis nach Training).
- **Autonomy Slider:** Produkte brauchen abstimmbare Autonomie-Level (z.B. Cursor: Tab -> cmd+K -> Agent Mode).
- **Generation-Verification Loop:** Je schneller der Mensch-AI-Loop, desto besser. "Demo is works.any(), product is works.all()."
- **Context Engineering:** "+1 for 'context engineering' over 'prompt engineering'. In every industrial-strength LLM app, context engineering is the delicate art and science of filling the context window with just the right information for the next step."

### Notable Quote

> "Context engineering is the delicate art and science of filling the context window with just the right information for the next step. Science because doing this right involves task descriptions, few shot examples, RAG, related data, tools, state and history, compacting... Art because of the guiding intuition around LLM psychology."

---

## Source 7: Petter Chr. Bjelland -- Three Layers of Context for Useful AI

- **URL:** https://medium.com/@pcbje/three-layers-of-context-for-useful-ai-f533276ca50a
- **Published:** 2025
- **Author:** Petter Chr. Bjelland

### Summary

Beschreibt unabhaengig ein Drei-Schichten-Modell fuer AI-Kontext, das im Wikipedia-Artikel als wiederkehrendes Muster identifiziert wird. Die drei Ebenen -- Global, Projekt, Aufgabe -- bilden eine Hierarchie mit abnehmender Allgemeinheit und zunehmender Spezifitaet.

### Relevanz

Bestaetigt, dass das Layered-Context-Pattern von mehreren Praktikern unabhaengig voneinander entdeckt wurde, was fuer seine Robustheit als Architekturmuster spricht.

---

## Source 8: Teresa Torres / Peter Yang -- Automate Your Life with Claude Code

- **URL:** https://creatoreconomy.so/p/automate-your-life-with-claude-code-teresa-torres
- **Published:** December 21, 2025
- **Authors:** Peter Yang (Interview), Teresa Torres (Autorin von "Continuous Discovery Habits")

### Summary

Teresa Torres beschreibt, wie sie ihr gesamtes Leben und Business mit zwei Claude Code Terminals und Obsidian betreibt. Sie implementiert ein dreischichtiges Kontextsystem.

### Das 3-Layer Context System

1. **Global (CLAUDE.md):** Universelle Praeferenzen wie "always plan before acting", Feedback-Stil
2. **Project-specific:** Projekt-Ordner (z.B. "tasks", "writing") mit eigener CLAUDE.md (z.B. bevorzugter Schreibstil)
3. **Reference Files:** Business-Details (Unternehmen, Produkte, Team), die Claude bei Bedarf einbezieht

### Key Takeaways

- "Claude Code is only as good as what it knows about you."
- Tipp zum Context Management: Kontext bewusst steuern, damit Claude nicht "dumber" wird
- Praxis-Beispiel eines Knowledge Operating System fuer Nicht-Entwickler

---

## Source 9: Serokell -- Design Patterns for Long-Term Memory in LLM-Powered Architectures

- **URL:** https://serokell.io/blog/design-patterns-for-long-term-memory-in-llm-powered-architectures
- **Published:** December 9, 2025
- **Author:** Ivan Smetannikov (Serokell)

### Summary

Technischer Vergleich von vier Ansaetzen fuer Langzeit-Gedaechtnis in LLM-Architekturen. Zeigt die architektonische Tiefe hinter Context Engineering.

### Vier Paradigmen

1. **MemGPT (OS-Paradigma):** Behandelt LLM-Context wie RAM, mit Paging-Mechanismus zu externem Speicher. Elegant, aber Single-Agent-Overhead.
2. **OpenAI Memory:** Globales, nutzer-zentrisches Gedaechtnis ueber alle Chats. "Magische" Personalisierung, aber Risiko von Context Leakage.
3. **Claude Memory:** Strikte Projekt-Isolation und User Control. Ideal fuer regulierte Umgebungen, aber hoher manueller Aufwand.
4. **AI Toolkits (LangChain, Autogen):** Maximale Flexibilitaet durch modulare Bausteine, aber hohe Build-Komplexitaet.

### Parallelen zur Kognitionspsychologie

Strukturelle Parallelen zum Drei-Speicher-Modell (Tulving):
- **Arbeitsgedaechtnis** = Context Window (Primary Context / RAM)
- **Episodisches Gedaechtnis** = Recall Storage (Gespraechshistorie)
- **Semantisches Gedaechtnis** = Archival Storage (abstrahiertes Wissen)

### Trends

- Von direktem Context Sharing zu RAG zu autonomer Memory-Orchestrierung
- Von unstrukturierten Snippets zu Knowledge Graphs
- Von Single-Agent zu Multi-Agent Pipelines

---

## Source 10: Carl Vellotti -- Carl's Product OS

- **URL:** https://github.com/carlvellotti/carls-product-os
- **Author:** Carl Vellotti (Autor von "Claude Code for PMs")

### Summary

Ein oeffentliches GitHub-Repository, das ein "Personal Operating System" fuer Claude Code zeigt. Demonstriert, wie ein Product Manager seinen gesamten Arbeitsplatz als Kontextarchitektur organisiert -- ein konkretes, funktionierendes Beispiel fuer Context Engineering in der Praxis.

### Struktur

| Ordner/Datei | Zweck |
|---|---|
| `CLAUDE.md` | Einstiegspunkt. Claude liest dies automatisch bei jedem Gespraech. |
| `GOALS.md` | Identitaet, Verantwortlichkeiten, aktuelle Ziele |
| `Tasks/` | Backlog -> Active -> Archive |
| `Projects/` | Einzelprojekte mit eigenem Kontext und Research |
| `Workflows/` | Wiederholbare Prozesse |
| `Knowledge/` | Persistentes Referenzmaterial ueber Projekte hinweg |
| `Templates/` | Dokumentvorlagen fuer konsistente Outputs |
| `.claude/skills/` | Slash-Commands fuer schnellen Zugriff |
| `Tools/` | Scripts und Automatisierungen |

### Key Concepts

- **Projects vs. Workflows:** Projects haben ein Ende und werden archiviert. Workflows sind wiederholbar.
- **Templates vs. Workflows:** Templates definieren die Struktur des Outputs. Workflows definieren den Prozess.
- **Knowledge vs. Project Research:** Knowledge ist persistent und projektuebergreifend. Project Research ist scope-spezifisch und wird mit dem Projekt archiviert.

### Relevanz

Lebendes Beispiel eines Knowledge Operating Systems. Zeigt, dass Context Engineering nicht nur Theorie ist, sondern bereits von Praktikern als Arbeitsorganisation umgesetzt wird. Die Struktur spiegelt das Layered-Context-Muster wider: Global (CLAUDE.md, GOALS.md) -> Projekt (Projects/) -> Aufgabe (Tasks/, Workflows/).
