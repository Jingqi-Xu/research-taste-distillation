# Research Philosophy Extraction Methodology

> From academic papers to a runnable Research Philosophy Profile — core methodology

## 1. Triple Verification for Core Philosophy Pattern Identification

An observed pattern must pass triple verification before being classified as
"core research philosophy" rather than "a specific technical choice in one paper."

### Verification 1: Cross-Paper Replication

The same research philosophy tendency appears in at least 2 different papers by
the researcher, spanning different specific topics.

**Example: Kaiming He's "simplicity first"**
- ResNet (2015): A minimal skip connection solving the degradation problem
- Masked Autoencoders (2021): Simple masking + reconstruction for self-supervised learning
- Two papers with entirely different topics (classification vs. self-supervised), yet the methodological philosophy is consistent: **solve the core problem with the simplest mechanism**
→ Replicated across 2 topics → This is a core research philosophy

**Counter-example**:
- A researcher uses Transformer in one paper → This does NOT mean their philosophy is "only use Transformers" — it may just be the best tool available at the time

### Verification 2: Generative Power

This pattern can be used to predict the researcher's likely approach to a
**new problem they haven't published on**.

**Example**: If Kaiming He's "simplicity first" is a core philosophy —
- Facing a problem that seems to require a complex multi-stage pipeline → He would likely ask "Can a single end-to-end simple approach replace this?"
- Facing a new benchmark → He would likely first try the simplest baseline and see how far it goes
→ Can generate new predictions → This is genuine research philosophy

### Verification 3: Distinctiveness

Not all good researchers share this tendency. This pattern reflects the
researcher's **unique taste**.

**Example**: "Simplicity first" is characteristic of Kaiming He, but not all
top researchers share this —
- Some researchers' taste is "theoretical elegance" (pursuing mathematical proofs)
- Some researchers' taste is "systematic completeness" (covering all corner cases)
- Some researchers' taste is "scale wins" (pursuing scaling laws)
→ Has discriminative power → Worth extracting

**If a pattern passes only 1-2 verifications** → Downgrade to "decision heuristic"
**If a pattern passes 0 verifications** → Likely just a situational technical choice; discard

---

## 2. Research DNA Quantification

### 2.1 Writing Style Fingerprint

Extract structural features from the researcher's papers:

| Dimension | Measurement |
|-----------|------------|
| Introduction structure | Motivation-first? Problem-first? Result-first? |
| Math formalism level | No formulas / key formulas / full theorem-proof |
| Figure density | Figure-heavy vs. text-heavy |
| Related Work placement | Beginning (survey-style) vs. end (comparison-style) |
| Ablation depth | None / basic / exhaustive (decomposing every component) |
| Experiment vs. theory ratio | Pure experiment / experiment-led with theory / theory-led with experimental validation |

### 2.2 Argumentation Style Tags

```
Theory-driven ←→ Experiment-driven
Minimalist ←→ Systematically comprehensive
First-principles ←→ Empirical accumulation
Single core contribution ←→ Multi-contribution bundling
Motivation-heavy ←→ Result-heavy
```

### 2.3 Signature Phrases

- Keywords/phrases that recur across the researcher's papers
- Expression styles they never use
- Typical motivation templates (e.g., "Despite significant progress in X, Y remains challenging...")

---

## 3. Contradiction Handling Principles

Contradictions are core features of research taste, not bugs to be fixed.

### Three Types of Contradictions

1. **Temporal contradictions** (philosophy evolution)
   - The researcher leaned toward A early on, but toward B recently
   - Handling: Record the evolution trajectory, annotate "early" vs. "recent"
   - Example: Hinton from staunch BP believer to proposing Forward-Forward questioning BP

2. **Domain contradictions** (different strategies for different topics)
   - Leans toward X in computer vision, toward Y in NLP
   - Handling: Record per-domain, do not force unification
   - This reveals their differentiated understanding of different problems

3. **Essential tensions** (internal value conflicts)
   - Pursues simplicity yet uses complex architectures in some works
   - Handling: Explicitly record as "core tension"
   - This is usually the most interesting part of a researcher, and the most insightful angle for critiquing your idea

### Wrong Ways to Handle Contradictions
- ❌ Pick one side and ignore the other
- ❌ Fabricate a reconciliation narrative
- ❌ Pretend the contradiction doesn't exist

---

## 4. Handling Insufficient Information

| Situation | Handling |
|-----------|---------|
| Little paper information on a dimension | Annotate in Profile: "Insufficient information, this dimension is speculative" |
| Only abstract available | Lower confidence, annotate: "Inferred from abstract only" |
| Contradictory information that can't be resolved | Present both sides, let the user decide |
| Researcher's work in a certain area not covered | Explicitly note in honest boundaries: "Did not cover XX area" |

---

## 5. Quality Self-Check Checklist

After generating a Profile, self-check with these questions:

### Core Philosophy Patterns
- [ ] Does every pattern have evidence from at least 2 different papers?
- [ ] Is the pattern count between 3-7?
- [ ] Does every pattern have clear application scenarios and limitations?
- [ ] Do patterns have tension but are not self-contradictory?

### Research DNA
- [ ] Is the writing style description specific enough to distinguish different researchers?
- [ ] Are experiment design preferences backed by specific papers?

### Decision Heuristics
- [ ] Is every rule backed by specific paper examples?
- [ ] Can the rule be triggered by new ideas (not only applicable to original paper scenarios)?

### Anti-Patterns
- [ ] At least 3 clear "would never do" items?
- [ ] Backed by paper evidence (e.g., criticisms in related work, deliberate avoidance in method design)?

### Honest Boundaries
- [ ] Clearly states what cannot be extracted?
- [ ] Annotates paper coverage range and information sources?
- [ ] Acknowledges dimensions with insufficient information?

### Overall
- [ ] Does viewing a new research idea through this Profile yield valuable research taste perspective?
- [ ] Is it a distillation of philosophy patterns, not a collage of paper abstracts?
- [ ] Remove the name — can you still tell whose research taste this is?
