# From Prompt Engineering to Context Engineering

*Why the smartest AI teams stopped optimizing prompts — and what they're building instead.*

---

## The Prompt Illusion

"Prompt Engineer" was the hottest job title of 2024. Bootcamps charged thousands to teach people how to write better instructions for AI. LinkedIn was flooded with "10x your productivity with these prompt templates."

Today, the role is quietly disappearing from job boards.

Not because AI got worse. Because the best teams realized they were solving the wrong problem.

Philipp Schmid, Senior AI Developer Relations at Google DeepMind, put it bluntly: **"Most agent failures are not model failures. They are context failures."** The model isn't broken. The information environment around it is.

---

## What Changed

To understand the shift, look at how we use AI systems today versus two years ago.

In 2023, a prompt *was* the product. You typed a question, you got an answer. The quality of that answer depended almost entirely on how well you phrased your request. Prompt engineering was the right skill for that world.

In 2026, the picture looks different. AI agents work in loops. They use tools, query databases, remember previous interactions, and make decisions across dozens of steps — often without human intervention between them. An agent scheduling a meeting might check your calendar, look up the sender's history, assess their priority, pick a time slot, and draft a response.

In that world, the initial prompt is just one input among many. If the agent has stale calendar data at step 5, no amount of prompt optimization will fix the output at step 12.

The question has shifted:

| Prompt Era | Context Era |
|---|---|
| "How do we phrase this better?" | "What should the agent know right now?" |
| "Should we add role prompting?" | "Which context sources should be included or excluded?" |
| "Can we make the prompt longer?" | "Can we compress, isolate, and refresh state?" |
| "Why did the model ignore the instruction?" | "What conflicting context overrode or diluted it?" |

[Graph: Prompt-Era vs. Context-Era]

---

## What Decision-Makers Need to Know

In June 2025, Shopify CEO Tobi Lütke coined the term that captured this shift. He called it **context engineering** — "the art of providing all the context for the task to be plausibly solvable by the LLM."

Within days, Andrej Karpathy (former AI lead at Tesla, co-founder of OpenAI) amplified it, calling context engineering "the delicate art and science of filling the context window with just the right information for the next step." Simon Willison, co-creator of the Django web framework, predicted the term would stick because the inferred meaning of "prompt engineering" had drifted too far from reality. People thought it meant "typing cleverly into a chatbot."

Schmid formalized the definition: **Context engineering is the discipline of designing dynamic systems that deliver the right information, with the right tools, in the right format, at the right time.**

Two things matter for AI-leaders here.

**First: context is a finite resource.** It's tempting to think that more context means better results. It doesn't. Anthropic's engineering team describes an **"attention budget"** — the model's ability to recall and use information degrades as the context window fills up. There are diminishing marginal returns. The goal is not maximum context. It's the *smallest possible set of high-signal information* that makes the task solvable.

**Second: this is now engineering, not wordsmithing.** Karpathy calls it both science and art — science because it involves measurable components like task descriptions, few-shot examples, RAG pipelines, tool definitions, and memory management. Art because there's still intuition involved in understanding what Karpathy calls "LLM psychology."

Here's the analogy that captures it best:

**Prompting is like giving a new employee an assignment.** Context engineering is like setting up their entire workspace — with the right tools, documents, access rights, and contacts they need to complete that assignment independently. The assignment (prompt) is just one part. The environment (context) determines whether they succeed.

---

## Three Strategic Implications

### Context Is the New Competitive Layer

If two companies use the same model but one has a better context architecture, that company will get better results. The model is a commodity. The context is the differentiator.

The architecture that practitioners keep converging on is **layered context** — three tiers of information with decreasing scope and increasing specificity:

[Graph: Layered Context Architecture]

| Layer | Contains | Lifespan | Example |
|---|---|---|---|
| **Global** | Identity, standards, policies | Permanent | Company rules, compliance, tone |
| **Project** | Domain knowledge, goals, status | Project duration | Research, stakeholder decisions |
| **Task** | Current data, active tools | Per session | Documents, API responses, chat history |

This isn't theoretical. Multiple practitioners have independently arrived at this pattern. Teresa Torres, author of *Continuous Discovery Habits*, runs her entire business with two Claude Code terminals and a note-taking app, organized into exactly these three layers. Carl Vellotti published his "Product OS" — a complete workspace structure for product managers that mirrors this architecture with folders for global context, projects, workflows, and persistent knowledge.

