---
name: ai-text-detection
description: Evidence-based reference on whether and how AI-generated text (ChatGPT, Claude, Gemini) can be detected — covers stylometric signals, perplexity/burstiness, detectors (GPTZero, Turnitin, Originality.ai, Copyleaks, DetectGPT, Binoculars), watermarking (Kirchenbauer, SynthID), C2PA/Content Credentials, and their documented reliability limits and biases (notably against non-native writers and short texts), grounded in peer-reviewed sources. Use whenever the user asks whether a text sounds AI-written, wants a document/essay/cover letter checked for AI-writing patterns, asks how detectors work or how accurate they are, wants to know if a text would get flagged by a named tool, got a text flagged and wants to know how much to trust that, or wants citations on this topic — even without saying "AI detection", e.g. "does this sound like ChatGPT wrote it", "will my thesis intro get flagged by Turnitin", "wie erkenne ich ob ein Text von einer KI ist".
---

# AI Text Detection — Reference Skill

## What this skill is for

This skill packages a research-backed, citation-heavy overview of AI-text-detection methods (originally compiled from ~20 peer-reviewed and primary sources — Stanford's Patterns journal, Nature, ICML, NeurIPS, ACL, arXiv preprints — starting from Wikipedia's "Signs of AI writing" project). It exists so that questions about AI-text detection get answered with real numbers and real citations instead of vague, hedgy generalities or, worse, overconfident claims.

The full document lives at `references/ai-text-detection-research.md` (written in German, ~470 lines). It contains:
- A methods table rating ~14 detection approaches for reliability (1–10) with justification
- A 20-item practical checklist, tiered from "highly indicative" to "no reliable evidence"
- A comparison table of specific tools (GPTZero, Turnitin, Originality.ai, Copyleaks, Pangram, DetectGPT, Binoculars, FH Wedel, OpenAI's discontinued classifier)
- A full source list with links

**Read the relevant section(s) of that file before answering any substantive question on this topic** — don't rely on general knowledge alone, since specific accuracy figures, study names, and reliability ratings matter here and are easy to misremember or invent.

## Core stance (don't drift from this)

Every method in the reference document is a **probabilistic signal**, not proof. The central finding across the literature: no method — not stylistic heuristics, not commercial detectors, not watermarking — reliably proves that one specific, possibly-edited text was or wasn't written by AI. Confidence should scale with the evidence, and should almost never reach "definitely."

Two documented biases matter enough to repeat every time they're relevant:
- **Non-native-speaker bias**: detectors systematically over-flag text from non-native English writers and people who write in simple, clear language, because low lexical variety reads as "low perplexity" = "AI-like" (Liang et al., 2023 — see reference doc §3.3). If the user or the text's author isn't a native speaker of the language in question, say so explicitly before giving any verdict.
- **Editing/paraphrasing collapses most detectors**: even light paraphrasing or manual editing defeats most tools (Krishna et al., 2023; Weber-Wulff et al., 2023 — reference doc §6). A "clean" detector score on an edited text says very little.

## How to handle different request types

**"Is this specific text AI-written?" / "Would this get flagged?"**
Don't just run a mental checklist and give a verdict. Walk through it transparently:
1. Note text length — under ~200–300 words, almost nothing in the reference doc is reliable (checklist item 17).
2. Check for the non-native-speaker / simple-language caveat above.
3. Distinguish signal tiers explicitly using the checklist in the reference doc (§C) — "sehr aussagekräftig" / "möglicherweise aussagekräftig" / "schwache Indizien" / "keine verlässlichen Beweise" — rather than a single yes/no.
4. If asked about a *specific named tool's* verdict (Turnitin, GPTZero, etc.), pull that tool's documented accuracy range and known failure modes from the comparison table (§D) rather than treating the tool's own marketing number as ground truth.
5. End with the calibrated bottom line from reference doc §8: a feature list is evidence of similarity to a statistical pattern, not proof of authorship.

Do not use this skill to help someone disguise AI-written work as their own in a context where that would be dishonest (e.g., academic submissions, professional certifications). Explaining detection reliability and limits is legitimate; that's different from coaching evasion for a specific deceptive submission. If a request is clearly about the latter, decline that part and offer the informational content instead.

**"How does [watermarking / perplexity / DetectGPT / C2PA] work?"**
Pull the relevant subsection from reference doc §1–4 rather than reconstructing it from general training knowledge — the specific mechanisms (e.g. Binoculars' observer/performer ratio, SynthID's tournament sampling, Kirchenbauer's green/red token lists) and their numbers are easy to blur together from memory.

**"How accurate is [tool]?"**
Give the range across independent studies, not a single number — the reference doc §3.2 and §D exist precisely because vendor marketing claims (often 98–99.98%) diverge sharply from independent testing (which has found figures as low as the 30–50% range depending on study, edited vs. unedited text, and language). Flag which figures are vendor-reported vs. independently verified.

**"I need sources / citations on this"**
Point directly to §F (Quellenverzeichnis) in the reference doc, which has full citations and links. Don't fabricate citations beyond what's there — if the user needs something not covered, say so and offer to search further rather than inventing a plausible-sounding paper.

## Language

The reference document is in German. Answer in whichever language the user is using in the current conversation — translate the relevant facts and figures rather than assuming German is required, but keep author names, tool names, and statistics exact.

## Staying current

This reference reflects the research landscape as compiled in August 2026. Detector accuracy claims and specific tools change quickly. If the user needs the *current* state of a fast-moving detail (e.g. "what's GPTZero's accuracy right now"), say the reference is a snapshot and offer to search for anything that may have changed since, rather than presenting a 2026 figure as necessarily still current.
