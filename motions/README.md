# Motions

## Repeatable GTM Workflows

A **motion** is a repeatable GTM workflow with defined inputs, processing stages, quality gates, and outputs. Each motion is a self-contained pipeline that an operator can run end-to-end with AI agents.

## Architecture

Every motion follows the same structural pattern:

```
Inputs → Processing Stages → Quality Gates → Outputs
```

- **Inputs**: Raw materials the motion consumes (transcripts, research, signals, content)
- **Processing Stages**: Sequential agent tasks that transform inputs
- **Quality Gates**: Checkpoints where a human reviews before the pipeline continues
- **Outputs**: Finished deliverables ready for distribution or use

## Current Motions

### Content Pipeline (SEO Articles from Sales Calls)
The first fully built motion. Takes sales call transcripts through customer intelligence extraction, topic clustering, keyword research, article drafting, proof enrichment, and SEO optimization — producing publish-ready long-form content grounded in real customer language.

### Issue 2 Fan-Out Branch (Thought Leadership Angles)
Issue 2 of Dirty Hands, "Skills, Chains, and Compound Interest," adds a fan-out branch from `/extract-insights` into `/thought-leadership-angles`. The point is not another prompt. It is a reusable pattern: one expensive extraction step creates structured intelligence that multiple downstream skills can reuse at marginal cost.

## Issue Map

| Issue | Repo artifact | What shipped |
|---|---|---|
| Issue 1 | Content pipeline baseline | Core repo structure and first motion |
| Issue 2 | `/thought-leadership-angles` | Cross-call thought leadership extraction, sample angle output, and the seven transfer patterns reference |

## Seven Architectural Patterns

These are the transferable patterns documented in Issue 2 and embodied in the repo:

1. **Filename-based state machines** — pipeline progress encoded in filenames rather than external state.
2. **Human review gates** — explicit pause points at strategic inflection points.
3. **Scored outputs for downstream routing** — outputs include scores, not just content.
4. **Tiered evidence mining** — sources searched in priority order, stopping when enough proof is found.
5. **Approval queues** — draft states before anything reaches the outside world.
6. **Skill self-modification** — retrospectives feed general learnings back into the system.
7. **MCP tool selection guides** — explicit task-to-tool mappings reduce ambiguity as integrations grow.

## Fan-Out Pattern

```text
/extract-insights
  -> /research-brief
  -> /linkedin-insights
  -> /thought-leadership-angles
```

One structured extraction can support multiple downstream motions without re-processing raw transcripts. That is the compounding behavior Issue 2 is describing.

## Planned Motions

Each future Dirty Hands newsletter issue will introduce a new motion:

| Motion | Description |
|---|---|
| **Signal-Based Outbound** | n8n + Clay + Lemlist pipeline that detects buying signals and triggers personalized outbound sequences |
| **Content Repurposing** | Newsletter-to-social atomization — break long-form into LinkedIn posts, threads, and short-form variants |
| **Customer Intelligence Extraction** | Structured analysis of sales conversations at scale to surface patterns across your entire call library |
| **Competitive Monitoring** | Continuous tracking of competitor positioning, pricing, and messaging changes |

## Shared Knowledge Foundation

All motions draw from the same strategy layer (`strategy/knowledge-base.md` and its derived modules). This means:

- A new persona insight from customer intelligence automatically improves content targeting
- Updated competitive positioning flows into both outbound messaging and article differentiation
- Voice calibration applies consistently across every motion's output

Each motion may add new skills to `.claude/skills/` and potentially new derived context files to `strategy/`, but they all share the same knowledge foundation.

## Adding a Motion

New motions follow the pattern established by the content pipeline:
1. Define inputs, stages, gates, and outputs
2. Create skills in `.claude/skills/` for each processing stage
3. Add any new derived context files needed
4. Document the motion in this directory
