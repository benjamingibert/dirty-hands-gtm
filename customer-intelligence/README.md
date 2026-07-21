# Customer Intelligence

## Building Your Content Foundation from Sales Conversations

The customer intelligence layer turns raw sales call transcripts into structured insights that feed every downstream motion — content, outbound, positioning refinement.

## Workflow

### 1. Drop Transcripts

Place sales call transcripts into `transcripts/` as markdown or plain text files. Name them descriptively:

```
transcripts/2026-04-15-acme-corp-discovery.md
transcripts/2026-04-18-globex-demo-followup.txt
```

Any format works. Fathom exports, Gong transcripts, manual notes — the extraction pipeline handles all of them.

### 2. Run Extraction

Run `/extract-insights` to process new transcripts. The skill reads each transcript and produces structured JSON output capturing:

- Pain points and challenges (verbatim language)
- Buying triggers and timing signals
- Objections raised and how they were handled
- Competitive mentions and comparisons
- Feature requests and use case descriptions
- Emotional language and urgency indicators

### 3. Insights Accumulate

Extracted insights land in `insights/` as structured JSON files, one per transcript. Over time, this directory becomes your richest source of customer voice data.

```
insights/2026-04-15-acme-corp-discovery.json
insights/2026-04-18-globex-demo-followup.json
```

### 4. Pattern Recognition

The real value compounds. Systematic analysis across all calls surfaces patterns that no single conversation reveals:

- Which pain points appear in 80% of discovery calls
- What language buyers actually use (vs. what marketing assumes)
- Which objections repeat and which are edge cases
- How different personas describe the same problem differently

These patterns flow upstream to refine your ICP definition, sharpen persona profiles, and calibrate positioning in the strategy layer.

They also flow sideways into downstream skills:
- `/linkedin-insights` turns single-call intelligence into post drafts
- `/thought-leadership-angles --min-calls 5` turns accumulated insight files into contrarian cross-call patterns for founder content and newsletter writing

## Reference

- **`examples/`** — Sample extraction output showing the expected structure and level of detail.
- **`examples/sample-angles.json`** — Reference shape for cross-call angle output.
- **`transcripts/`** — Drop your raw transcripts here.
- **`insights/`** — Structured extractions accumulate here over time.
