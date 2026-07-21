# Thought Leadership Angles

Extracts contrarian, pattern-based thought leadership angles from accumulated customer intelligence.

## Trigger

User invokes `/thought-leadership-angles` with optional flags or filters as arguments.

## Context Consumed

- `strategy/personas.md` -- map patterns to specific buyer perspectives
- `strategy/positioning.md` -- align angles to positioning themes and differentiators
- `customer-intelligence/insights/*.json` -- structured intelligence from prior `/extract-insights` runs

Does NOT read: `strategy/icp.md`, `strategy/voice-guide.md`, `strategy/competitive-landscape.md`, `strategy/knowledge-base.md`, transcripts, or proof-library files.

## Input

- No required file argument. The skill reads all available files in `customer-intelligence/insights/`.
- Optional `$ARGUMENTS`:
  - `--min-calls 5` -- minimum number of supporting calls required for a pattern to qualify
  - a persona or theme filter, such as `compliance`, `security`, or `comparison`

If `--min-calls` is not provided, default to `5`.

If no insight files exist, stop and tell the user: "No customer intelligence found. Run /extract-insights on your sales call transcripts first, or drop insight JSON files into customer-intelligence/insights/."

## Output

- `outputs/angles/[date]-angles.json` -- scored angle set across all eligible calls
- If the `outputs/angles/` directory does not exist, create it.

## Workflow

### Step 1: Load context

Read these files (skip any that do not exist, but warn):
1. `strategy/personas.md`
2. `strategy/positioning.md`

### Step 2: Load intelligence

1. Read all `.json` files in `customer-intelligence/insights/`.
2. Parse the structured fields that are most useful for pattern finding:
   - pains
   - quotes
   - workflow reality
   - alternatives and competitors
   - lexicon
   - keyword candidates
3. Apply any user-supplied persona or theme filter.

### Step 3: Identify candidate patterns

Look for recurring signals across calls in these four pattern types:

1. **Conventional wisdom violations**
   - Customer reality contradicts accepted market advice or category messaging.
2. **Impossible tradeoffs**
   - Buyers describe resource, budget, staffing, or workflow constraints that force ugly compromises.
3. **Deviant language**
   - Buyers use repeated terms or frames that do not match vendor or category language.
4. **Private/public divergence**
   - What buyers admit in calls differs from what their companies or the market say publicly.

For each candidate pattern, collect:
- supporting calls
- supporting quotes
- primary persona
- positioning theme
- suggested content formats

### Step 4: Apply qualification gates

Reject any candidate that fails one of these gates:

- **Evidence gate:** must be supported by at least `min_calls` distinct call files
- **Novelty gate:** cannot be a generic restatement of common pain
- **Persona gate:** must map cleanly to a persona or buying role
- **Tension gate:** must contain a clear contrast between the accepted narrative and ground truth

If a candidate is heavily driven by one company or one narrow vertical, flag it as weak or reject it.

### Step 5: Score angles

For each surviving angle, score on these dimensions:

| Dimension | Range | What It Measures |
|-----------|-------|------------------|
| Novelty | 0-10 | How surprising or non-obvious the pattern is |
| Tension | 0-10 | How sharp the conflict is between narrative and reality |
| Evidence strength | 0-10 | How well the pattern is supported across calls |
| Persona fit | 0-10 | How clearly it maps to a specific buyer perspective |
| Content usefulness | 0-10 | How usable it is for LinkedIn posts, newsletter essays, or long-form thought leadership |

Calculate a weighted total:

`weighted_total = (novelty * 0.30) + (tension * 0.25) + (evidence_strength * 0.20) + (persona_fit * 0.15) + (content_usefulness * 0.10)`

Sort angles by `weighted_total` descending.

### Step 6: Write output

Write `outputs/angles/[date]-angles.json` using this structure:

```json
{
  "generated_date": "ISO date",
  "min_calls": 5,
  "source_files": ["list of insight files consumed"],
  "filter_applied": "string or null",
  "angles": [
    {
      "pattern": "conventional_wisdom_violation | impossible_tradeoff | deviant_language | private_public_divergence",
      "title": "string",
      "tension": {
        "accepted_narrative": "string",
        "ground_truth": "string"
      },
      "evidence_calls": 0,
      "supporting_quotes": [
        {
          "quote": "string",
          "speaker_role": "string",
          "source_file": "string"
        }
      ],
      "scores": {
        "novelty": 0,
        "tension": 0,
        "evidence_strength": 0,
        "persona_fit": 0,
        "content_usefulness": 0,
        "weighted_total": 0
      },
      "primary_persona": "string",
      "positioning_theme": "string",
      "suggested_formats": ["linkedin_post", "newsletter_section", "long_form_article"],
      "hook_suggestion": "string"
    }
  ]
}
```

### Step 7: Report

Print a summary:
- Number of insight files consumed
- Minimum-calls threshold used
- Number of qualified angles generated
- Top 3 angles with pattern type, title, primary persona, and weighted score
- Output file path
- Reminder: "Review the angle set before publishing. Small-sample patterns can still look stronger than they are."
