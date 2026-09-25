# n8n AI Automation — Practical Assessment
## Build: "The Lead Sorter" 📈

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

**"BrightPath Consulting,"** a 3-person B2B consultancy, gets contact-form inquiries from their website. Most are genuinely low-quality (students doing research, spam, people asking totally unrelated questions), but a few are real potential clients. Right now the founder personally reads all of them, which means real leads sometimes wait days for a reply while she wades through noise. She says:

> "I want something that reads every inquiry and tells me, in the language salespeople actually use, whether this is worth my time — and why. Not just a score. I need to know what makes it a good or bad lead so I trust the system."

You're building a **BANT-style lead qualification bot** — Budget, Authority, Need, Timeline — a real framework used by actual sales teams, automated with AI.

---

## 2. The Twist: Framework-Grounded Scoring (No Vibes-Based Scores)

A lead score that's just "AI vibes, 1–100" is not trustworthy to a real salesperson. Your workflow must force the AI to **score against the 4 specific BANT dimensions separately**, each with its own short justification, and only *then* compute an overall recommendation — making the reasoning auditable dimension-by-dimension rather than one opaque number.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** with fields: `Full Name`, `Company`, `Email`, `Inquiry Message` (free text — the actual contact-form message).

### Stage 2 — BANT Analysis (AI)
- **Free LLM node.** Prompt it to analyze the inquiry against the 4 BANT dimensions and return structured JSON:
  - `budget_signal`: `"Strong" | "Weak" | "None mentioned"` + `budget_reason`: string
  - `authority_signal`: `"Decision-maker" | "Unclear" | "Likely not decision-maker"` + `authority_reason`: string
  - `need_signal`: `"Clear pain point" | "Vague interest" | "No real need expressed"` + `need_reason`: string
  - `timeline_signal`: `"Urgent" | "Some timeline mentioned" | "No timeline"` + `timeline_reason`: string

### Stage 3 — Score Computation (Code node, not AI)
- Use a **Code node** (JavaScript) to convert the 4 categorical signals into a numeric score using a fixed, transparent point system you define (e.g., Strong/Decision-maker/Clear/Urgent = 3 points each, middle tier = 1–2 points, weakest tier = 0 points). This is a deliberate design choice: **scoring math should be deterministic code, not another AI guess** — this is exactly how real hybrid AI+logic systems are built.

### Stage 4 — Routing
- **IF/Switch node** based on the computed score: `High Priority Lead` (e.g., 8+), `Nurture — Follow Up Later` (4–7), `Low Priority` (0–3).

### Stage 5 — Logging
- Log the lead + all 4 BANT signals/reasons + computed score + final tier to **Google Sheets** or a local file.

### Stage 6 — Confirmation
- **Set/NoOp** node confirming the routed outcome.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- The **scoring math must happen in a Code node, not inside the AI prompt** — this is a specific, graded architectural requirement.
- Max **10–12 nodes**.
- Must test with at least 3 inquiries spanning all 3 priority tiers.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the 4 fields.
3. Build the BANT analysis prompt, being explicit about the 4-dimension structured JSON output.
4. Parse the AI response.
5. Write the Code node implementing your fixed point system, converting categorical signals to a numeric score.
6. Add the IF/Switch node for 3-tier routing.
7. Log to Google Sheets or a local file.
8. Add closing Set/NoOp confirmation.
9. Test with 3 inquiries you write yourself: one obviously strong lead, one obviously weak/spam, one ambiguous. Confirm correct tiering.
10. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png`
3. `writeup.md` (max 300 words):
   - Which free LLM did you use?
   - Explain your point system from the Code node — show the actual code snippet.
   - Why is it better to compute the final score in code rather than asking the AI to output a single number directly?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| BANT analysis returns accurate, well-justified structured signals | 25% |
| Score computation correctly implemented in a Code node | 20% |
| 3-tier routing works correctly across test cases | 15% |
| Logging completeness | 10% |
| Write-up quality and architectural reasoning | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Lead qualification automation is one of the **highest-demand freelance n8n use cases** — small sales teams and consultancies actively pay for this.
- The "score in code, not in the prompt" constraint teaches a genuinely important hybrid-architecture lesson: **use AI for judgment/extraction, use deterministic code for math** — a pattern that shows real engineering maturity, not just prompt-writing.
- CV line: *"Built a BANT-based AI lead-qualification workflow in n8n combining LLM-driven signal extraction with a deterministic scoring engine — giving sales teams auditable, dimension-by-dimension lead prioritization instead of an opaque single score."*
- Entirely free to build, test, and keep.

---

*End of assessment.*
