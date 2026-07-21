# Dirty Hands GTM

**Tactical AI systems for go-to-market operators.**

---

## What This Is

An open-source framework and execution toolkit for building AI-powered GTM systems in Claude Code. Companion repo to the [Dirty Hands](https://dirtyhandsgtm.substack.com/) newsletter. Subscribe to Dirty Hands to get new Claude Code GTM walkthroughs and updates to the repo.

This is not a prompt library. It is a structured system with three layers:

1. **A knowledge foundation** -- a master knowledgebase that captures your positioning, ICP, personas, voice, and competitive landscape in one source of truth.
2. **A modular context architecture** -- derived files scoped from the master doc, each consumed by specific agents. No agent loads more than it needs.
3. **Executable skills** -- Claude Code skills that run real GTM workflows: extracting customer intelligence from sales calls, building research-backed content briefs, and publishing SEO articles through a multi-stage pipeline with human review gates.

The content pipeline is the first fully-built motion. More get added with each newsletter issue.

---

## Core Philosophy

### 1. One source of truth, modular consumption

You maintain a single master knowledgebase. Derived files (`icp.md`, `personas.md`, `positioning.md`, `voice-guide.md`, `competitive-landscape.md`) are scoped extracts. Agents consume only the modules they need -- never the full document.

### 2. Cascading updates

Edit the master knowledgebase. Run `sync-context`. All derived modules update. Every downstream agent's output changes. Maintain in one place, consume in many.

### 3. Tightly constrained agents

Each skill specifies exactly which context files it reads. The research agent reads ICP + competitive + customer intelligence. The writer reads voice + positioning + the approved outline. Tight context means better output, fewer tokens, and less drift.

### 4. Show what good looks like

Every directory includes example files from a fictional B2B SaaS company ("ComplianceOS" -- mid-market compliance automation). These are not placeholder stubs. They are fully written, realistic content that demonstrates the quality bar and the patterns you should follow.

### 5. The repo grows with the newsletter

The content pipeline is the first motion shipped. Each future Dirty Hands issue adds new skills and motions to the repo. Signal-based outbound, content repurposing, competitive monitoring -- each one lands here as executable code.

### 6. MCP integrations are optional enhancements

The core pipeline works with just Claude Code and local files. MCP servers (Firecrawl, Webflow, HubSpot, Clay) enhance specific skills when available. Skills detect whether MCP tools are present and adapt. If an MCP server is not connected, the skill continues without it and notes what you would gain by adding it.

---

## Repo Structure

```
dirty-hands-gtm/
├── README.md                            # You are here
├── CLAUDE.md                            # Onboarding agent -- loads when you open
│                                          Claude Code and guides setup
│
├── strategy/
│   ├── examples/
│   │   ├── knowledge-base.md            # MASTER: full knowledgebase (ComplianceOS)
│   │   ├── icp.md                       # DERIVED: firmographics, dream customer,
│   │   │                                  buying committee, external signals
│   │   ├── personas.md                  # DERIVED: per-persona buying psychology,
│   │   │                                  pain points, decision criteria, objections
│   │   ├── positioning.md               # DERIVED: narrative, differentiators, proof
│   │   ├── voice-guide.md               # DERIVED: tone, style, anti-patterns,
│   │   │                                  prohibited terms
│   │   └── competitive-landscape.md     # DERIVED: competitor mapping, battlecards
│   │
│   └── templates/
│       ├── knowledge-base-template.md   # Guided master doc (start here)
│       ├── icp-template.md              # Guided: firmographics, dream customer
│       ├── personas-template.md         # Guided: buying psychology, pain points
│       ├── positioning-template.md      # Guided: narrative, differentiators
│       ├── voice-guide-template.md      # Guided: tone, style rules
│       └── competitive-template.md      # Guided: competitor mapping
│
├── customer-intelligence/
│   ├── examples/
│   │   ├── sample-transcript.md         # Fictional sales call transcript
│   │   ├── sample-insights.json         # Call analyzer output (structured)
│   │   ├── sample-brief.json            # Research agent output (content brief)
│   │   └── sample-angles.json           # Thought leadership angle output
│   └── transcripts/                     # Drop your own transcripts here
│
├── proof-library/
│   ├── examples/
│   │   └── sample-case-study.md         # Case study with quantifiable metrics
│   └── case-studies/                    # Add your own
│
├── .claude/
│   ├── skills/
│   │   ├── setup-strategy/              # Walks through master knowledgebase creation
│   │   │   └── SKILL.md
│   │   ├── sync-context/                # Reads master, updates all derived modules
│   │   │   └── SKILL.md
│   │   ├── extract-insights/            # Call analyzer (Grow & Convert methodology)
│   │   │   └── SKILL.md
│   │   ├── research-brief/              # Research agent: topic backlog + briefs
│   │   │   └── SKILL.md
│   │   ├── seo-pipeline/                # 6-stage content pipeline with review gate
│   │   │   └── SKILL.md
│   │   ├── linkedin-insights/           # LinkedIn post insights from calls
│   │   │   └── SKILL.md
│   │   └── thought-leadership-angles/   # Contrarian patterns across calls
│   │       └── SKILL.md
│   │
│   └── rules/
│       └── writing-quality.md           # Global anti-slop rules
│
├── outputs/                             # Pipeline outputs land here
│   ├── articles/
│   ├── angles/                          # Created on first thought-leadership run
│   ├── seo-assets/
│   ├── linkedin/
│   └── briefs/
│
└── motions/                             # Future GTM motions (added per issue)
```

---

## Getting Started

**Prerequisites:** [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and configured.

### The guided path

1. Clone the repo:
   ```bash
   git clone https://github.com/benjamingibert/dirty-hands-gtm.git
   cd dirty-hands-gtm
   ```

2. Open Claude Code. The `CLAUDE.md` onboarding agent will detect your setup state and guide you through everything. It checks whether you have a knowledgebase, whether derived files exist, and suggests the right next step.

### The manual path

1. Start with `strategy/templates/knowledge-base-template.md` to build your master knowledgebase. Fill in your positioning, ICP, personas, voice rules, and competitive landscape.

2. Run `/setup-strategy` to create your knowledge foundation interactively. The skill walks you through each section, asks clarifying questions, and produces a complete `strategy/knowledge-base.md`.

3. Run `/sync-context` to derive module files. This reads your master knowledgebase and generates `icp.md`, `personas.md`, `positioning.md`, `voice-guide.md`, and `competitive-landscape.md` in the `strategy/` directory.

4. Drop sales call transcripts into `customer-intelligence/transcripts/`.

5. Run `/extract-insights` to analyze transcripts into structured intelligence (JTBD, pains, workflows, competitor mentions, customer lexicon).

6. Run `/thought-leadership-angles --min-calls 5` to surface contrarian patterns across calls for founder content, newsletter angles, and long-form thought leadership.

7. Run `/research-brief` to generate a prioritized topic backlog and detailed content briefs from your intelligence.

8. Run `/seo-pipeline` to execute the full content pipeline: enrichment, outline (with human review gate), writing, editing, internal linking, and publishing.

---

## Skill Context Consumption Map

Each skill loads only the context files it needs. This table shows exactly what each skill reads and why.

| Skill | Context Files Consumed | Why These Files |
|-------|----------------------|-----------------|
| `setup-strategy` | Templates only | Guides creation -- does not consume existing context |
| `sync-context` | `knowledge-base.md` --> all derived files | Reads master, diffs and updates modules |
| `extract-insights` | `icp.md`, `personas.md`, `competitive-landscape.md` | Classify buyer roles, tag by persona, map competitor mentions |
| `research-brief` | `icp.md`, `personas.md`, `competitive-landscape.md`, `customer-intelligence/` | Audience definition, pain mapping, competitive gaps, existing intelligence |
| `seo-pipeline` (enrichment) | `customer-intelligence/`, `proof-library/` | Mine evidence for brief sections |
| `seo-pipeline` (outline) | Enrichment output + original brief | Merge evidence into writer-ready spec |
| `seo-pipeline` (writer) | `voice-guide.md`, `positioning.md`, approved outline | Voice/tone, value props, outline carries evidence forward |
| `seo-pipeline` (editor) | `voice-guide.md` | Style enforcement only |
| `seo-pipeline` (linker) | Sitemap / URL inventory | Link placement only |
| `seo-pipeline` (publisher) | SEO assets YAML | Metadata for CMS creation |
| `linkedin-insights` | `personas.md`, `positioning.md` | Persona-specific framing, positioning themes |
| `thought-leadership-angles` | `personas.md`, `positioning.md`, `customer-intelligence/insights/` | Cross-call pattern extraction, buyer-perspective mapping, contrarian content angles |

---

## MCP Integrations

All optional. The core pipeline works without any of these.

| MCP Server | Enhances | What It Adds |
|-----------|----------|-------------|
| **Firecrawl** | `research-brief` | Automated SERP crawling and competitor content analysis before writing. Briefs informed by what is actually ranking. |
| **Webflow** | `seo-pipeline` (publisher) | Direct CMS draft creation. Markdown to HTML, FAQ schema injection, category detection, related article linking. |
| **HubSpot** | `research-brief` | Contact engagement data for topic prioritization. Which pain points correlate with closed deals? |
| **Clay** | `extract-insights` | Company enrichment from transcript mentions. Firmographic patterns across your customer base. |
| **Lemlist** | Outbound motions (future) | Load outbound sequences directly from extracted insights and persona segmentation. |
| **GA4 / Analytics** | `research-brief` | Article performance feedback loop. Which topics drive pipeline? Which briefs produce articles that rank? |

Skills detect MCP availability at runtime. If a server is not connected, the skill runs without it and notes what the integration would add.

---

## Future Motions

The `motions/` directory is where new GTM workflows land as the newsletter covers them. It now includes the Issue 2 fan-out branch from `/extract-insights` into `/thought-leadership-angles`, plus the reference patterns that make the motion architecture reusable. Planned:

- **Signal-based outbound** -- trigger-aware sequences from intent signals, job changes, and funding events
- **Content repurposing** -- newsletter to social atomization, long-form to short-form extraction
- **Customer intelligence extraction** -- systematic mining of calls, support tickets, and reviews into structured intelligence
- **Competitive monitoring** -- automated tracking of competitor positioning, pricing, and content changes

Each motion adds new skills, potentially new derived context modules, and updated consumption documentation.

---

## Links

- [Dirty Hands newsletter](https://dirtyhandsgtm.substack.com/) -- weekly deep-dives on tactical AI systems for GTM operators
- [Guest post on GTM Strategist](https://gtmstrategist.substack.com) -- the original walkthrough that introduced this framework

---

Built by [Ben Gibert](https://www.linkedin.com/in/benjamingibert/). The systems are real. The failures are included. The hype is not.
