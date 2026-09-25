# n8n AI Automation — Practical Assessment
## Build: "The Empty-Fridge Rescue Bot" 🍳

**Duration:** 1.5 hours
**Format:** Hands-on build (n8n Free 14-Day Trial account)
**Cost to complete:** $0 — free tools only
**Submission:** Exported workflow JSON + short write-up

---

## 1. The Story

You're prototyping a feature for a small food-tech startup, **"PantryPal,"** aimed at reducing household food waste. Their idea:

> "People stare into their fridge with random leftover ingredients and have no idea what to cook. We want to type in whatever's left, plus any dietary restriction, and get back a real recipe using *mostly* what we already have — plus a short shopping list for the one or two things we're missing. Bonus points if it warns us about any restriction conflicts."

You're building the **first working prototype** of this feature — a genuinely useful personal tool, not just a demo.

---

## 2. The Twist: Constraint Safety Check

Dietary restrictions are not a "nice to have" — getting this wrong (e.g., suggesting peanuts for someone with a peanut allergy) is a real trust-breaking failure. Your workflow must include an explicit **second-pass safety check**: after the recipe is generated, a **separate AI call re-reads the final recipe against the stated restriction** and confirms compliance or flags a conflict — never trusting the first generation blindly.

---

## 3. What You Must Build

### Stage 1 — Intake
- **n8n Form Trigger** with fields: `Available Ingredients` (multiline text, comma or line separated), `Dietary Restriction` (e.g., "vegetarian", "gluten-free", "nut allergy", or "none"), `Servings Needed`.

### Stage 2 — Recipe Generation (AI)
- **Free LLM node**. Prompt it to generate a recipe using **primarily** the listed ingredients, respecting the stated restriction, scaled to the servings count. Require structured JSON:
  - `recipe_name`: string
  - `ingredients_used_from_pantry`: array
  - `additional_ingredients_needed`: array (the shopping list — should be short, ideally 0–3 items)
  - `steps`: array of strings
  - `restriction_applied`: string (repeats back what restriction it followed)

### Stage 3 — Safety Re-Check (AI, second pass)
- A **second, separate AI call** takes the generated recipe + stated restriction and returns:
  - `compliant`: `true` or `false`
  - `conflict_details`: string explaining any conflict found (or `"none"`)

### Stage 4 — Routing
- **IF node**: if `compliant == false` → route to **"Blocked — Regenerate Needed"** (do not deliver the recipe as-is); if `true` → route to **"Approved"**.

### Stage 5 — Output
- On the Approved path, use a **Set node** to format a clean, human-readable recipe card (name, ingredients, shopping list, steps).
- Log every request (inputs + generated recipe + compliance result) to **Google Sheets** or a local file.

### Stage 6 — Confirmation
- **Set/NoOp** node confirming the final status.

---

## 4. Constraints

- **No paid tools** — n8n free trial + free LLM API only.
- Must implement the **second-pass safety re-check as a genuinely separate AI call**, not a rule reused from Stage 2 — the point is independent verification.
- Max **10–12 nodes**.
- Must test with **at least one deliberately conflicting restriction case** (e.g., ask for a recipe with "peanut" in the ingredient list AND a "nut allergy" restriction) to prove the safety check actually catches something.

---

## 5. Step-by-Step Guidance

1. Set up n8n free trial + free LLM API key.
2. Build the Form Trigger with the 3 fields.
3. Build the recipe-generation prompt, requiring the structured JSON shape above.
4. Build the independent safety re-check prompt (must not simply reuse Stage 2's output as "trusted").
5. Parse both AI responses.
6. Add the IF node routing on `compliant`.
7. Format the approved recipe with a Set node.
8. Log to Google Sheets or a local file.
9. Add closing Set/NoOp confirmation.
10. Test 3 cases: a normal request, a restriction that's easy to satisfy, and one deliberately conflicting case — confirm the conflicting case is correctly blocked.
11. Export the workflow JSON.

---

## 6. Deliverables

1. `workflow.json`
2. `screenshot-execution.png` — including the blocked/conflict test case
3. `writeup.md` (max 300 words):
   - Which free LLM did you use?
   - Show the output of your deliberately-conflicting test case — did the safety check catch it?
   - Why is a second independent AI call better here than just trusting the first generation's `restriction_applied` field?
4. *(Optional)* 2–3 min screen recording

---

## 7. Evaluation Rubric

| Criteria | Weight |
|---|---|
| End-to-end execution without errors | 20% |
| Recipe generation is coherent and uses mostly pantry ingredients | 20% |
| Independent safety re-check is genuinely implemented as a separate call | 25% |
| Conflict case is correctly caught and blocked | 20% |
| Logging and output formatting | 5% |
| Write-up quality | 10% |

**Passing threshold:** 70%

---

## 8. Why This Assessment Is Worth Doing

- Practical, everyday-useful AI tools (recipe/food-waste apps) are a strong **portfolio category** — tangible, relatable, easy to demo to a non-technical audience.
- The independent safety re-check pattern — **"don't trust generation 1, verify with a separate pass"** — is a core technique in production LLM systems dealing with any safety-critical constraint (allergies, medical, legal, financial).
- CV line: *"Built an AI recipe-generation workflow in n8n with an independent dietary-safety verification pass, preventing restriction-violating recipes from being delivered to users."*
- Fully free, and genuinely fun to demo.

---

*End of assessment.*
