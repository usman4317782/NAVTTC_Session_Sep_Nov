# n8n AI Automation — Practical Assessment
## Build: "The Fair-Shot Resume Screener" 🎯

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

A small remote-first startup, **"Northwind Labs,"** is hiring for a Junior Developer role and just opened applications publicly. Within two days they have 80+ submissions and no recruiter. The founder — overwhelmed — says:

> "I don't want an AI that rejects people. I want something that reads every application fairly, summarizes it in plain English, and tells me which ones clearly meet the *must-have* requirements — without me having to open 80 tabs."

You're building the **first-pass screener**: something that respects candidates (nobody gets silently auto-rejected without a human seeing a summary) while saving the founder hours of reading.

---

## 2. The Twist: Explainable Scoring, Not a Black Box

A screener that just outputs "Pass/Fail" is unfair and useless for a hiring context — nobody should trust a black-box rejection. Your workflow must make the AI **show its reasoning**: for every application, it must list *which specific requirements were met, which were not,* and *why* — before giving a recommendation. This "explainability" layer is exactly what real-world responsible-AI hiring tools are built around, and it's a strong differentiator to describe in an interview.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** with fields: `Candidate Name`, `Email`, `Years of Experience`, `Cover Letter / Summary` (free text), `Key Skills` (free text).

### Stage 2 — Requirement Matching (AI)
- Store the job's must-have requirements directly in a **Set node** (e.g., "2+ years JavaScript", "Git experience", "Can work async") so it's reusable.
- Use a **free LLM node** (Gemini free tier / OpenRouter free models / Hugging Face free tier) to compare the candidate's submission against the requirements list.
- Require structured JSON output:
  - `requirements_met`: array of strings
  - `requirements_missing`: array of strings
  - `match_score`: 0–100
  - `summary`: 2-sentence plain-English summary of the candidate

### Stage 3 — Explainability Check
- A **second AI call** (or extended prompt) must produce a `reasoning` field — one sentence justifying the `match_score`, referencing at least one specific requirement. This forces the model to ground its score instead of guessing.

### Stage 4 — Routing (never silent rejection)
- **IF node**: `match_score >= 70` → tagged `Recommend Interview`; otherwise → tagged `Needs Human Review` (never `Rejected` — a human always makes the final call).

### Stage 5 — Logging
- Log every candidate + all AI fields + final tag to **Google Sheets** or a local file via **Read/Write File** node.

### Stage 6 — Confirmation
- **Set/NoOp** node summarizing the outcome for that candidate.

---

## 4. Constraints

- **No paid tools.** n8n free trial + any free LLM API only.
- Max **10–12 nodes**.
- The workflow must **never produce a final "Rejected" status automatically** — this is a deliberate ethical design constraint, not an oversight. Explain this choice in your write-up.
- Must run successfully end-to-end at least once.

---

## 5. Step-by-Step Guidance

1. Set up the n8n free trial and get a free LLM API key (Google AI Studio recommended).
2. Build the Form Trigger with the 5 fields above.
3. Add a Set node hard-coding the job's 3–5 must-have requirements.
4. Build the AI matching prompt — be explicit that it must return valid JSON with the 5 fields listed in Stage 2/3.
5. Parse the response with a Structured Output Parser or Set node.
6. Add the IF node for routing.
7. Log to Google Sheets or a local file.
8. Add the closing Set/NoOp node.
9. Test with 3 candidates: one clearly strong, one clearly weak, one borderline — confirm the reasoning field actually references real requirements each time.
10. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png` — one full successful run
3. `writeup.md` (max 300 words):
   - Which free LLM did you use and why?
   - Show one example of the `reasoning` field output — does it actually justify the score?
   - Why does this workflow deliberately avoid an automatic "Rejected" status? What's the risk of removing that constraint?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| Requirement matching returns accurate, structured JSON | 25% |
| Reasoning/explainability field is genuinely grounded (not generic) | 20% |
| Routing logic respects the "no silent rejection" rule | 15% |
| Logging completeness | 10% |
| Write-up quality and ethical reasoning | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Hiring automation is a **real, high-demand freelance/agency niche** — companies pay well for tools that save recruiter time without creating legal or ethical risk.
- The explainability requirement teaches a genuinely important AI-automation skill: **forcing structured, grounded reasoning out of an LLM** instead of trusting a raw score.
- CV line: *"Built an explainable AI resume-screening workflow in n8n that scores candidates against job requirements with transparent, human-auditable reasoning — designed to support (not replace) human hiring decisions."*
- 100% free to build and keep.

---

*End of assessment.*
