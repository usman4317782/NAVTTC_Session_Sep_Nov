# n8n AI Automation — Practical Assessment
## Build: "The Meeting That Actually Ends" 📋

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

A 6-person remote team at **"Loom & Co."** has a recurring problem: every meeting produces a wall of raw notes, but nobody follows up on what was actually agreed. Tasks fall through the cracks because nobody explicitly wrote "who does what by when." The team lead says:

> "I don't need a transcription tool — I have that already. I need something that takes messy meeting notes and forces out the actual commitments: who owns what, and by when. If it can't find an owner or a deadline, I want it to say so instead of guessing."

You're building an **action-item extraction pipeline** — turning unstructured meeting notes into accountable, trackable tasks.

---

## 2. The Twist: Refuse to Guess

The single biggest failure mode of "AI extracts tasks from notes" tools is that the model **invents** an owner or deadline when the notes are ambiguous, giving false confidence. Your workflow must explicitly instruct the AI to output `"unassigned"` or `"no deadline specified"` rather than guessing — and then your workflow must **route incomplete action items differently** from complete ones, prompting a human to fill the gap instead of silently trusting a hallucinated owner.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** with one large multiline field: `Raw Meeting Notes` (paste a realistic block of messy notes — decisions, tangents, half-formed ideas).

### Stage 2 — AI Extraction
- Use a **free LLM node**. Prompt it to extract **all action items** as a JSON array, where each item has:
  - `task`: string
  - `owner`: string, or exactly `"unassigned"` if not stated in the notes
  - `deadline`: string, or exactly `"no deadline specified"` if not stated
  - `confidence`: `"clear"` or `"inferred"` — `"inferred"` if the model had to read between the lines at all

### Stage 3 — Splitting
- Use n8n's **Split Out** (or **Item Lists**) node to turn the array of action items into individual items flowing through the workflow separately — a core n8n data-handling skill.

### Stage 4 — Completeness Routing
- **IF node** per item: if `owner == "unassigned"` OR `deadline == "no deadline specified"` OR `confidence == "inferred"` → route to **"Needs Clarification"**; otherwise → route to **"Ready to Assign"**.

### Stage 5 — Logging
- Log every action item (with its routing status) as its own row in **Google Sheets** or append to a local file — one meeting's worth of tasks should produce multiple rows.

### Stage 6 — Confirmation
- **Set/NoOp** or **Aggregate** node producing a final summary: total tasks found, how many were ready vs. needing clarification.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- Must use a **Split Out / Item Lists node** — this is a required, graded skill check for handling arrays of AI-extracted items.
- The AI must **never fabricate an owner or deadline** — enforce and verify this explicitly in testing.
- Max **10–12 nodes**.
- Must run end-to-end with meeting notes producing **at least 4 distinct action items**, with at least one deliberately ambiguous (no clear owner/deadline).

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the `Raw Meeting Notes` field.
3. Write realistic sample meeting notes for testing (at least 150–200 words, mixing clear and vague commitments).
4. Build the AI extraction prompt, being explicit about the "never guess" instruction and required JSON array shape.
5. Parse the response, then use Split Out to fan out each action item.
6. Add the IF node for completeness routing.
7. Log each item to Google Sheets or a local file.
8. Add an Aggregate/Set node for the final summary.
9. Test and confirm ambiguous items correctly route to "Needs Clarification."
10. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png`
3. `writeup.md` (max 300 words):
   - Paste your sample meeting notes and the resulting action items list.
   - Did the AI correctly say `"unassigned"` instead of guessing on your ambiguous item? Show the output.
   - How would this integrate with a real task tool (Trello, Asana, Linear) in a production version?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| AI correctly extracts multiple discrete action items as structured JSON | 20% |
| AI correctly avoids fabricating owners/deadlines on ambiguous items | 25% |
| Split Out node correctly fans out items for individual processing | 15% |
| Logging shows each action item as a distinct, complete row | 10% |
| Write-up quality | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Meeting-to-action-item automation is one of the **most commonly requested AI automations** for remote teams and consultancies — genuinely sellable as a freelance service.
- The "refuse to guess" constraint teaches a critical, often-overlooked AI engineering skill: **designing prompts that make hallucination visible instead of hiding it**.
- The Split Out / Item Lists pattern is core n8n knowledge for any workflow that processes a *list* of AI outputs, not just one — a skill this assessment specifically forces you to practice.
- CV line: *"Built an AI meeting-notes-to-action-items pipeline in n8n that extracts structured, accountable tasks and explicitly flags ambiguous ownership/deadlines instead of guessing — reducing follow-up errors for remote teams."*
- Fully free to build and keep.

---

*End of assessment.*
