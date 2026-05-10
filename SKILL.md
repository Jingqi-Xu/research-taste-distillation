---
name: research-taste-distillation
description: |
  Research Taste Distillation: extract research philosophy from top researchers'
  papers, then use the extracted philosophy to critique and improve your research idea.
  Supports multi-researcher fusion for collective intelligence.
  Trigger phrases: "distill research taste", "extract research philosophy",
  "critique my idea from XX's perspective", "research taste", "research philosophy",
  "improve my idea", "how would XX evaluate this idea"
---

# Research Taste Distillation

> "Not imitating how they talk — extracting recurring research philosophy patterns
> from their papers, and using those patterns to improve your idea."

## Core Principles

This is NOT role-playing. This is extracting **verifiable research philosophy
patterns** from academic papers, then using those patterns as lenses to examine
your idea.

A good Research Philosophy Profile is a runnable **research taste operating system**:
- What kind of **problems** do they choose? (problem taste)
- What **methods** do they prefer? (method philosophy)
- How do they **validate** their work? (evidence standards)
- What do they **never do**? (anti-patterns)
- How has their taste **evolved**? (temporal trajectory)
- What **can't we extract**? (honest boundaries)

**Key distinction**: We capture HOW they do research, not WHAT they published.

---

## Execution Pipeline

### Phase 0: Requirements Clarification

Upon receiving user input, confirm the following:

1. **Researcher list**: Whose research philosophy to distill? (one or more)
2. **Your research idea**: What idea needs to be critiqued and improved?
3. **Your goal**: Top-venue paper? Long-term research direction? Quick prototype?
4. **Paper sources** (optional):
   - User has PDFs? → Analyze directly (highest quality)
   - Has arXiv ID list? → Fetch directly
   - Neither? → Auto-search via Semantic Scholar
5. **Focus direction** (optional): Full portrait vs. focused dimension (e.g., methodology only)

If the user simply says "use XX's perspective on my idea" with no further info →
default to Semantic Scholar search + full portrait + paper-publishing goal.
Proceed immediately.

After confirmation → Phase 0.5.

---

### Phase 0.5: Create Workspace

**Execute immediately after confirmation**:

```
.claude/skills/research-taste-distillation/
├── SKILL.md                          # This file (already exists)
├── references/
│   ├── extraction-framework.md       # Extraction methodology
│   └── profile-template.md           # Profile output template
└── workspace/                        # Working directory for current run
    ├── profiles/                     # Extracted philosophy profiles
    │   ├── {researcher-name}.md      # One per researcher
    │   └── ...
    ├── critiques/                    # Idea critique results
    │   ├── {researcher-name}-critique.md
    │   └── ...
    ├── fusion/                       # Multi-expert fusion results
    │   └── fusion-result.md
    └── papers/                       # Paper research records
        ├── {researcher-name}/
        │   ├── paper-list.md         # Paper list and metadata
        │   └── signals/              # Per-paper extraction signals
        │       ├── paper-1.md
        │       └── ...
        └── ...
```

**Key rules**:
- Every intermediate result must be written to a file. Analysis without file output is analysis not done.
- All files must reside within workspace/ to keep things self-contained.

---

### Phase 1: Paper Collection

For each researcher, collect their representative papers.

#### Path A: User-provided PDFs / arXiv IDs

Use user-provided materials directly, skip search. Record paper info in
`papers/{name}/paper-list.md`.

#### Path B: Semantic Scholar Auto-Search

Use WebSearch to find the researcher's papers:

```
Search strategy:
1. "{researcher name} most cited papers site:semanticscholar.org"
2. "{researcher name} recent papers 2024 2025 2026"
3. "{researcher name} {field} seminal work"
```

**Collection targets**:
- Highly cited landmark works (top 5-8 papers)
- Recent work from the past 3 years (3-5 papers)
- Total 10-15 papers, covering different stages of their career

**Record for each paper**:
- Title, year, venue, citation count
- Abstract (required)
- If full text is accessible → record Introduction and Method sections (highest information density)

**Output**: `papers/{name}/paper-list.md`, formatted as:

```markdown
# {Researcher Name} - Paper Collection

## Paper List

| # | Title | Year | Venue | Citations | Source |
|---|-------|------|-------|-----------|--------|
| 1 | ...   | ...  | ...   | ...       | Abstract / Full |

## Source Notes
- Search channels: Semantic Scholar / arXiv / User-provided
- Coverage range: YYYY-YYYY
- Known gaps: [if any]
```

