# n8n AI Automation — Practical Assessment
## Build: "The Weekly Money Mirror" 💸

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

Your friend **Sara** runs a tiny freelance design business and hates budgeting. She manually logs expenses in a messy note app but never looks back at them. She asks you:

> "Can you build me something that takes my raw expense entries and turns them into a plain-English summary each week — what I spent on, whether anything looks unusual, and one honest tip? I don't want a finance app. I want something that actually talks to me."

You're building a **personal finance digest generator** — a genuinely useful tool that real freelancers/solo founders would pay for, built entirely on free infrastructure.

---

## 2. The Twist: Anomaly Awareness, Not Just Totals

Any spreadsheet can sum numbers. What makes this worth building is that the AI must **compare the current batch of expenses against typical categories** and flag anything that looks like an **outlier** (e.g., a category spending 2x+ its usual pattern, or a single transaction unusually large relative to the rest). This requires the AI to reason across a *set* of entries, not just describe one — a meaningfully harder and more useful skill than single-item classification.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** simulating a batch expense submission. Since forms handle one submission at a time, use a **multiline text field** called `Expenses` where the user pastes several lines at once, e.g.:
  ```
  2026-09-20, Software subscription, 45
  2026-09-21, Client lunch, 120
  2026-09-22, Office supplies, 15
  2026-09-23, Software subscription, 45
  2026-09-24, Client lunch, 300
  ```

### Stage 2 — Parsing
- Use a **Code node** (JavaScript, free/built-in) to parse the multiline text into a structured array of `{ date, category, amount }` objects. This is your non-AI data-wrangling step — a core n8n skill.

### Stage 3 — AI Analysis
- Send the parsed array to a **free LLM node**. Prompt it to return structured JSON:
  - `total_spent`: number
  - `by_category`: object mapping category → total
  - `anomalies`: array of objects `{ entry, reason }` for anything unusual
  - `digest`: a friendly 3–4 sentence plain-English weekly summary, written in a warm, non-judgmental tone
  - `one_tip`: a single practical, specific suggestion

### Stage 4 — Formatting
- Use a **Set node** to assemble a clean final report combining the digest, tip, and anomaly list into one readable text block.

### Stage 5 — Delivery / Logging
- Log the full digest + raw data to **Google Sheets** (one row per week) or write it to a local `.txt`/`.md` file via **Read/Write File** node, formatted like a real weekly report.

### Stage 6 — Confirmation
- **Set/NoOp** node confirming the digest was generated and where it was saved.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- Must include a **Code node** for the parsing step (this is a required skill check, not optional).
- Max **9–11 nodes**.
- Must run end-to-end successfully at least once with at least 5 sample expense lines, including at least one deliberate anomaly.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the multiline `Expenses` text field.
3. Write a Code node to split lines by `\n`, then by `,`, producing a clean JS array.
4. Build the AI prompt — pass the parsed array as context, require the 5 structured fields above.
5. Parse the AI's JSON response.
6. Assemble the final formatted report with a Set node.
7. Log/save via Google Sheets or Read/Write File.
8. Add closing Set/NoOp confirmation.
9. Test with a sample batch that includes one obvious anomaly (e.g., a category spiking 2–3x) and confirm the AI actually catches it.
10. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png`
3. `writeup.md` (max 300 words):
   - What logic did your Code node use to parse the raw text?
   - Paste the AI's `anomalies` output from your test run — did it correctly catch your planted anomaly?
   - What would you add if this ran automatically every Sunday against a real bank export?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| Code node correctly parses multiline input into structured data | 20% |
| AI analysis returns accurate totals, categories, and digest | 20% |
| Anomaly detection correctly identifies the planted outlier | 20% |
| Logging/report formatting is clean and readable | 10% |
| Write-up quality | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Combines **AI reasoning over a dataset** (not just single-item classification) with a **hand-written parsing step** — a core, transferable n8n skill (Code nodes) that many tutorials skip.
- Personal finance / expense digest tools are a real micro-SaaS category — this is a legitimate proof-of-concept for a sellable product.
- CV line: *"Built an AI-powered financial digest automation in n8n that parses raw expense data, detects spending anomalies, and generates a natural-language weekly summary."*
- Entirely free to build, test, and keep.

---

*End of assessment.*
