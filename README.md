# verify-doc / Workslop Checker

[繁體中文](README.zh-TW.md) | English

> A tool for checking whether an AI-written document is ready to hand off, ship, publish, or use for decisions.
> Not about detecting AI. About stopping AI output from dumping cleanup work onto whoever has to use it next.

---

## Try it directly (recommended)

No setup needed. Click the link:

**👉 https://chatgpt.com/g/g-6a0c5412dca48191be1632fac7523af4-verify-doc-workslop**

The GPT is bilingual and automatically matches the language of your conversation.

---

## What this solves

**Workslop** is a term coined by BetterUp Labs and Stanford Social Media Lab in their [September 2025 Harvard Business Review article](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity), defined as: "AI-generated work content that masquerades as good work but lacks the substance to meaningfully advance a given task."

Their research found:
- **40%** of employees received workslop in the past month
- **~2 hours** average to correct each piece
- **$186/employee/month** ($9M/year for a 10,000-person org)

This tool does not ask **"is this AI-written?"** — that question is hard to answer and often does not solve the real problem.

It asks **"will this document push cleanup work onto whoever has to use it?"** Can you hand it off, ship it, decide on it — or do you need to redo half the work first?

---

## How to use

### Most users

Click the GPT link above. Paste your document into the conversation. Ask whether it is ready to use.

### Claude Code users (developers)

Copy `claude-skill/zh-TW/SKILL.md` into your `~/.claude/skills/verify-doc/SKILL.md`. Restart Claude Code. Trigger with "verify this doc", "doc review", or "workslop check".

(An English SKILL.md is on the TODO list. The Chinese version still works in English conversations — the model handles cross-language rules — but it won't match English trigger phrases until the English version is added.)

### Want to fork or customize?

See the README files in these folders:
- [Claude skill (zh-TW)](claude-skill/zh-TW/SKILL.md) — full ruleset
- [ChatGPT Custom GPT setup (zh-TW)](chatgpt-custom-gpt/zh-TW/README.md) — Description / Conversation starters / Instructions, ready to paste into Custom GPT Editor

---

## Good for

- AI-written reports, SOPs, lesson plans, proposals, slide text, announcements, meeting notes, handoff documents
- Anyone deciding whether a document can be handed off, shipped, or used as a basis for decisions

## Not for

- Conversation quality checks (rating each chat response)
- Code review
- Chat logs, scratch notes, rough drafts, or personal notes not meant to be delivered

---

## Structure

```
workslop-checker/
├── README.md                       # This file (English)
├── README.zh-TW.md                 # Traditional Chinese
├── LICENSE                         # CC-BY-4.0
├── claude-skill/
│   ├── en/SKILL.md                 # TODO
│   └── zh-TW/SKILL.md              # Full Claude Code skill (ruleset)
├── chatgpt-custom-gpt/
│   ├── en/README.md                # TODO
│   └── zh-TW/README.md             # Custom GPT setup with source (Description/Starters/Instructions)
└── docs/
    ├── design-rationale.md         # Why this design
    └── workslop-background.md      # Workslop origin & context
```

---

## Feedback

Open a GitHub issue if the tool gets something wrong:

- **False positive**: a good document was flagged Red or Yellow
- **False negative**: workslop was rated Green

Please include:
- Document characteristics (type, scale, source — no need to paste the whole thing)
- The tool's verdict
- What you expected

---

## License

[CC-BY-4.0](LICENSE). Commercial use allowed. Attribution required.

---

## Credits

- **Workslop concept**: BetterUp Labs + Stanford Social Media Lab ([original HBR article, Sep 2025](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity))
- **Design**: [@shihchengwei-lab](https://github.com/shihchengwei-lab) in collaboration with Claude / Codex