---

### Phase 2: Per-Paper Philosophy Signal Extraction (MAP Step)

First, read `references/extraction-framework.md` for the full extraction methodology.

For each paper in `paper-list.md`, extract philosophy signals across 8 dimensions:

```
For this paper:
1. Problem Selection — What type of problem was chosen? Why is it important?
2. Solution Style — What is the method design philosophy? (minimal / elegant math / brute-force scaling / modular)
3. Assumptions — What key assumptions or bets does this work make?
4. Evidence Style — How are claims supported? (ablation / scaling law / SOTA / visualization / theoretical proof)
5. Research Taste Signal — What does this paper reveal about the author's deeper research taste?
6. Writing DNA — How is the paper structured and argued? (motivation-first / result-first / math-heavy / intuition-driven)
7. What They Didn't Do — What did this paper deliberately NOT do? (implied anti-patterns)
8. Framing — How is the problem framed? Where does the motivation come from?
```

**Write each paper's extraction result to** `papers/{name}/signals/paper-{n}.md`.

**Key rules**:
- Extract based on actual paper content. Do not fabricate things the paper didn't express.
- Distinguish "explicitly stated in the paper" vs. "inferred by me".
- When information is insufficient, annotate: "Limited information, this dimension is speculative."

---

### Phase 2.5: Signal Review Checkpoint

**After all papers are extracted, pause and display an extraction quality summary**:

```
┌──────────────────┬──────────┬──────────────────────────────────┐
│ Paper            │ Quality  │ Key Findings                     │
├──────────────────┼──────────┼──────────────────────────────────┤
│ Paper 1          │ Full/Abs │ Minimalist methodology, strong   │
│                  │          │ ablation preference ...           │
│ Paper 2          │ Full/Abs │ First-principles, quality >      │
│                  │          │ novelty ...                       │
│ ...              │ ...      │ ...                              │
├──────────────────┼──────────┼──────────────────────────────────┤
│ Cross-paper      │ —        │ Recurring: simplicity, generality│
│ preliminary      │          │ prioritized ...                   │
│ patterns         │          │                                  │
│ Insufficient     │ —        │ Early work coverage lacking ...  │
│ dimensions       │          │                                  │
└──────────────────┴──────────┴──────────────────────────────────┘
```

User confirms OK → Phase 3.
User wants more on a dimension → supplement search, then continue.

---

### Phase 3: Cross-Paper Aggregation & Triple Verification (REDUCE Step)

Synthesize all per-paper signals into a unified Research Philosophy Profile.

#### 3.1 Candidate Pattern Identification

Scan all `signals/paper-{n}.md`, list all candidate research philosophy patterns
(typically 15-25 candidates).

#### 3.2 Triple Verification Filtering

For each candidate pattern, apply triple verification
(see `references/extraction-framework.md` for full details):

| Verification | Criterion | Passing Requirement |
|-------------|-----------|---------------------|
| **Cross-paper replication** | Appears in ≥2 different papers / different periods / different topics | Not a specific technical choice in one paper, but a recurring philosophical tendency |
| **Generative power** | Can predict the researcher's approach to new problems | Knowing this pattern, you can predict their reaction to an unseen idea |
| **Distinctiveness** | Not something all good researchers would do | A taste **unique** to this researcher, not generic research methodology |

- Passes all 3 → **Core Philosophy Pattern** (select 3-7)
- Passes 1-2 → **Decision Heuristic** (select 5-10)
- Passes 0 → Discard (just a specific technical choice in one paper)

**Fewer is better** — 3 profound core patterns are far better than 10 shallow principles.

#### 3.3 Anti-Pattern Extraction

Identify practices the researcher **explicitly opposes or never adopts**:
- What do their papers never do?
- What approaches do they criticize in related work?
- What does their methodology imply they reject?

#### 3.4 Research DNA Analysis

| Dimension | What to Extract |
|-----------|----------------|
| Writing style | Paper structure preference (motivation-heavy / result-first / theory-guided) |
| Argumentation structure | How they build arguments (experiment-first / theoretical derivation / intuition-guided) |
| Experiment design preference | Preferred experiments (ablation-heavy / scaling study / transfer / visualization) |
| Formalism level | Math-heavy / moderate / lightweight |
| Collaboration pattern | Solo theorist / large team / fixed co-author clusters |
| Signature phrases | Recurring expressions in their papers |

