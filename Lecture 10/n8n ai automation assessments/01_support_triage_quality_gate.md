# n8n AI Automation — Practical Assessment
## Build: "The AI Support Triage Agent" 🤖

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — no paid tools, APIs, or subscriptions required
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

You've just landed your first freelance automation gig. Your client, **"QuickDesk"**, is a scrappy 5-person SaaS startup drowning in support emails. Every message currently lands in one inbox, and a human has to read it, figure out if it's urgent, decide what kind of issue it is, write a reply, and log it somewhere — all by hand. It's slow, inconsistent, and nobody enjoys doing it.

The founder tells you:

> "I don't need magic. I need something that reads a request, understands it, drafts a reply, and doesn't let anything urgent slip through the cracks. If you can prove that works, I'll pay you for the real integration next month."

This is your **proof-of-concept**. What you build in the next 90 minutes is the exact kind of demo that gets freelance automation engineers hired — and it's a real pattern used in production by support, sales, and moderation teams everywhere.

---

## 2. The Twist: Your Agent Must Grade Its Own Work

Anyone can build "form → AI → sheet." That's table stakes. To make this genuinely worth building (and worth showing off), your workflow includes one extra step most beginner tutorials skip:

**A self-check / quality-gate loop.**

After the AI drafts a reply, a *second* AI call reviews that draft against simple rules (tone, length, does it actually address the customer) and returns a **confidence score**. If the score is low, the ticket gets flagged for **human review** instead of being auto-logged as "ready to send." If it's high, it flows straight through.

This single addition turns your project from "a script that calls an API" into **"an AI workflow with a built-in quality-control mechanism"** — a concept every real automation client cares about, and a genuinely strong talking point in an interview or on a CV.

---

## 3. What You Must Build

A working n8n workflow with these stages:

### Stage 1 — Intake (Trigger)
- **n8n Form Trigger** (free, built-in) simulating an incoming support request.
- Fields: `Customer Name`, `Email`, `Subject`, `Message`.

### Stage 2 — AI Understanding
- Use any **free LLM access point** available in n8n — e.g. **Google Gemini free API tier**, **OpenRouter free models**, or **Hugging Face free inference**. No credit card, no paid plan.
- Prompt the model to return structured JSON:
  - `category`: `Bug Report` | `Feature Request` | `General Question`
  - `priority`: `High` | `Medium` | `Low`
  - `draft_reply`: a short, polite 2–4 sentence draft response

### Stage 3 — The Quality Gate (the interesting part)
- Send the `draft_reply` to a **second AI call** with a review prompt, e.g.:
  > "Rate this draft reply from 1–10 on tone, relevance, and completeness. Return `{ score, reason }`."
- Use an **IF node**: if `score >= 7` → auto-approved path; if `score < 7` → flagged-for-human-review path.

### Stage 4 — Priority Routing
- Separately, branch on `priority`/`category`: **Bug Reports or High priority** get tagged differently from everything else — in a real deployment this is the branch that would page someone; here it just needs to be visibly distinct in your logged output.

### Stage 5 — Logging
- Append every processed ticket — original fields + AI output + quality score + final status (`Auto-Approved`, `Needs Human Review`, `Escalated`) — as a new row in a **Google Sheet** (free account) or via n8n's **Read/Write File** node if you'd rather not connect Google.

### Stage 6 — Confirmation Output
- End with a **Set/NoOp** node returning a clean summary object of what happened to the ticket.

---

## 4. Constraints

- **Zero paid tools.** Everything runs on n8n's free 14-day trial + free-tier third-party services only.
- Any free LLM provider is fine — Google AI Studio (Gemini) is the most reliable free option and recommended.
- Workflow must **run successfully end-to-end at least once** — proof required (see Submission).
- **Max 10–12 nodes.** This is a focused, elegant build — not a sprawling pipeline. Efficiency is part of what's graded.
- Choose any AI node style (AI Agent, Basic LLM Chain, or raw HTTP Request) — you should be able to explain *why* you picked it.

---

## 5. Step-by-Step Guidance

1. Sign up for the n8n free trial (no card required for basic use).
2. Add a **Form Trigger** with the 4 intake fields.
3. Grab a **free API key** from Google AI Studio (Gemini) — under 5 minutes, free.
4. Add an **AI node** for classification + drafting; prompt it to return clean JSON.
5. Parse the JSON with a **Structured Output Parser** or **Set node**.
6. Add a **second AI node** — the reviewer — that scores the draft reply.
7. Add an **IF node** on the score (`>= 7` vs `< 7`).
8. Add another **IF/Switch** on priority/category for the urgent-routing branch.
9. Log everything to **Google Sheets** or a local file, including the final status.
10. Add a closing **Set/NoOp** node summarizing the outcome.
11. Test with 3 different tickets: an obvious bug, a vague/low-quality request (to trigger the review path), and a routine question.
12. Export the workflow JSON.

---

## 6. Deliverables (Submission)

Submit one .zip or shared folder containing:

1. **`workflow.json`** — exported n8n workflow.
2. **`screenshot-execution.png`** — one successful full run, all nodes green.
3. **`writeup.md`** (max 300 words) answering:
   - Which free LLM provider did you use, and why?
   - How does your quality-gate step actually change the outcome for a ticket? Walk through one concrete example.
   - If QuickDesk hired you for real next month, what's the first thing you'd upgrade?
4. *(Optional, strongly recommended for CV/portfolio impact)* A 2–3 minute screen recording (Loom or similar, free tier) walking through a live run.

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| Workflow triggers and runs end-to-end without errors | 20% |
| AI classification + drafting returns correct structured output | 20% |
| Quality-gate logic correctly scores and branches drafts | 25% |
| Priority/category routing works and is clearly distinguishable in the log | 15% |
| Logging captures all fields including quality score and final status | 10% |
| Write-up shows real understanding of design trade-offs | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- **It's not a toy.** Form-in → AI-classify → AI-review → conditional-route → log is a real pattern used in production support, sales-lead qualification, and content-moderation systems today.
- **The quality-gate step is the differentiator.** Most beginner AI-automation projects stop at "call an API once." Adding a second AI pass that checks the first one's work is a concept straight out of real agentic system design — and it's the kind of detail that makes a portfolio piece stand out.
- **It's genuinely CV-worthy.** A candidate can honestly write: *"Designed and built an AI-powered support triage system in n8n featuring a self-review quality gate — automatically routing low-confidence AI outputs to human review while auto-approving high-confidence responses."* That's a sentence that gets a second interview.
- **Zero cost, full learning.** Every component — trigger, LLM calls, conditional logic, structured parsing, storage — is built entirely on free tiers, so any student can complete it and keep the working workflow afterward.

---

*End of assessment.*