The pattern also has deep roots. Researchers have noted structural parallels to the three-store model in cognitive psychology: working memory, episodic memory, and semantic memory. We're essentially building the same architecture for machines that evolution built for human cognition.

### Your AI Investment Must Shift

Most organizations are still spending their AI budget on model access, prompt template libraries, and fine-tuning experiments. That's like investing in better ink while ignoring the printing press.

The investment needs to move toward:

- **Context architecture** — How is information structured, versioned, and loaded into the model?
- **Persistent knowledge** — What does the agent remember across sessions? What does it forget? How is prior context preserved and recalled?
- **Tool integration** — Which external systems can the agent access, and how is their output formatted?
- **Instrumentation** — Can you see what the model actually received when it made a decision?

Schmid illustrated this with a simple example: the same email — "Hey, just checking if you're around for a quick sync tomorrow" — produces a generic, useless response with poor context, but a specific, actionable response when the model has access to your calendar, email history, contact list, and scheduling tools. Same model. Same prompt. Radically different output. The difference is entirely in the context.

### Prompt Engineering Isn't Dead — It Got Promoted

Prompt engineering still matters. Crafting clear instructions, finding the right level of specificity, structuring system prompts — all of this remains valuable work.

But it's now **one layer in a larger stack**. Optimizing only that layer is like redecorating the wallpaper while ignoring the structural integrity of the building.

If you're familiar with the **MECE principle** from strategy consulting — mutually exclusive, collectively exhaustive — that's essentially what good context architecture demands: no overlaps, no gaps. For every AI initiative, decision-makers should be asking five questions:

1. Is the context **relevant** to the task at hand?
2. Is it **sufficient** — does the model have what it needs?
3. Is it **isolated** — are different workstreams properly separated?
4. Is it **economical** — are we staying within the attention budget?
5. Is it **traceable** — can we reconstruct what the model saw when something went wrong?

If your team can't answer these questions, you're not doing context engineering. You're guessing.

---

## What to Do Tomorrow

You don't need to rebuild your AI stack overnight. But three steps will immediately sharpen your results:

**Run a context audit.** Ask your AI team: what information does the model actually see when it makes a decision? Most teams cannot answer this question. They know what the prompt says, but they don't know what the full context window contains — the retrieved documents, the tool outputs, the conversation history, the system instructions. Map it. You'll find surprises.

**Separate stable from volatile.** Business rules, tone guidelines, and compliance policies should not live in the same bucket as fresh API responses and real-time data. Stable context should be compact and persistent. Volatile context should be time-scoped and replaceable. Mixing them is how you get contradictory outputs.

**Measure instead of guessing.** If you're not monitoring cost per query, response latency, tool call patterns, and failure modes, you're flying blind. Context engineering without instrumentation is just hope with extra steps.

---

## The Bottom Line

The question is no longer "How do I write the perfect prompt?" The question is: **"What information environment does my AI system need to work reliably?"**

Those who understand this will stop polishing prompts and start building context architecture. Those who don't will keep wondering why their AI demos work beautifully but their production systems fail quietly.

The prompt got the AI revolution started. The context will determine who wins it.

---

## References

- Anthropic Applied AI Team, "Effective Context Engineering for AI Agents," anthropic.com, September 2025
- Philipp Schmid, "The New Skill in AI is Not Prompting, It's Context Engineering," philschmid.de, June 2025
- Tobi Lütke, post on X, June 18, 2025
- Simon Willison, "Context Engineering," simonwillison.net, June 2025
- Andrej Karpathy, "Software 3.0," YC AI Startup School / Latent Space, June 2025
- Ilia Ilinskii, "7 Steps to Context Engineering," rephrase-it.com, March 2026
- Petter Chr. Bjelland, "Three Layers of Context for Useful AI," Medium, 2025
- Peter Yang / Teresa Torres, "Automate Your Life with Claude Code," CreatorEconomy, December 2025
- Ivan Smetannikov, "Design Patterns for Long-Term Memory in LLM-Powered Architectures," serokell.io, December 2025
- Carl Vellotti, "Carl's Product OS," github.com/carlvellotti/carls-product-os
- "Context Engineering," Wikipedia (de), March 2026
