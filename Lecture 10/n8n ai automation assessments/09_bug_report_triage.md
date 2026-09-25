# n8n AI Automation — Practical Assessment
## Build: "The Duplicate-Killer Bug Triage System" 🐛

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

**"DevFlow,"** a small dev tool startup, gets bug reports through a simple form, and the tiny 2-person engineering team is tired of two problems: (1) reports with almost no useful detail ("it's broken"), and (2) the same bug reported 5 different times by 5 different users in slightly different words, wasting triage time. The lead engineer says:

> "I need two things: tell me if a report is actually detailed enough to act on, and check it against bugs we already have logged so I'm not re-triaging the same issue for the tenth time."

You're building a **bug intake system with quality-checking and duplicate detection against an existing bug log** — a real internal tool pattern used by every engineering team with a public-facing bug tracker.

---

## 2. The Twist: Matching Against Existing Data, Not Just Classifying New Input

Every other "classify the incoming request" pattern only looks at *one* new submission. This assessment requires your AI step to **compare the new bug report against a small existing log of already-known bugs** (which you seed yourself) and determine if it's a likely duplicate — a genuinely harder and more valuable pattern: **retrieval-style reasoning**, not just single-item classification.

---

## 3. What You Must Build

### Stage 0 — Seed Data
- Before building the live flow, create a small **"Known Bugs" Google Sheet or local file** with 4–5 fictional but realistic existing bug entries (e.g., `BUG-101: Export button does nothing on Safari`, `BUG-102: Dark mode toggle resets on page refresh`, etc.) — each with an ID, title, and short description.

### Stage 1 — Intake
- **n8n Form Trigger** with fields: `Reporter Email`, `Bug Title`, `Steps to Reproduce`, `Expected vs Actual Behavior`.

### Stage 2 — Quality Check (AI)
- **Free LLM node #1.** Evaluate whether the report has enough detail to be actionable. Return structured JSON:
  - `is_actionable`: `true`/`false`
  - `missing_info`: array of strings (e.g., `"No steps to reproduce"`, `"Browser/device not specified"`) — empty array if fully actionable

### Stage 3 — Retrieve Known Bugs
- Use a **Google Sheets (Read)** node or **Read File** node to pull your seeded "Known Bugs" list into the workflow.

### Stage 4 — Duplicate Check (AI, second pass)
- **Free LLM node #2.** Pass both the new report AND the full known-bugs list. Prompt it to return:
  - `is_likely_duplicate`: `true`/`false`
  - `matched_bug_id`: string (the ID if matched, or `"none"`)
  - `match_reason`: one sentence explaining the match (or non-match)

### Stage 5 — Combined Routing
- **Switch node** with branches:
  - `is_actionable == false` → **"Needs More Info"**
  - `is_actionable == true AND is_likely_duplicate == true` → **"Merged — Duplicate of [ID]"**
  - `is_actionable == true AND is_likely_duplicate == false` → **"New — Ready to Triage"**

### Stage 6 — Logging
- Log every incoming report + both AI outputs + final routing status to a **"New Reports" Google Sheet** or local file.

### Stage 7 — Confirmation
- **Set/NoOp** node confirming the final status.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- Must genuinely **read from a seeded existing dataset** (Stage 3) — this is not optional; the duplicate check must reference real stored data, not just the single incoming report.
- Max **11–13 nodes** (slightly higher cap due to the extra retrieval stage).
- Must test with **at least one deliberate duplicate** (a new report clearly describing the same issue as one of your seeded bugs, worded differently) and confirm it's correctly matched.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Create your seeded "Known Bugs" sheet/file with 4–5 entries (Stage 0) — do this first, outside the live workflow.
3. Build the Form Trigger with the 4 intake fields.
4. Build the quality-check AI prompt (Stage 2).
5. Add the node to read your Known Bugs list (Stage 3).
6. Build the duplicate-check AI prompt, passing both the new report and full known-bugs list as context (Stage 4).
7. Add the Switch node for 3-way routing (Stage 5).
8. Log to a "New Reports" sheet/file (Stage 6).
9. Add closing Set/NoOp confirmation (Stage 7).
10. Test with 3 cases: a vague low-detail report, a detailed genuinely-new report, and a detailed report that's a reworded duplicate of a seeded bug. Confirm all 3 route correctly.
11. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png` — including the duplicate-match test case
3. `writeup.md` (max 300 words):
   - Which free LLM did you use?
   - Paste your seeded Known Bugs list and your deliberate duplicate test report — did the AI correctly match it and to which ID?
   - What would break this approach at scale (e.g., 500 known bugs instead of 5), and how would you fix it in a real production system?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 15% |
| Quality check correctly identifies actionable vs. incomplete reports | 20% |
| Duplicate check correctly reads and reasons over seeded existing data | 25% |
| Deliberate duplicate test case is correctly matched | 15% |
| 3-way routing and logging are correct and complete | 15% |
| Write-up quality, including scaling discussion | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- This is the only assessment in the set that requires **reasoning against an existing stored dataset** rather than just the current input — a direct, simplified introduction to the **retrieval-augmented reasoning** pattern that underlies real-world RAG systems, without needing a vector database or paid tools.
- Bug triage automation is a genuine internal-tooling need at any dev-focused company — a strong, specific portfolio piece for anyone targeting DevTools/SaaS clients.
- CV line: *"Built an AI bug-triage workflow in n8n that checks report completeness and cross-references new submissions against an existing bug log to detect duplicates — reducing redundant engineering triage time."*
- The scaling discussion in the write-up also shows the candidate understands the **limits** of this simple approach, which is a sign of real engineering maturity.
- Entirely free to build and keep.

---

*End of assessment.*
