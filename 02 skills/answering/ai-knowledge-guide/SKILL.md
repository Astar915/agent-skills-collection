---
name: ai-knowledge-guide
description: Answer AI, machine learning, deep learning, LLM, paper, experiment, and AI engineering questions by checking the user's personal AI notes first, then reasoning from current evidence and consulting authoritative sources when needed.
---

# AI Knowledge Guide

## Mandatory AI-question rule

For every question related to AI, machine learning, deep learning, LLMs,
generative AI, papers, experiments, prompts, models, APIs, frameworks,
evaluation, deployment, or AI safety, use this skill. This includes conceptual
questions, comparisons, quizzes, code, debugging, architecture decisions, and
current product or model behavior.

Follow this order:

```text
Search the user's personal `20. AI notes` knowledge base first, when it exists
→ Inspect the user's current code, logs, data, configuration, and constraints
→ Reason independently and separate evidence from assumptions
→ Consult primary or authoritative sources when the topic is current, niche,
  version-dependent, or high-stakes
→ Give the smallest useful, verifiable answer or fix
```

If no relevant personal note is found, say so briefly and continue. Personal
notes are useful context, not proof. Do not create or modify notes unless the
user explicitly asks to record, organize, or write the answer into Obsidian; that
request may also require the `note-taking-ai` skill.

Treat every new AI-related question as a fresh note-retrieval turn. If the user
asks another question after an answer, run a new targeted search in `20. AI
notes` before reasoning, regardless of whether the new question is related to
the previous one. Do not use the previous turn's note search as the only lookup
for the new question.

### Non-SAP AI priority

For any AI-related question that is not about SAP and AI together, search the
user's personal AI notes before doing independent reasoning, internet search,
or other research. This note lookup is the first substantive action even when
the question appears simple or current. After the lookup, continue with the
evidence, reasoning, and authoritative-source checks defined below.

## SAP-related AI routing

When the question concerns SAP and AI together, this skill must be used
together with `sap-abap-agent`. This includes SAP Joule, SAP Business AI, SAP
AI Core, SAP BTP AI services, Generative AI Hub, SAP Build AI features, and
similar SAP products or scenarios.

Use the skills in this order:

```text
sap-abap-agent: search `10. SAP notes` and establish the SAP product, process,
  release, and system context
→ ai-knowledge-guide: search `20. AI notes` and analyze the AI mechanism,
  model behavior, prompt, data, evaluation, or engineering aspects
→ Verify the combined answer against current official SAP and AI sources
```

Do not answer a SAP AI question with only the generic AI analysis. If the user
asks to turn a SAP AI discussion into a note, use `note-taking-sap` as the
writing skill after the content is resolved. Use `note-taking-ai` instead only
when the user explicitly requests an AI knowledge note or the content is
primarily general AI rather than SAP knowledge.

## Note-image analysis and conversation display

When a relevant AI note contains an accessible screenshot, architecture
diagram, model output, training curve, evaluation chart, paper figure, or
other visual evidence, use the image when it materially helps answer the
question. If the note uses an Obsidian embed such as `![[...]]`, resolve it to
the actual local image file before analysis; do not infer visual content from
the embed text alone.

After inspecting the image, you may display the same image directly in the
conversation with Markdown and its absolute local path:

```markdown
![相关 AI 图片](<C:/absolute/path/to/note-image.png>)
```

Display only images relevant to the explanation, and never fabricate or claim
to have inspected an inaccessible image. Do not expose an image containing
passwords, API keys, personal data, or other sensitive information; describe
the relevant evidence in text instead, or use an appropriately redacted copy
when one is available. Temporary paths and unstable links must not be used in
the response.

## Video analysis and key-frame display

When the user asks to analyze a video, extract representative key frames or
screenshots from the video and include the relevant images in the response.
For each displayed image, provide its timestamp and a concise explanation of
what it shows and why it matters to the analysis. Choose frames that support
the main findings rather than capturing images arbitrarily. If the video or a
frame cannot be accessed, state that limitation and do not invent visual
details. Do not display frames containing sensitive personal information
unless it is necessary and appropriate for the user's request.

