# n8n AI Automation — Practical Assessment
## Build: "The Community Guardrail" 🛡️

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

**"ForumHive"** is a small online community (think a niche subreddit-style forum) with about 2,000 active members and zero moderation budget. The one volunteer moderator is burning out reading every post manually. She tells you:

> "I don't need something that deletes posts — that's too risky and I don't trust a black box with that. I need something that reads every new post, tells me how severe any problem is, and only pings me directly for the genuinely bad stuff. Everything else I can review at my own pace."

You're building a **tiered content moderation pipeline** — a real pattern used by every major platform, scaled down to something buildable in 90 minutes with free tools.

---

## 2. The Twist: Severity Tiers, Not Binary Flagging

A binary "flag / don't flag" system is what beginners build — and it's not useful in practice, because it treats a typo-filled rant the same as a genuine threat. Your workflow must classify content into **at least 3 severity tiers** with **different handling per tier**, mimicking real trust & safety systems:

- **Tier 1 — Clean:** no action, just logged.
- **Tier 2 — Borderline:** logged with a note, added to a "review when you have time" queue.
- **Tier 3 — Severe:** logged as urgent AND routed to a distinct "needs immediate attention" output.

This tiered design is exactly what separates a toy filter from a genuinely deployable moderation tool.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** simulating a new forum post: `Username`, `Post Title`, `Post Body`.

### Stage 2 — AI Classification
- Use a **free LLM node** to analyze the post. Require structured JSON:
  - `severity`: `Clean` | `Borderline` | `Severe`
  - `categories`: array of applicable tags (e.g., `spam`, `harassment`, `off-topic`, `hate-speech`, `none`)
  - `confidence`: 0–100
  - `explanation`: one sentence justifying the severity rating

### Stage 3 — Confidence Safety Check
- **IF node**: if `confidence < 60`, override the routing to **Borderline** regardless of what the model said — low-confidence AI judgments on moderation should never be treated as certain. This is a deliberate safety design choice you must implement, not skip.

### Stage 4 — Tiered Routing
- **Switch node** with 3 branches (Clean / Borderline / Severe) based on the (possibly overridden) severity.
- Each branch should produce a visibly different logged status.

### Stage 5 — Logging
- Log every post + AI output + final tier to **Google Sheets** or a local file, with Severe items clearly distinguishable (e.g., a separate sheet tab, or a `URGENT_` filename prefix if using files).

### Stage 6 — Confirmation
- **Set/NoOp** node summarizing the action taken.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- Must implement the **confidence override rule** in Stage 3 — this is graded specifically.
- Max **10–12 nodes**.
- Workflow must **never auto-delete or auto-ban** — it only classifies, logs, and routes for human action. State this explicitly in your write-up as a deliberate design boundary.
- Must run end-to-end successfully with at least 3 test posts covering all 3 tiers.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the 3 post fields.
3. Write the AI classification prompt, being explicit about the 3-tier system and required JSON fields.
4. Parse the AI response.
5. Add the confidence-override IF node.
6. Add the Switch node for 3-way routing.
7. Log to Google Sheets (recommend 3 tabs or a `tier` column) or local files.
8. Add closing Set/NoOp confirmation.
9. Test with: one clearly clean post, one mildly rude/off-topic post, and one clearly severe post (you can write a synthetic example — don't use real harmful content). Confirm all 3 route correctly.
10. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png` — showing at least one run through each of the 3 tiers (3 screenshots or one combined log view is fine)
3. `writeup.md` (max 300 words):
   - Which free LLM did you use?
   - Describe a case where your confidence-override rule actually changed the outcome (or explain why it didn't trigger in your tests).
   - Why is "never auto-delete" an important design boundary for a moderation tool built by a freelancer for a small client?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| AI classification returns accurate, structured severity + categories | 20% |
| Confidence-override safety rule correctly implemented | 20% |
| 3-tier routing works and is clearly distinguishable in logs | 20% |
| Logging completeness and clarity | 10% |
| Write-up quality and safety reasoning | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Trust & safety / content moderation tooling is a **real, well-paid automation niche** for small platforms, Discord servers, and online communities that can't afford enterprise moderation tools.
- The confidence-override requirement teaches a genuinely important AI-safety engineering pattern: **never fully trust a single model output for consequential decisions** — a concept that applies far beyond moderation.
- CV line: *"Built a tiered AI content-moderation pipeline in n8n with confidence-based safety overrides — routing severe content for urgent human review while auto-logging low-risk content, without any autonomous delete/ban actions."*
- Fully buildable and keepable at zero cost.

---

*End of assessment.*
