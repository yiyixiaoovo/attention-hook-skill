# attention-hook-skill

A skill pack for **diagnosing and rewriting openers, titles and covers** of articles and short videos.
Install it into any agent that reads `SKILL.md` (Claude Code, Codex, DeepSeek Harness, …) and it routes
“fix my opening”, “why is this hook flat”, “is this title clickbait?” to the right capability card.

**18 capability cards**: 9 evidence-backed (papers / meta-analyses) + 9 practitioner cards. Every card
has an evidence-boundary section; practitioner cards state **0 controlled experiments** and never
promise lift.

## Install

**Copy the skill**

```bash
git clone https://github.com/yiyixiaoovo/attention-hook-skill.git
cp -r attention-hook-skill/skills/attention-hook ~/.claude/skills/attention-hook
# DeepSeek Harness: copy to ~/.dsh/skills/attention-hook
```

**Claude Code plugin**

```
/plugin marketplace add yiyixiaoovo/attention-hook-skill
/plugin install attention-hook@attention-hook
```

**Single card** — each file under `skills/attention-hook/references/capabilities/` is a standalone card.

## What is inside

```
skills/attention-hook/
├── SKILL.md                  # router table + principles + boundaries
└── references/
    ├── capabilities/         # 18 cards (R/I/A1/A2/E/B)
    ├── capability-graph.md   # composes-with / contrasts-with / depends-on
    ├── capability-index.md   # intents & keywords
    ├── cheatsheet.md         # one-line rules
    ├── overview.md
    └── glossary.md
evals/
├── test-prompts/             # 18 routing suites (162 cases, minimum_pass_rate 0.8)
└── behaviors/                # 8 behavior suites (24 cases / 72 must-appear checks)
knowledge-base/               # reviews: pre-registered hypotheses, 4-level verdicts, limitations
source/                       # public excerpts + provenance
INDEX.md                      # capability table
verified.md                   # evidence conclusions & differential notes
coverage-audit.md             # key-task coverage audit
```

## Cards

| Card | One-liner |
|---|---|
| `gap-design` | Give a little information, leave a question you will pay off |
| `arousal-choice` | Choose by arousal, not by positive/negative valence |
| `concretize` | Replace abstract nouns with things you can see, count, imagine |
| `surprise-contrast` | A related-but-unexpected angle, not shock value |
| `distribution-first` | Decide where it is shown before optimizing opens or shares |
| `stickiness-pass` | Run the six-item checklist before publishing |
| `promise-integrity` | Every hook must point back to the paragraph that pays it off |
| `video-metrics` | Measure the first 5 seconds before rewriting |
| `story` | Stories are easier to understand and remember — not automatically more persuasive |
| `hook-craft` | Three beats / six slots / four failure modes / four channels (practitioner) |
| `x-playbook` | Posting on X and catching the traffic (practitioner) |
| `packaging` | Title–cover–opening triple (practitioner) |
| `script-flow` | Five-step script + mini hooks + a high-note ending (practitioner) |
| `story-craft` | Question, stakes, layered release (practitioner) |
| `audience-psychology` | Stance / symbols / obsession levels + mandatory ethics check (practitioner) |
| `content-business` | Audience avatar / 50-video plan / credibility line (practitioner) |
| `platform-native` | Xiaohongshu 3:4, IG 125-char fold, Douyin first 3s, X 280 (parameters drift) |
| `hook-forensics` | Sample table → deconstruction table → template → rewrite & compare |

## Evidence policy

- Every card's **section B** states what it does **not** support; strong evidence and practitioner
  heuristics are never mixed silently.
- Practitioner cards provide procedures only — no lift promises.
- Judge effects on your own account: see `knowledge-base/` and the A/B log in `stickiness-pass`.

## Sources & license

- Code and card text: MIT (`LICENSE`).
- Source list and licenses: `source/PROVENANCE.md`; short excerpts only, no full copyrighted texts.
- Practitioner material: Kallaway YouTube captions (short excerpts), an MIT-licensed Instagram skill
  pack (one verbatim quote), Xiaohongshu layout parameters from an AGPL repo (numeric facts only, no
  copied expression).

## About

Compiled from a capability bundle in [cangjie-skill](https://github.com/kangarooking/cangjie-skill).