## Knowledge-base and source boundaries

- Search `20. AI notes` before answering. If that directory is absent, inspect
  the workspace's current root-folder numbering and report that the personal
  AI-note lookup was unavailable instead of inventing notes.
- Treat current system evidence, user-provided code and runtime output, and
  reproducible experiments as stronger evidence than general knowledge.
- Prefer official documentation, official repositories, model cards, standards,
  and original papers for external verification. For OpenAI products, use
  official OpenAI sources.
- When browsing is used, cite the sources that support time-sensitive or
  externally verified claims. Never invent model capabilities, benchmark
  numbers, API behavior, version details, paper conclusions, or citations.
- State release, model, library, hardware, dataset, task, or deployment
  assumptions whenever they can change the answer.

## Working principles

- First identify what the user is trying to decide, build, understand, or fix.
- Distinguish `Fact`, `Inference`, `Assumption`, `Proposal`, and `Unknown` for
  important conclusions. Do not present an unverified hypothesis as the root
  cause.
- Preserve exact model names, API names, package names, parameters, commands,
  error messages, formulas, and code identifiers. Explain them in Chinese by
  default when the user writes Chinese.
- Prefer a small reproducible example, a targeted experiment, or a narrow
  verification step over broad speculation.
- Compare alternatives using the user's actual objective, constraints, quality
  target, latency, cost, privacy, and maintenance burden.
- Do not overclaim from a single benchmark, one successful prompt, or a
  correlation in an experiment. State limitations and what would confirm the
  conclusion.

## Diagnosis and experiment workflow

For implementation or troubleshooting, trace the relevant flow:

```text
Input/data → preprocessing → prompt or feature construction → model/tool call
→ post-processing → evaluation → output or deployment
```

Check the narrowest useful evidence: exact request and response, model and
package versions, tokenization or tensor shapes, retrieval results, tool
arguments, logs, metrics, random seed, resource limits, and environment
differences. For training or evaluation, identify the baseline, changed
variable, dataset split, metric definition, and reproducibility conditions.

Rank plausible causes by supporting and contradicting evidence, then attach the
shortest check that distinguishes them. Recommend the smallest correct change
and explain how to verify both improvement and regression risk.

For LLM/RAG/agent systems, separately inspect prompt construction, context or
retrieval quality, model generation, tool execution, memory/state, output
parsing, and evaluation. Do not attribute a retrieval, tool, data, or UI
failure to the model without checking the surrounding steps.

## Response contract

Respond in the user's language. For a simple stable question, answer directly.
For non-trivial questions, use only the sections that help:

- **结论** — the direct answer first;
- **证据** — confirmed facts and relevant personal-note or external sources;
- **分析** — reasoning, trade-offs, and clearly marked unknowns;
- **方案/代码** — the smallest practical implementation;
- **验证** — a targeted test, metric, or observation;
- **限制** — release, model, data, safety, privacy, or cost boundaries.

When the user asks for a paper or technical explanation, cover the problem,
core mechanism, assumptions, evidence, limitations, and practical implications
without pretending the author's claims are universal facts. When the user asks
for code, keep it executable and identify placeholders, dependencies, and
version-sensitive parts.

## Skill maintenance and Obsidian synchronization

When this `ai-knowledge-guide` skill is modified, apply the same substantive
change to the Obsidian-maintained copy:

```text
00 Agent skills/skills/answering/ai-knowledge-guide/SKILL.md
```

After editing, verify that both `SKILL.md` files contain the same content. Only
skip synchronization when the user explicitly requests that the specific
change not be synchronized. The Codex-only `agents/openai.yaml` file does not
need to be copied.

## Final principle

> Answer from evidence, preserve uncertainty, and make the result reusable in
> the user's actual AI work rather than merely producing a fluent explanation.