#### 3.5 Evolution Trajectory

Identify how their research philosophy changed over time:
- Early career (PhD/postdoc) → mid-career → recent
- Key inflection points: what events changed their direction or methodology?
- **Contradiction is depth**: inconsistencies over time are often the most insightful

#### 3.6 Internal Tensions

Identify internal contradictions in the researcher's philosophy:
- e.g., Pursuing minimalism yet using heavyweight architectures in some works
- e.g., Emphasizing theory yet most work is empirically driven
- **Do not reconcile contradictions — preserve them.** Contradictions are core features of personality.

#### 3.7 Honest Boundaries

Explicitly annotate:
- Which papers were analyzed, which were not covered
- Which dimensions have insufficient information
- Which judgments are high-confidence, which are speculative
- Published papers ≠ all thoughts — we cannot extract what they didn't write

#### 3.8 Output

Read `references/profile-template.md`, fill in the template, and write the Profile
to `workspace/profiles/{researcher-name}.md`.

---

### Phase 3.5: Profile Confirmation Checkpoint

**Display extraction summary for user confirmation**:

```
Extraction Summary: {Researcher Name}
- Core philosophy patterns: N (list names and one-line descriptions)
- Decision heuristics: N
- Research DNA: [3 key characteristics]
- Anti-patterns: N items
- Internal tensions: N pairs
- Honest boundaries: N items
- Paper coverage: YYYY-YYYY, N papers total
```

User confirms OK → Phase 4.
User thinks a pattern is wrong or missing → return to Phase 3 to adjust.

**Why this checkpoint matters**: Profile quality determines the ceiling for
subsequent critique. Catching issues here is far cheaper than rework in Phase 5.

---

### Phase 4: Quality Verification

Run a 6-dimension quality self-check on the generated Profile:

| Check Item | Pass Criteria | Failure Signal |
|-----------|--------------|----------------|
| Core pattern count | 3-7, each with ≥2 paper evidence | <3 or >10 |
| Limitation per pattern | Explicitly states failure conditions | Only lists strengths |
| Anti-patterns | At least 3 "would never do" items | No anti-patterns |
| Internal tensions | At least 1-2 contradictions | Perfectly consistent (too clean) |
| Honest boundaries | At least 3 specific limitations | Only "cannot replace the person" |
| Distinctiveness | Remove the name — can you still tell whose philosophy this is? | Could describe any good researcher |

Fails → annotate weak areas, revise once.
Still fails after revision → note weak dimensions in honest boundaries, proceed.

**Better to deliver an honest 60-point Profile with clear limitations than a
seemingly perfect 90-point Profile that fabricates claims.**

---

### Phase 5: Idea Critique

For each researcher's Philosophy Profile, independently generate a structured critique.

**Key principle**:

```
You are NOT {Researcher Name}.
You are an analytical agent using a Research Philosophy Profile extracted from
{Researcher Name}'s public papers.
Your job is to critique and improve the user's idea according to the extracted
philosophy patterns.
You must cite profile evidence.
Do not claim what the real person would think.
Use "Based on the extracted patterns from {Name}'s published work, ..." to phrase suggestions.
```

**Each critique contains 9 sections**:

1. **Core Diagnosis** (2-3 sentences): What is the essence of this idea, what is its core bet?
2. **Strengths** (3-5 items): Which aspects align with the philosophy? Cite specific verified patterns.
3. **Weaknesses** (3-5 items): Which aspects conflict with the philosophy? Cite specific anti-patterns.
4. **Philosophy-based Reshape** (1-2 paragraphs): How would the philosophy patterns suggest re-framing this problem?
5. **Improved Idea** (1-2 paragraphs): A concrete improved version of the idea.
6. **Suggested Experiments** (3-5 items): Based on the researcher's evidence_preferences.
7. **Risks** (2-4 items): Remaining risks after improvement.
8. **Cited Evidence**: Which profile evidence items support each key suggestion.
9. **Confidence Notes**: Label which suggestions are based on "core philosophy" (high confidence) vs. "heuristic" (medium) vs. "speculation" (low).

**Output**: Write to `workspace/critiques/{researcher-name}-critique.md`.

---

### Phase 6: Multi-Expert Fusion

**Execute only when ≥2 researchers are specified.**

Read all critiques and perform cross-analysis:

#### 6.1 Consensus Identification
Improvement directions that multiple researchers' philosophy patterns
**independently converge on** → high-confidence suggestions.

#### 6.2 Conflict Preservation
Disagreements between researchers are not bugs to eliminate —
they are **valuable tensions**.

Format:
```
Agent A (based on {pattern X}) suggests Y,
while Agent B (based on {pattern Z}) suggests W.
This tension reflects a fundamental difference between [philosophy A] and [philosophy B].
```

#### 6.3 Conflict Resolution
Make trade-offs based on the user's goal (publish paper / long-term direction /
quick prototype), but **must explain why**.

#### 6.4 Final Idea
Synthesized improved idea (2-3 paragraphs).

#### 6.5 Three Variants

| Variant | Positioning |
|---------|------------|
| **Safe Version** | Conservative, easy to execute, high probability of producing a solid paper |
| **Strong Conference Version** | Optimized for novelty, aiming for top venue |
| **Ambitious Long-term Version** | Bold, potentially high-impact long-term research direction |

#### 6.6 Honest Boundaries
What this fusion analysis **cannot tell the user**:
- Blind spots in areas none of the selected researchers cover
- Limitations inherent to paper-based extraction
- etc.

**Output**: Write to `workspace/fusion/fusion-result.md`.

---

### Phase 7: Final Delivery

Present complete results to the user in this order:

1. **Executive Summary**: One paragraph summarizing the core conclusion
2. **Profile Highlights**: Core patterns + key insights for each researcher (summary, not full text)
3. **Critiques**: Key points from each researcher's perspective
4. **Fusion** (if multi-researcher): Consensus, conflicts, final idea, three variants
5. **Next Steps**: Recommended next actions based on the analysis

Inform the user: full detailed reports are saved in the `workspace/` directory.

---

## Taste Codex (Quick Reference)

Consult when facing judgment calls.

| Principle | One-liner |
|-----------|-----------|
| Papers > Hearsay | A researcher's papers reveal their philosophy better than any secondhand interpretation |
| Method > Result | Method choices reveal taste more than results — why they chose a method matters more than what score it got |
| Recurring > One-off | Patterns in 3+ papers = real philosophy; a single paper's choice may just be situational |
| Evolution > Static | Changes in research philosophy are more informative than consistency |
| Contradiction > Consistency | Internal tensions are a source of depth — don't smooth them out |
| Honesty > Perfection | Annotating limitations is more valuable than fabricating completeness |

### Things We Never Do
- Fabricate research opinions the researcher never expressed in their papers
- Package generic "good research standards" as someone's "unique taste"
- Say "XX would think this" — instead say "based on patterns extracted from XX's papers"
- Generate high-confidence judgments when information is insufficient
- Ignore disagreements between researchers and simply average their advice

---

## Special Scenarios

### Researcher Type Adaptation

| Type | Strategy |
|------|----------|
| **Highly prolific** (100+ papers) | Focus on top-cited + recent 3 years, cap at 15 papers |
| **Emerging researcher** (<20 papers) | Can cover all papers; annotate "based on limited sample" in Profile |
| **Cross-disciplinary** | Confirm which field the user cares about; focus on that paper subset |
| **Collaboration-heavy** | Attempt to distinguish which patterns are unique to this researcher vs. shared across the co-author group |

### Single vs. Multiple Researchers

- **Single researcher**: Skip Phase 6 (fusion), go directly from Phase 5 critique to Phase 7
- **Multiple researchers**: Execute Phase 6 in full; conflict preservation is the most valuable output

### Profile-Only Mode (No Idea)

User says "distill XX's research philosophy" without providing an idea → execute
Phase 1-4 only, output Profile, skip critique. Inform user: "Profile generated and
saved. You can submit your idea anytime to receive critique."

### Adding Researchers Later

User says "add YY's perspective too" → execute Phase 1-4 for YY, then re-run
Phase 6 to fuse all researchers' critiques.

---

## Final Words

What this Skill extracts is not the researcher themselves — it is a **mirror
constructed from their papers**.

A good Research Philosophy Profile lets you see your own idea through another
researcher's eyes. Not to imitate them, but to **expand the boundaries of your
own research taste**.

Better to admit "we can't extract their true inspiration and intuition" than to
pretend we can perfectly replicate someone's research taste.

---

> This Skill is inspired by [nuwa-skill](https://github.com/alchaincyf/nuwa-skill),
> adapting its "distill how anyone thinks" methodology for academic research.
