# AI Anatomy Drawing Prompts

A curated bundle of the **three most-starred GitHub resources** that teach AI agents
to draw human anatomy, skeletons, and animals **without hallucinating** extra fingers,
fused limbs, mutated faces, or impossible proportions.

Each pick is vendored into this repo as a git **subtree** under `skills/` so the
full source — prompts, skill files, examples, license, history — travels with
this repo and can be updated cleanly from upstream.

---

## Why this exists

"Bad anatomy" is the single most common failure mode of generative image models:
six-fingered hands, two-jointed elbows, mirrored faces, vestigial limbs, animals
with the wrong number of legs. Three communities on GitHub have published the
most-cited countermeasures:

1. A **negative-prompt vocabulary** that names every anatomical failure mode so
   the sampler steers away from them.
2. An **agentic skill** (Claude Code / Codex / OpenClaw) that wraps a curated
   prompt gallery, parameter best-practices, and a CLI — so the model is given
   structure instead of a blank canvas.
3. A **prompt cookbook** for OpenAI's GPT-Image-2 that pairs every example with
   the actual rendered output, reference-image anchoring, and explicit "Avoid"
   clauses so identity and proportions stay intact across edits.

Together they cover the three layers of the stack: **what to forbid** (negatives),
**how to ask** (skill scaffolding), and **what good looks like** (reference gallery).

---

## The three picks

