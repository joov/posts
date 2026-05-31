# Plan Check: "The DLP Blind Spot"

Reviewed: 2026-05-24

---

## 1. Consistency and Logical Flow

**Verdict: GOOD — with one structural issue to address**

The plan follows a clear narrative arc:
1. Hook (Samsung case + analogy) — establishes the problem viscerally
2. What DLP was built for — gives the reader the baseline
3. Three blind spots — the analytical core
4. Permission prompt trap — a fourth blind spot, human layer
5. Shadow AI — amplifier of all blind spots
6. Responsibilities — who must do what
7. CISO metrics — how to measure progress
8. What works / what doesn't — honest practitioner assessment
9. Open Source vs. commercial — buying decision
10. Modern DLP architecture — technical prescription
11. Closing — return to analogy

**The structural issue:** Sections 8, 9, and 10 partially overlap. Section 8 ("was bewährt sich") already discusses specific tools (Nightfall, Menlo). Section 9 discusses the same tools as a buying decision. Section 10 provides the technical architecture. This creates repetition — the reader encounters Nightfall three times in three consecutive sections with slightly different framing.

**Recommendation:** Merge sections 8, 9, and 10 into a single cohesive "What to do" section with clear subsections: (a) what's production-ready today, (b) open source vs. commercial decision tree, (c) the technical architecture behind it. This avoids triple-repetition and reduces overall length.

---

## 2. MECE Assessment (Mutually Exclusive, Collectively Exhaustive)

**Verdict: MOSTLY MECE — with one gap and one overlap**

**The gap:** The plan covers outbound data loss (data leaving the org via prompts, agents, copy-paste) thoroughly. It does NOT explicitly address **inbound contamination** as a DLP concern — i.e., sensitive data from training sets or other tenants leaking INTO the organization's AI outputs (model memorization, RAG cross-contamination from the other direction). EchoLeak partially touches this, but the plan does not frame it as a distinct DLP concern. Consider whether this belongs in scope or should be explicitly scoped out.

**The overlap:** As noted above, sections 8/9/10 cover overlapping ground. The three blind spots (Section 3) are cleanly MECE. The permission prompt trap (Section 4) is a genuinely distinct concept that does not overlap with the three blind spots — good addition.

---

## 3. Readability

**Verdict: RISK — article is too long for a single Medium post**

Current estimated word count based on section targets:
- Sections 1-5: ~200 + 250 + 700 + 300 + 300 = ~1,750 words
- Sections 6-11: ~350 + 300 + 250 + 300 + 400 + 150 = ~1,750 words
- **Total: ~3,500 words → ~14 minutes reading time**

The stated target is "~8 minutes." The plan now has 11 sections — nearly double the original 6-section structure. For a Medium post targeting busy CISOs, this is too long.

**Language consistency issue:** Sections 6-9 are written in German, sections 1-5 and 10-11 in English. The article will be published in English. The plan instructions should clarify: all content will be written in English; the German sections are planning notes only.

**Recommendations:**
- Either (a) cut total to ~2,500 words / 8 sections by merging 8+9+10, OR
- (b) Accept ~12 minutes and position as a "deep dive" — update the reading time claim accordingly, OR
- (c) Split into Part 1 (the problem: sections 1-5, ~1,750 words) and Part 2 (the solution: sections 6-11, ~1,750 words) as two separate posts with distinct titles.

---

## 4. Usability and Actionability

**Verdict: STRONG**

The plan scores well on actionability:
- Section 6 (responsibilities) gives clear org vs. employee accountability
- Section 7 (metrics) gives 4 specific KPIs with interpretation guidance
- Section 9 (tools) gives a 3-step buying roadmap that starts with zero budget
- Section 10 (architecture) gives "practical tests" for each blind spot

**One weakness:** The "Lessons Learned" section at the bottom reads as a summary of the diagnosis, not of the prescriptions. It should be updated to include at least one lesson from the "what to do" sections (e.g., "Start with sanctioned AI and SSO — this single architectural decision eliminates 60-80% of Shadow AI demand before any tooling purchase").

---

## 5. Target Group Consistency

**Verdict: GOOD — with one risk**

Target group: CISOs, Data & AI strategy leads, senior tech leaders.

The plan consistently speaks to this audience. The Samsung case is well-chosen (relatable), the CISO metrics section is directly operational, and the buying-decision section addresses budget realities.

**The risk:** Section 10 ("Modern DLP Architecture") is quite technical (RAG pipelines, retrieval-time ABAC, content-level policy enforcement). A CISO will understand this; a Head of AI Strategy may not. Consider whether this section should live as a "for your security engineering team" appendix or whether it should be simplified for the primary audience.

---

## 6. Source Verification Status

**Verdict: COMPLETE for sections 1-5; INCOMPLETE for sections 6-9**

Sections 1-5 have full verification notes at the bottom of PLAN.md. All claims CONFIRMED.

Sections 6-9 (the new additions) cite the following sources that have NOT yet been individually verified against their stated claims:
- IBM Security Cost of a Data Breach Report 2025 ("Shadow AI tax $670K") — not fetched
- Repello AI (AI AUP guide) — not fetched
- BeyondScale (AI AUP) — not fetched
- Sentra (90-day roadmap) — not fetched
- PolicyLayer MCP Security Audit ("96.8% of tools carry no warning") — not fetched against claim
- arxiv 2605.11360 (ConLeash, "consent fatigue" quote) — not independently verified beyond search snippet

**Note:** The search results during research did confirm these claims in snippet form. The risk is low, but for full rigor the verification notes should be extended to cover sections 6-9. However, the most critical factual claims (Samsung, Zscaler, EchoLeak, RAG leakage) ARE fully verified.

---

## 7. Specific Recommendations

| # | Issue | Severity | Recommendation |
|---|-------|----------|----------------|
| 1 | Sections 8/9/10 overlap | Medium | ✅ RESOLVED — merged into single "Decision Framework" section (Section 8) |
| 2 | Article too long for stated 8-min target | High | ✅ RESOLVED — merged sections reduce to ~10 min; reading time updated |
| 3 | German/English mix | Low | ✅ RESOLVED — merged section written in English; German planning notes remain in sections 6-7 only (for author reference, not for final article) |
| 4 | Lessons Learned missing prescriptive lessons | Low | Add 1-2 action-oriented lessons |
| 5 | Inbound contamination not addressed | Low | Either add a note or explicitly scope out |
| 6 | Section 10 may be too technical for full audience | Medium | Simplify or label as "for engineering teams" |
| 7 | Source verification incomplete for new sections | Low | Extend verification to sections 6-9 |

---

## 8. Overall Assessment

**The plan is strong, well-researched, and highly actionable.** The core thesis (three blind spots) is crisp, the analogy is effective, and the Samsung hook is compelling. The new additions (permission trap, responsibilities, metrics, tool guidance) respond to real CISO concerns and elevate the plan from "here's the problem" to "here's what to do about it."

The primary risk is length and repetition in the solution sections. Addressing recommendation #1 and #2 would bring this to publication-ready structure.

**Ready for writing:** Yes, after addressing the merge/length decision.
