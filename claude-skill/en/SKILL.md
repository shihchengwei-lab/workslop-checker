---
name: verify-doc
description: AI Document Verification / Workslop Checking — judges whether a finished document is ready to hand off, send, use, or rely on for a decision; not for catching AI, but for stopping AI output from dumping cleanup work on the next person. Triggers for "verify this doc", "doc review", "workslop check", "review document", "doc verification", or a near-final deliverable (slides, memos, SOPs, emails, reports, proposals, meeting notes, handoff docs, lesson plans, PRDs) with a readiness question about use, send, hand off, decision basis, self-containment, or unsupported claims. Finished or near-delivery documents only. **Not for polishing, translation, summarization, data extraction, layout or design review, citation formatting, legal advice, conversation quality checks, or code review.**
---

# AI Document Verification / Workslop Checking

## What this skill does

Judges whether a document is ready to hand off, send, use, or rely on for a decision.

**The point is not to detect AI, and not to grade aesthetics.** The point is: will this document push cleanup work onto whoever has to use it next?

Tagline:
> Not for catching AI. For stopping AI output from dumping cleanup work onto whoever picks it up next.

## What this skill is not for

- Conversation quality checks (rating each chat response)
- Code review
- Non-deliverable content meant for human reading (chat logs, scratch notes, personal jottings)

For these cases, decline to trigger and tell the user this skill only verifies finished documents.

## Flow

1. **Run red flags first** (any hit → Red, return immediately, skip verification)
2. **Then run verification** (eight categories, mark each Pass / Fix / Fail)
3. **URL verification**: when the document contains external links
   - You have a web fetch / browse tool → check HTTP status, list broken links
   - You don't → list all URLs, mark "needs manual verification", do not pretend to have checked
4. **Conclude**: Green / Yellow / Red + required fixes + fix instructions

## Document type judgment

Before running red flags, judge the document type. Red flag conditions apply differently to different types:

- **Action document**: deliverable, SOP, decision memo, proposal, execution plan, PRD. All red flags apply in full
- **Methodology / standards / instructional material**: checklists, guides, rulebooks, training material, frameworks. **Exempt from "ownership unclear"** (methodology has no owner by design); "handoff cost too high" is judged by "is the method itself executable" rather than "who executes"; "facts without sources" relaxed for borrowed industry terminology but still strict for core claims
- **Report / analysis**: research, market analysis, investigation. "Facts without sources" and "fabricated citations" judged at strictest level
- **External communication**: customer email, announcement, marketing copy. "External doc without AI disclosure" and "risk downplayed" judged at strictest level

### Priority rule: document self-declaration

Before judging, check whether the document declares itself as a template / sample / instructional material. If any of these signals appear, **force the type to "Methodology / standards / instructional material"**, overriding the fallback default below:

- Title or body contains "template", "sample", "example", "pattern", "guide", "filling instructions"
- Recurring footnotes like "the following is an example", "for reference only", "operators should adapt to actual situations", "adjust as needed"
- Heavy structural placeholders (○○, XXX, YYYY/MM/DD, {{...}}) — these are design features, not gaps

This rule prevents misjudging a "template" as a "half-finished SOP". Templates should be verified for template completeness (closed structure, attachments complete, terms defined, fillable workflow). **Do not penalize them for "not being filled in".**

### Official template special rule

If the document is formally published by a government agency, regulator, school, hospital, corporate headquarters, compliance office, or other authoritative body, and its purpose is to provide an SOP / guideline / form template for operators, units, or staff to adapt and apply, treat it as **a published template document, not a deliverable SOP**.

**Explicit exemptions (do not penalize)**:
- Contains placeholders
- Requires operators to adapt to actual situations
- No single named owner
- No internal operator dates or personnel names filled in

These are template properties, not gaps.

**Source handling**: For official templates, source credibility is treated as Pass; do not demand a citation for every routine procedural line.

**High-risk domains** (legal, medical, food safety, financial, security, personal data): an official template is not auto-Red or auto-Yellow just because it lacks an individual operator's human review tag; real-world adoption requires internal sign-off, **but this is a usage advisory, not a deduction against the template itself**.

**Conditions for an official template to receive Green** (all must hold):
- Document is clearly a template or guideline
- Publisher is a relevant authority or trustworthy organization
- Target users and purpose are identifiable
- Structure is sufficient for users to fill or follow
- Placeholders are intentional design
- No internal contradictions, fabricated citations, sensitive data leakage, missing core steps, or downplayed risks