| # | Repo | Stars | Why it made the cut |
|---|------|-------|---------------------|
| 1 | [`EvoLinkAI/awesome-gpt-image-2-API-and-Prompts`](https://github.com/EvoLinkAI/awesome-gpt-image-2-API-and-Prompts) | ~15.6k | The largest curated gallery of GPT-Image-2 prompts with paired output images, including portrait, character, and figure cases that lean hard on reference-image anchoring + explicit "Avoid: extra fingers, deformed hands, warped face" clauses. |
| 2 | [`wuyoscar/GPT-Image2-Skill`](https://github.com/wuyoscar/GPT-Image2-Skill) | ~2.4k | The top-ranked agentic **skill** (Claude Code / Codex / OpenClaw) for image generation. Ships a `SKILL.md`, CLI, parameter cheatsheets, and a deliberately small, high-signal gallery covering character design, figure illustration, and animal subjects. |
| 3 | [`mikhail-bot/stable-diffusion-negative-prompts`](https://github.com/mikhail-bot/stable-diffusion-negative-prompts) | ~90 | The most-direct match for the brief: a battle-tested vocabulary of negative prompts (`bad anatomy`, `mutated hands`, `extra fingers`, `fused fingers`, `missing limbs`, `long neck`, `malformed limbs`, `disfigured`, `cloned face`) that ships with every modern SD-style stack. Small star count, outsized influence — these tokens are copy-pasted into millions of generations. |

Each lives under `skills/<name>/`.

---

## 1. `awesome-gpt-image-2-API-and-Prompts` — the reference gallery

**Location:** [`skills/awesome-gpt-image-2-API-and-Prompts/`](skills/awesome-gpt-image-2-API-and-Prompts/)
**Upstream:** https://github.com/EvoLinkAI/awesome-gpt-image-2-API-and-Prompts
**License:** CC0 1.0

### What it gives you

- **583+ curated prompt cases** organised by use case (portrait, character
  design, poster & illustration, e-commerce, ad creative, UI mockups).
- For *every* case: the exact prompt, the rendered output, and (where relevant)
  an "Avoid" section listing the anatomical failures the prompt is engineered
  to suppress.
- API usage patterns for `/v1/images/generations` and the multi-turn editing
  flow that lets you keep a subject's face/proportions stable across iterations.
- 11 language localisations of the README.

### Anti-hallucination techniques it teaches

| Technique | Example clause |
|-----------|----------------|
| Reference-image anchoring | *"use the uploaded photo as main reference; preserve the exact facial features"* |
| Negative phrasing inside positive prompts | *"Avoid: extra fingers, deformed hands, warped face"* |
| Identity locking across edits | *"Do not alter my facial features, only change the background"* |
| Visual over-specification | dense descriptors that leave no anatomical detail for the model to guess |
| Output verification | every prompt is published next to its real generated image, so users can compare expected vs. actual anatomy before reusing the prompt |

> ⚠️ The authors caution against using outputs as-is in academic figures —
> always validate anatomy against ground truth.

### Best for
Browsing for a known visual style and lifting the negative/avoid clauses
verbatim into your own pipeline.

---

## 2. `GPT-Image2-Skill` — the agentic skill

**Location:** [`skills/GPT-Image2-Skill/`](skills/GPT-Image2-Skill/)
**Upstream:** https://github.com/wuyoscar/GPT-Image2-Skill
**License:** MIT

### What it gives you

- A complete **agent skill** folder (`skills/gpt-image/`) ready to drop into
  Claude Code, Codex (`$skill-installer`), OpenClaw, or Hermes Agent.
- A `gpt-image` **CLI** for batch generation/editing with the OpenAI API.
- Markdown reference guides covering parameter semantics (`size`, `quality`,
  `n`, `format`), OpenAI's official prompting best-practices, and a per-domain
  craft checklist.
- A curated (intentionally small) gallery: character design, figure
  illustration, pixel-art creatures, and photorealistic wildlife.

### Anti-hallucination techniques it teaches

| Technique | How the skill applies it |
|-----------|--------------------------|
| Curated, not crawled | "Small but mighty — curated for signal, not volume." Every example is hand-vetted, so anatomy patterns aren't averaged across junk prompts. |
| Constraint-based prompts | Each entry uses explicit negations (*"no nudity," "no existing copyrighted characters"*) and bounded descriptors. |
| Local guides bundled with the skill | The agent has on-disk reference markdown to consult before issuing a generation — closes the loop where the model would otherwise improvise parameters. |
| Workflow caution | An on-skill warning instructs the agent to treat outputs as sketches, never as ground-truth anatomy for research figures. |
| Reproducibility | Prompts are versioned alongside seed/parameter metadata so anatomy regressions are catchable in diffs. |

### Best for
Teams that want an installable, callable skill — not a copy-paste cookbook.
Plays nicely with `claude-code` plugin marketplaces and Codex skill installers.

```bash
# Claude Code
/plugin marketplace add wuyoscar/gpt_image_2_skill
/plugin install gpt-image@wuyoscar-skills
```

---

## 3. `stable-diffusion-negative-prompts` — the anti-hallucination vocabulary

**Location:** [`skills/stable-diffusion-negative-prompts/`](skills/stable-diffusion-negative-prompts/)
**Upstream:** https://github.com/mikhail-bot/stable-diffusion-negative-prompts
**License:** see upstream `LICENSE`

### What it gives you

A short, dense list of negative-prompt strings collected from Prodia, Reddit,
ImgSli, and community contributors. Every string is engineered around
anatomical failure modes. The repo's entire purpose is captured in this single
canonical block:

> `((((ugly)))), (((duplicate))), ((morbid)), ((mutilated)), out of frame, extra
> fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)),
> (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad
> proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame,
> ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs),
> ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))),
> mutated hands, (fused fingers), (too many fingers), (((long neck)))`

### The taxonomy of hallucinations it neutralises

| Failure mode | Tokens it forbids |
|--------------|-------------------|
| Hands & fingers | `extra fingers`, `fused fingers`, `too many fingers`, `missing fingers`, `extra digit`, `fewer digits`, `broken finger`, `twisted fingers`, `disfigured hand`, `poorly drawn hands` |
| Limbs | `extra limbs`, `missing arms`, `missing legs`, `extra arms`, `extra legs`, `malformed limbs`, `floating limbs`, `disconnected limbs`, `missing limb`, `split limbs`, `disembodied limb`, `linked limb` |
| Body proportions | `bad anatomy`, `gross proportions`, `long neck`, `long body`, `bad proportions`, `disfigured butt`, `extra knee`, `extra elbow` |
| Faces | `poorly drawn face`, `cloned face`, `2 heads`, `2 faces`, `cross-eye`, `squint`, `deformed face`, `irregular face`, `blurred faces` |
| General morphology | `mutated`, `mutation`, `deformed`, `disfigured`, `mutilated`, `morbid`, `amputee`, `severed`, `dismembered` |
| Quality / framing | `out of frame`, `cropped`, `low-res`, `blurry`, `jpeg artifacts`, `watermark`, `signature` |

These tokens generalise: they work for human anatomy, skeletons (the same
"extra limbs / fused" failure modes apply), and animals (apply to legs, paws,
ears, tails — the same vocabulary catches polydactyl pets and four-eared
rabbits).

### Best for
Dropping straight into the **negative prompt** field of any Stable
Diffusion, SDXL, Flux, or ComfyUI workflow. Also a useful seed list when
authoring "Avoid:" clauses for closed-source models that don't expose a
dedicated negative-prompt parameter (GPT-Image-2, Nano Banana, Midjourney
v6+ with `--no`).

---

## How the three fit together

```
   ┌─────────────────────────────────────────────────────────┐
   │  USER INTENT: "Draw a skeleton holding a cat"           │
   └─────────────────────────────────────────────────────────┘
                 │
                 ▼
   ┌─────────────────────────────────────────────────────────┐
   │  2. GPT-Image2-Skill                                    │
   │     - Agent picks the closest gallery exemplar          │
   │     - Loads parameter cheatsheet                        │
   │     - Issues a structured prompt                        │
   └─────────────────────────────────────────────────────────┘
                 │
                 ▼
   ┌─────────────────────────────────────────────────────────┐
   │  1. awesome-gpt-image-2-API-and-Prompts                 │
   │     - Lifts the matching positive prompt + Avoid clause │
   │     - Anchors identity with a reference image           │
   └─────────────────────────────────────────────────────────┘
                 │
                 ▼
   ┌─────────────────────────────────────────────────────────┐
   │  3. stable-diffusion-negative-prompts                   │
   │     - Appends the anatomy negative vocabulary           │
   │     - (or: rephrased as "Avoid:" for GPT-Image-2)       │
   └─────────────────────────────────────────────────────────┘
                 │
                 ▼
                Image (audited against reference)
```

---

## Selection methodology

GitHub repository search on **2026-05-27**, sorted by stars, intersected with
the following criteria:

1. Explicit focus on **prompts** or **agent skills** (not model weights, not
   apps, not 3D viewers).
2. Demonstrable coverage of **human anatomy / skeletons / animal** drawing,
   either via dedicated cases or via vocabulary that targets anatomical
   failure modes.
3. Active maintenance in the last 12 months (`pushed:>2025-05-27`).
4. Real signal — not Coursera-class fork chains.

Queries that produced the shortlist:
- `anatomy drawing AI prompt skill in:name,description,readme stars:>10`
- `claude skill drawing anatomy svg in:name,description,readme`
- `stable-diffusion-negative-prompts sort:stars`
- `awesome claude skills sort:stars` (for skill-format candidates)

Honourable mentions that lost on either stars or scope:
- `Sunwood-ai-labs/draw-io-skill` — diagrams, not anatomy.
- `Agents365-ai/excalidraw-skill` — hand-drawn style, no anatomy gallery.
- `bentossell/visualise` — inline SVG, agent-focused, but no anatomy coverage.
- `minimaxir/stable-diffusion-negative-prompt` — experimentation notebook
  rather than a reusable vocabulary.

---

## Repo layout

```
exec_dashbd/
├── LICENSE
├── README.md                                ← you are here
└── skills/
    ├── awesome-gpt-image-2-API-and-Prompts/  (subtree @ EvoLinkAI/main)
    ├── GPT-Image2-Skill/                     (subtree @ wuyoscar/main)
    └── stable-diffusion-negative-prompts/    (subtree @ mikhail-bot/main)
```

Each subtree carries its own `LICENSE` and `README.md`; refer to those for
upstream license terms and contribution guidelines.

## Updating a subtree from upstream

```bash
# Pull latest from any one of the three
git subtree pull --prefix=skills/awesome-gpt-image-2-API-and-Prompts \
  https://github.com/EvoLinkAI/awesome-gpt-image-2-API-and-Prompts.git main --squash

git subtree pull --prefix=skills/GPT-Image2-Skill \
  https://github.com/wuyoscar/GPT-Image2-Skill.git main --squash

git subtree pull --prefix=skills/stable-diffusion-negative-prompts \
  https://github.com/mikhail-bot/stable-diffusion-negative-prompts.git main --squash
```

## License

This curation/README is released under the repo's existing `LICENSE`. Each
vendored subtree retains its own upstream license; do not re-license their
contents.
