# n8n AI Automation — Practical Assessment
## Build: "The Global Feedback Funnel" 🌍

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

**"TravelNest,"** a small vacation-rental platform, just expanded into 4 new countries and now receives guest feedback in English, Spanish, French, and German — but the entire 3-person support team only reads English. Feedback in other languages currently gets ignored or badly mistranslated by guesswork. The ops lead says:

> "I don't need someone to build me a translation app — Google Translate already exists. I need something that translates the feedback *and* tells me instantly if it's a serious complaint that needs urgent action, regardless of what language it came in. Language shouldn't be why we miss a five-alarm problem."

You're building a **multilingual intake and urgency-routing system** — proving that language of origin never determines whether a real problem gets seen.

---

## 2. The Twist: Sentiment/Urgency Must Be Judged on the *Translation*, Not Assumed From the Source

A naive build might translate the text and separately guess urgency from surface cues (like exclamation marks) without deeply understanding the translated content. Your workflow must **explicitly translate first, then run sentiment/urgency analysis on the English translation as a distinct step**, and your write-up must show one example where the original non-English phrasing might have looked mild but the meaning was actually serious (or vice versa) — proving the pipeline isn't just keyword-matching.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** with fields: `Guest Name`, `Property ID`, `Feedback Text` (free text, any language), `Language` (dropdown: English / Spanish / French / German / Other — self-reported by the guest, may sometimes be wrong, which your workflow should handle gracefully).

### Stage 2 — Translation (AI)
- **Free LLM node #1.** Translate `Feedback Text` into English regardless of the stated `Language` field (don't just trust the dropdown — have the AI detect the actual language too). Return structured JSON:
  - `detected_language`: string
  - `english_translation`: string
  - `language_mismatch`: `true`/`false` (true if `detected_language` doesn't match the form's `Language` field)

### Stage 3 — Urgency & Sentiment Analysis (AI, second pass, on the translation)
- **Free LLM node #2**, operating **only on `english_translation`**, not the original text. Return:
  - `sentiment`: `"Positive" | "Neutral" | "Negative"`
  - `urgency`: `"Low" | "Medium" | "Urgent — Safety/Legal/Health Concern"`
  - `key_issue`: one sentence summarizing the core point, in English

### Stage 4 — Routing
- **IF/Switch node**: `urgency == "Urgent..."` → **"Immediate Escalation"** path; everything else → **"Standard Queue"** path, further split by sentiment for reporting purposes.

### Stage 5 — Logging
- Log guest info + original text + detected language + translation + sentiment + urgency + routing outcome to **Google Sheets** or a local file. Include the `language_mismatch` flag as its own column.

### Stage 6 — Confirmation
- **Set/NoOp** node confirming the routing outcome, printed in English regardless of input language.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only (the LLM itself performs translation; no separate paid translation API needed).
- Urgency/sentiment analysis must run **on the English translation as a separate AI call**, never directly on non-English source text — this is specifically graded.
- Max **10–12 nodes**.
- Must test with **at least 2 different non-English inputs** (you may write these yourself, e.g., in Spanish and French) — including at least one that is urgent (e.g., a safety concern) to confirm it's not missed due to language.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the 4 fields.
3. Write 2–3 test feedback samples in different languages yourself (a search engine translation is fine for creating realistic test input).
4. Build the translation + language-detection prompt (Stage 2).
5. Parse the response.
6. Build the urgency/sentiment prompt, explicitly operating on `english_translation` only (Stage 3).
7. Add the IF/Switch node for routing (Stage 4).
8. Log to Google Sheets or a local file, including the `language_mismatch` flag (Stage 5).
9. Add closing Set/NoOp confirmation (Stage 6).
10. Run all test cases and confirm the urgent non-English case is correctly escalated.
11. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png` — including your urgent non-English test case
3. `writeup.md` (max 300 words):
   - Which free LLM did you use, and does it genuinely support multilingual input reliably?
   - Show your urgent-in-another-language test case and confirm it was correctly escalated. Explain why running urgency analysis on the translation (not the raw source) matters here.
   - What would you add for a real production version handling 10+ languages and higher volume?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| Translation + language detection accurate and structured correctly | 20% |
| Urgency/sentiment correctly analyzed on the translated text as a separate step | 20% |
| Urgent non-English test case correctly escalated | 20% |
| Logging completeness, including language_mismatch flag | 10% |
| Write-up quality | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Multilingual support intake is a **real, common gap** for any small company scaling internationally without budget for a multilingual support team — a genuinely sellable automation.
- The "translate first, analyze second, as distinct steps" requirement teaches a subtle but important AI pipeline design lesson: **don't conflate translation quality with understanding quality** — treating them as separate, chainable AI operations is a transferable pattern for any multi-step LLM pipeline.
- CV line: *"Built a multilingual guest-feedback automation in n8n that translates and independently analyzes sentiment/urgency in real time — ensuring safety-critical complaints are escalated regardless of the language they were submitted in."*
- Entirely free — the LLM itself handles translation, no separate paid translation API required.

---

*End of assessment.*
