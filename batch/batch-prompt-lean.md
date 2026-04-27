# career-ops Lean Scorer — Score-only, minimal tokens

Score a job posting for candidate Sashank Siwakoti. Be brief. No PDFs. No WebSearch. No STAR stories.

## Candidate (read cv.md for details)
- 7+ yrs data engineering: Fifth Third Bank (dbt, Snowflake, Spark), Kroger (PySpark, Redshift, Kafka, MLflow), Ncell, Intuji
- Target: Senior Data Engineer / Analytics Engineer
- Stack: Python, Scala, SQL, Snowflake, Redshift, Databricks, Spark, dbt, Kafka, MLflow, AWS, Azure
- Comp floor: $120K, target $150K–$200K
- Location: Cincinnati OH, open to relocation, prefers remote

## Steps

1. Read cv.md from project root
2. Fetch JD from {{URL}} using WebFetch (one attempt only — if it fails, score 0 and note "JD unavailable")
3. Score 1–5 on: CV match, role fit, comp (estimate from title/company if not listed), red flags
4. Write report to reports/{{REPORT_NUM}}-{company-slug}-{{DATE}}.md (compact format below)
5. Write TSV to batch/tracker-additions/{{ID}}.tsv

## Report format (keep it SHORT)

```
# {{REPORT_NUM}} — {Company}: {Role}
**Score:** X.X/5 | **URL:** {{URL}} | **Date:** {{DATE}}
**Verdict:** [Apply / Skip / Maybe]

### Match
[3–5 bullet points mapping JD requirements to CV — cite exact cv.md lines]

### Gaps
[1–3 gaps with severity: blocker / minor]

### Comp
[Estimated range if not listed. Does it clear $120K floor?]

### Red flags
[Any: repost, domain mismatch, comp too low, etc.]
```

## TSV format (9 tab-separated columns)
{next_num}\t{{DATE}}\t{Company}\t{Role}\tEvaluated\t{score}/5\t❌\t[{{REPORT_NUM}}](reports/{{REPORT_NUM}}-{slug}-{{DATE}}.md)\t{verdict + 1-line reason}

Where next_num = max # in data/applications.md + 1.

## Output (stdout)
```json
{"status":"completed","id":"{{ID}}","report_num":"{{REPORT_NUM}}","company":"{co}","role":"{role}","score":{n},"verdict":"{Apply|Skip|Maybe}","error":null}
```

## Rules
- NO WebSearch
- NO PDF generation
- NO STAR stories
- NO blocks C/E/F
- Keep entire report under 400 words
- If JD fetch fails: score null, verdict "Skip", note error
