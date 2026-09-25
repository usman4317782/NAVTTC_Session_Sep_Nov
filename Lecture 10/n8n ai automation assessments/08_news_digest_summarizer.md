# n8n AI Automation — Practical Assessment
## Build: "The Signal-Not-Noise Digest" 📰

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only (real, free public RSS feeds, no paid news API)
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

A busy startup founder, **Amir**, follows 5+ industry blogs and news sources but never has time to read them. He's drowning in RSS clutter and skipping things that actually matter. He asks you:

> "I don't want a headline dump — I already get that from every app I've tried. I want a short digest that groups stories by topic, tells me the overall *sentiment* of the news (is this good or bad news for the industry?), and only surfaces genuinely new information, not the same story rehashed by five outlets."

You're building a **real RSS-to-AI-digest pipeline** using n8n's built-in **RSS Feed Trigger** — pulling actual live articles, no simulated data, entirely free.

---

## 2. The Twist: Deduplication Before Summarization

The single most annoying failure of naive "AI summarizes my RSS feed" tools is presenting the **same underlying story 3 times** because 3 outlets covered it. Your workflow must include a **deduplication step** — using AI to detect when multiple articles in the same batch are about the same underlying event — and merge them into a single digest entry before final summarization, rather than summarizing every article independently.

---

## 3. What You Must Build

### Stage 1 — Real Data Intake
- Use n8n's built-in **RSS Feed Read** node pointed at a real, free public RSS feed (e.g., a tech news feed like TechCrunch, Hacker News RSS, or any free feed of the candidate's choice relevant to a topic they pick).
- Limit to the **latest 8–10 items** per run.

### Stage 2 — Deduplication (AI)
- Send the batch of article titles + short descriptions to a **free LLM node**. Prompt it to group articles that cover the same underlying story, returning structured JSON:
  - `story_groups`: array of objects, each with `representative_title`, `related_titles` (array, may be empty), `topic_tag` (e.g., "AI", "Funding", "Product Launch", "Policy")

### Stage 3 — Summarization + Sentiment (AI, second pass)
- For each `story_group`, a **second AI call** (or looped call using n8n's **Split In Batches** node) produces:
  - `summary`: 2-sentence plain-English summary
  - `sentiment`: `"Positive" | "Neutral" | "Negative"` relative to the industry, with `sentiment_reason`: one sentence

### Stage 4 — Digest Assembly
- Use a **Code node** or **Set node** to assemble all summarized story groups into one clean digest document, organized by `topic_tag`.

### Stage 5 — Output
- Save the final digest as a dated Markdown file via **Read/Write File** node, or log each story group as a row in **Google Sheets**.

### Stage 6 — Confirmation
- **Set/NoOp** node confirming how many stories were processed and how many duplicate groups were merged.

---

## 4. Constraints

- **No paid tools/APIs.** Must use a genuinely free, public RSS feed via n8n's built-in RSS node — no paid news API.
- Must demonstrably **reduce article count through deduplication** — your test run should show at least one case of 2+ articles merging into 1 story group (if your chosen feed doesn't naturally have duplicates in one run, you may add 1–2 synthetic near-duplicate titles via a Set node before the AI step to prove the logic works — disclose this in your write-up).
- Max **10–12 nodes**.
- Must run end-to-end successfully at least once with real fetched RSS data.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Add the **RSS Feed Read** node pointed at a real feed URL (test a few free feeds to find one that returns clean data).
3. Limit/filter to the latest ~10 items using a Set/Filter node.
4. Build the deduplication prompt, requiring the `story_groups` JSON structure.
5. Parse the response.
6. Build the summarization + sentiment prompt, applied per story group (Split In Batches if looping).
7. Assemble the final digest with a Code/Set node.
8. Save to a Markdown file or Google Sheets.
9. Add closing Set/NoOp confirmation.
10. Run the workflow, confirm real articles were fetched and at least one dedup merge occurred (synthetic if needed).
11. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png`
3. `writeup.md` (max 300 words):
   - Which RSS feed and free LLM did you use?
   - Paste one example of a dedup merge — what were the original titles, and what became the merged `representative_title`?
   - What's one real limitation of using AI for sentiment on news headlines, and how would you address it in production?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors, using real RSS data | 20% |
| Deduplication step correctly groups related stories | 25% |
| Summarization + sentiment output is accurate and well-structured | 20% |
| Final digest is clean, organized by topic, and readable | 15% |
| Logging/file output completeness | 10% |
| Write-up quality | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- This is the **only assessment in this set using a real live external data source** (RSS) rather than simulated form input — a genuinely different and valuable n8n skill: working with real, unpredictable data.
- The deduplication-before-summarization pattern is exactly what separates a **usable digest tool from a spammy newsletter generator** — a real product differentiator.
- CV line: *"Built a real-time RSS news digest automation in n8n that deduplicates overlapping coverage via AI before generating topic-grouped, sentiment-tagged summaries — reducing reading time without losing signal."*
- Entirely free — uses public RSS feeds and free-tier LLM access only.

---

*End of assessment.*