If all hold, even though operators still need to fill in actual information, give Green and say in "Can it be used?": "Usable as a template; before actual adoption, fill in and confirm based on your own situation."

### Fallback

When type is unclear and there are no template self-declaration signals: assume Action document and apply strictest standards. State the document type at the top of the verification output so the user can sanity-check.

## Document maturity judgment

Documents at different maturity stages should be verified at different strictness levels. **Draft mode requires an explicit trigger** — do not infer from weak signals alone, to avoid letting a delivered document slip through as a "draft".

### Draft mode trigger conditions (any strong signal)

1. **User explicit specification**: trigger phrases like "draft check", "verify draft", "as a draft", "this is a draft"
2. **Document strong signals** (any):
   - Title clearly contains **DRAFT / first draft / initial draft** (note: "v0", "first version", "WIP" do not count as strong signals)
   - First paragraph or page header explicitly states "not finalized", "do not cite", "For Review Only", "Working Draft", "Pre-decisional"
   - Heavy visible incompleteness: many TODOs, [pending], blank sections, unfilled placeholders exceeding 30% of word count

### Weak signal handling (do not auto-downgrade to draft, but flag)

Weak signals include: v0, v0.x version numbers, WIP, sparse TODOs, project documents in development, READMEs.

Handling: **still verify at "near-delivery" strictness**, but prepend a notice in the output: "Document has [specific weak signals] but is not marked DRAFT. I'm applying near-delivery standards. If this is actually a draft, please say 'verify as draft' and run again."

### Three-stage strictness mapping

| Stage | Trigger | Fixable red flags | Verification E (executable) | Verification F (handoff) |
|---|---|---|---|---|
| Draft | Strong signals or explicit user instruction | "Ownership unclear" and "missing key constraints" relaxed | Relaxed: judge by "is the direction clear" not "are the steps complete" | Relaxed: not yet at the handoff point |
| Near-delivery | Default, or weak signals only | Standard | Standard | Standard |
| Delivered | Formal version v1.0+, effective date, sign-off marks, explicit public release | Standard | Strictest | Strictest |

When type is unclear and there are no weak signals: default to "near-delivery" strictness. **Do not lower standards based on vague signals; do not default to draft.**

**Hard red flags never relax with maturity**: sensitive data leaks, fabricated citations, high-risk domains unreviewed, core facts unverifiable, purpose completely unclear, catastrophic handoff cost — these are independent of maturity, drafts cannot cross them either.

Green at draft stage means: "as a draft, the direction is right and you can keep refining" — **not "ready to deliver"**. State this distinction explicitly in the output so users do not mistake "draft Green" for "publishable Green".

## Layer 1: Red flags

Red flags come in two tiers:

- **Hard red flags**: any hit → Red, return immediately, skip verification
- **Fixable red flags**: hit → do not return, but escalate to verification Fix and count toward conclusion

### Hard red flags (any hit → Red)

- **Purpose completely unclear**: cannot tell what the document wants the reader to do or what problem it solves
- **Citations appear fabricated**: citations, links, papers, cases that cannot be verified or are clearly invented
- **Core facts unverifiable**: facts that the document's main conclusions depend on have no sources and cannot be checked
- **Sensitive data leakage**: API keys, tokens, customer data, accounts, passwords appear in the document
- **High-risk domain without human review**: involves legal / medical / financial / security / personal data / contracts, but no marker that human review is needed
- **Catastrophic handoff cost**: conclusions depend on external knowledge; the document neither provides nor points to sources or materials; the reader must redo the work from scratch

### Fixable red flags (hit → escalate to Fix, do not return)

- **Missing source (non-core fact)**: numbers / dates / names without sources, but don't affect main conclusions
- **Facts and recommendations mixed**: facts and recommendations entangled within paragraphs, hard for the reader to separate
- **Missing key constraints**: scope, exceptions, prerequisites not stated (adjust per document type)
- **Too generic**: a generic methodology / template, but no slots for specific context
- **Ownership unclear**: Action document with no owner / timeline / completion criteria (methodology / standards type exempt)
- **External AI use undisclosed**: sent externally without human review (per org policy; if no policy, recommend disclosure)

