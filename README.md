# Research Taste Distillation

> *"What if Kaiming He could review your research idea? Not the person — the patterns behind 70+ papers."*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)

**Distill research philosophy from top researchers' papers, then use that philosophy to critique and improve your ideas.**

Not role-playing. Not "what would Kaiming say." This extracts **verifiable research philosophy patterns** — the recurring problem-selection instincts, method-design taste, and evidence standards embedded in a researcher's body of work — then uses those patterns as lenses to examine your idea.

[See it in action](#demo) · [Install](#installation) · [How it works](#how-it-works) · [What gets extracted](#what-gets-extracted)

---

## Demo

### Distilled Profile: Kaiming He

After analyzing 8 papers (ResNet, MAE, MoCo, Mask R-CNN, ...), the system extracts 5 triple-verified core philosophy patterns:

```
Core Pattern 1: "Minimal Surgery"
Solve the most critical problem with the simplest possible intervention.

  Evidence:
  - ResNet: a shortcut connection (a few lines of code) solving the degradation problem
  - MAE: strip away tokenizer, contrastive learning, momentum encoder — keep only masking + reconstruction
  - Mask R-CNN: RoIAlign + one mask branch extending instance segmentation

  Generative Power: When He faces a new problem, his first move is to find
  "what is THE bottleneck" and fix it at minimal cost. He never designs a
  complex system first and ablates down.

  Distinctiveness: Many researchers pursue simplicity, but He's minimalism
  is more radical — he asks "remove X, does it still work?" and keeps
  deleting until nothing more can be removed.
```

```
Core Pattern 3: "Challenge the Obvious"
Actively question field consensus. Treat "common knowledge" as unverified hypotheses.

  Evidence:
  - Rethinking ImageNet Pre-training (2019): questions "pre-training is necessary"
  - MAE (2021): questions "BERT-style masking doesn't work for vision"
  - Transformers without Normalization (2025): questions "norm layers are essential"
  - He Init (2015): questions "Xavier init is correct for ReLU networks"

  Spanning 2015-2025, this is a career-long pattern.
```

The full profile also includes decision heuristics, anti-patterns, Research DNA, evolution trajectory, internal tensions, and honest boundaries. See the [complete example](examples/kaiming-he/profile.md).

This is not "Kaiming He would say X." This is: *"Based on patterns that recur across ResNet, MAE, MoCo, and 5 other papers, here's what that research taste implies about your idea."*

---

## Installation

```bash
# Copy the skill into your project
cp -r skill/ your-project/.claude/skills/research-taste-distillation/
```

Then in [Claude Code](https://claude.ai/code):

```
> Distill Kaiming He's research taste, then critique my idea

> Improve my idea from Kaiming He and Yann LeCun's perspectives:
> I want to build a self-supervised method that ...

> Just distill Geoffrey Hinton's research philosophy (no critique)
```

That's it. No dependencies, no API keys, no setup. Claude Code does the rest.

---

## How It Works

### The Pipeline

```
Phase 1                Phase 2              Phase 3              Phase 4
Paper Collection  →  Per-Paper Signal  →  Cross-Paper       →  Quality
(Semantic Scholar     Extraction (MAP)     Aggregation &         Verification
 or user PDFs)        8 dimensions         Triple Verify         6-dimension
                                           (REDUCE)              self-check

Phase 5                Phase 6              Phase 7
Idea Critique     →  Multi-Expert     →  Final Delivery
(per researcher)     Fusion                (3 variants)
                     (if ≥2 researchers)
```

### What Gets Extracted

We don't summarize papers. We extract **how they do research**:

| Layer | What's Captured |
|-------|----------------|
| **Problem taste** | What problems do they choose? What makes a problem "interesting" to them? |
| **Method philosophy** | Minimalist? Elegant math? Brute-force scaling? Modular systems? |
| **Evidence standards** | Ablation-driven? Scaling laws? Transfer as gold standard? Visualization? |
| **Anti-patterns** | What they NEVER do — often more revealing than what they do |
| **Research DNA** | Writing style, argumentation structure, signature phrases, formalism level |
| **Evolution** | How their taste changed over time — contradictions are the most insightful |
| **Internal tensions** | Contradictions are features, not bugs. Preserved, never reconciled. |
| **Honest boundaries** | What we CAN'T extract. Every profile admits its own limitations. |

### Triple Verification

An observed pattern must pass three checks before being classified as "core research philosophy" rather than "a technical choice in one paper":

```
                         Candidate Pattern
                               │
                  ┌────────────┼────────────┐
                  ▼            ▼            ▼
           Cross-Paper    Generative    Distinctive
           Replication      Power
                  │            │            │
            Appears in    Can predict    Not generic
            ≥2 papers,    approach to    "good research"
            different     NEW unseen     — unique to
            topics        problems       THIS researcher
                  │            │            │
                  └────────────┼────────────┘
                               │
              ┌────────────────┼────────────────┐
              ▼                ▼                ▼
         All 3 pass       1-2 pass          0 pass
              │                │                │
        Core Philosophy   Decision          Discard
        Pattern (3-7)     Heuristic
                          (5-10)
```

**Fewer is better** — 3 profound core patterns beat 10 shallow principles.

### Multi-Expert Fusion

When you specify multiple researchers (e.g., Kaiming He + Yann LeCun + Geoffrey Hinton):

1. **Independent distillation** — Each researcher gets their own full profile (Phase 1-4, in parallel)
2. **Independent critique** — Each profile independently critiques your idea
3. **Consensus identification** — Where multiple philosophies converge → high-confidence suggestions
4. **Conflict preservation** — Disagreements are NOT bugs. They are **valuable tensions** that reveal fundamental trade-offs
5. **Three variants** — Safe (solid paper), Strong (top venue), Ambitious (long-term impact)

---

## What This Is NOT

| | Role-Playing | Research Taste Distillation |
|---|---|---|
| Source | General knowledge + stereotypes | Specific papers, cited with evidence |
| Claim | "Kaiming He would say..." | "Based on patterns from He's papers..." |
| Verification | None | Triple-verified: replication × generative power × distinctiveness |
| Limitations | Hidden | Explicitly stated as "honest boundaries" |
| Anti-patterns | Rarely captured | Core output: what they NEVER do |
| Contradictions | Smoothed over | Preserved as "internal tensions" |

---

## File Structure

```
research-taste-distillation/
├── SKILL.md                        # Main instruction file (the "brain")
├── README.md
├── references/
│   ├── extraction-framework.md     # Triple verification + Research DNA methodology
│   └── profile-template.md         # Profile output template
└── examples/                       # Pre-built example outputs
    └── kaiming-he/
        └── profile.md              # Distilled philosophy profile
```

---

## Taste Codex

Core principles that guide every extraction:

| Principle | Why |
|-----------|-----|
| **Papers > Hearsay** | A researcher's papers reveal philosophy better than any secondhand interpretation |
| **Method > Result** | Why they chose a method matters more than what score it got |
| **Recurring > One-off** | Patterns in 3+ papers = real philosophy; one paper's choice may be situational |
| **Evolution > Static** | Philosophy changes are more informative than consistency |
| **Contradiction > Consistency** | Internal tensions are depth, not noise |
| **Honesty > Perfection** | A 60-point profile with honest limitations beats a fabricated 90-point one |

---

## Inspiration

This project is inspired by [nuwa-skill](https://github.com/alchaincyf/nuwa-skill), which demonstrated that distilling anyone's cognitive framework into a runnable skill is not only possible but powerful.

**nuwa-skill** distills how people *think* — mental models, decision heuristics, expression DNA — from public figures across all domains.

**Research Taste Distillation** adapts this methodology for **academic research**: replacing public speeches and social media with *papers*, replacing expression DNA with *Research DNA*, and adding domain-specific innovations like triple verification against paper evidence, anti-pattern extraction from methodology choices, and multi-expert fusion with conflict preservation.

| | nuwa-skill | Research Taste Distillation |
|---|---|---|
| **Source material** | Books, talks, interviews, social media | Academic papers |
| **Target** | Anyone (entrepreneurs, investors, creators) | Researchers |
| **Extracts** | Mental models, expression DNA | Research philosophy, method taste, evidence standards |
| **Verification** | Triple-verified mental models | Triple-verified philosophy patterns (paper evidence) |
| **Unique additions** | — | Anti-patterns from methodology, Research DNA, internal tensions, evolution trajectory |

---

## Contributing

Contributions welcome! Particularly:

- **New researcher profiles** — Run the skill, validate the output, submit as an example
- **Prompt improvements** — Better extraction or critique instructions in SKILL.md
- **Methodology refinements** — Improvements to triple verification or fusion logic

---

## License

MIT — use it, modify it, distill with it.

---

<p align="center">

**nuwa-skill** distills how people think.<br>
**Research Taste Distillation** distills how researchers do research.<br>
<i>The next advisor you want doesn't have to be on your committee.</i>

</p>