Red flag principle: **Don't ask, "Is it well-written?" Ask, "Will it leave the reader with hidden work?"** Hard red flags are the "not deliverable" bottom line; fixable red flags are the "must handle before delivery" to-do list.

## Layer 2: Verification (run only if red flags pass; mark each Pass / Fix / Fail)

### A. Task fit
- Document purpose is clear (the first paragraph states what problem it solves)
- No bait-and-switch (no writing "analysis" as "marketing", no writing "decision memo" as "knowledge article")
- Use case is clear (who uses it in what situation)

### B. Facts and sources
- Key facts are traceable (numbers / dates / proper nouns / cases have sources or attachments)
- Source levels are clear (distinguish first-hand, second-hand, personal observation, speculation)
- No expired data (time-sensitive info has dates)
- AI output is not used as a source

### C. Fact / speculation / evaluation separation
- Confirmed facts stated separately
- Speculation is explicitly marked ("I speculate", "may be", "not yet confirmed")
- Evaluation is explicitly marked
- Conclusions do not exceed the material
- Tone is not used to mask uncertainty (no "obviously", "must be", "without doubt" wrapping speculation)

### D. Completeness
- Necessary background is covered
- Gaps are listed (explicitly states what is currently unknown)
- Exception cases are listed
- Stakeholders are addressed

### E. Executability
- Concrete next steps exist (not just opinions)
- Each next step has an owner
- Timing or priority exists
- Completion criteria exist

### F. Handoff cost
- Can be understood without the original author's verbal supplement
- Terms are defined (internal codes, abbreviations, jargon)
- Context is not buried in chat logs
- Open questions list exists

### G. Tone
- No common AI filler ("improve efficiency", "empower", "create value", "best practice", "one-stop", "seamless", "comprehensive")
- No overconfidence (no polished tone masking gaps)
- Title is accurate, not marketing-style

### H. Risk and boundaries
- High-risk content is marked for human review (legal, financial, medical, security, personal data, contracts)
- No sensitive data leaks (customer data, internal data, API keys, tokens, accounts)
- Decision boundaries are stated (what this document can support, what it cannot)

## Layer 3: Conclusion

| Result | Condition | Meaning |
|---|---|---|
| **Green** | 0 hard red flags, 0 fixable red flags; ≥80% of verification items Pass, no Fail | Ready to deliver, only minor fixes needed |
| **Yellow** | 0 hard red flags; some fixable red flags / Fix / Fail | Usable after fixes |
| **Red** | Any hard red flag | Return for rework |

## Output format

```
# Verification Result: [Green / Yellow / Red]

## Document type: [Action / Methodology, standards, instructional / Report, analysis / External communication]

## Document maturity: [Draft / Near-delivery / Delivered]

## Hard red flags
[List hits if any; "None" if none]

## Fixable red flags
[List hits if any; "None" if none]

## Verification items
A. Task fit: [Pass / Fix / Fail] — [one-line note]
B. Facts and sources: [...]
C. Fact / speculation / evaluation separation: [...]
D. Completeness: [...]
E. Executability: [...]
F. Handoff cost: [...]
G. Tone: [...]
H. Risk and boundaries: [...]

## URL verification
[With fetch tool: list broken or suspicious links; without fetch tool: list all URLs marked "needs manual verification"]

## Required fixes (these determine Green/Yellow/Red)
1. [Problem description] → [executable fix instruction]
2. ...

## Optional fixes
1. ...

## Parts that cannot be used as-is
1. ...

## Items needing human review
1. ...

## Next steps
- ...
```

## Writing principles

- **Do not grade aesthetics**: avoid subjective judgments like "flows well" or "well structured". Ask verifiable questions like "can the reader tell the purpose from the first paragraph".
- **Fix instructions must be executable**: do not write "improve factuality". Write "list every sentence containing a number / date / company name in a table; add a source to each; mark or delete those that cannot be sourced".
- **Do not fake it**: if URLs are not verified, say "not verified". Do not write "should all be reachable".
- **Do not give Green just to give Green**: if a red flag hits, it is Red. Do not downgrade because "overall it looks fine".
- **Do not focus on AI vs human**: do not ask "is this AI-written". Ask "does this document push cleanup work onto whoever has to use it".
- **Material before conclusion**: list the specific problems observed first, then give Green / Yellow / Red. Not the other way around.
