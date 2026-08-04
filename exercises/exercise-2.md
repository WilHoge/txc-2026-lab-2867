# Exercise 2 — Adding Metadata Context

**Goal:** Connect watsonx.data Intelligence to Bob and experience how metadata transforms the same data into meaningful answers.

**Mode:** switch to the **Flight-Info with Metadata** mode.

---

## Step 1 — Enable the Intelligence MCP server

1. Open `bob/mcp-servers.json` in a text editor
2. Find the `watsonx-intelligence` entry
3. **Delete** the line `"disabled": true`
4. Save the file
5. **Restart Bob** and switch to the **Flight-Info with Metadata** mode

Bob now has access to Business Terms, Glossary entries, and Data Classes from watsonx.data Intelligence.

---

## Questions to ask Bob

Repeat the same flight-status questions from Exercise 1 — and compare the answers:

6. **"What is the status of flight UA892?"** ← same as question 2 in Exercise 1

7. **"What is the status of flight DL404?"** ← same as question 3 in Exercise 1

8. **"Which flights are currently boarding?"**

9. **"I am flying to New York. Where and when is my flight?"** ← same as question 1 in Exercise 1

---

## What to observe

- Questions 6 and 7 are identical to Exercise 1 — Bob now resolves the numeric `status_code` into a human-readable label and explanation (e.g. *"DELAYED — Flight is delayed, check current departure time."*)
- Question 8: Bob identifies flights with `status_code = 1` (BOARDING) without guessing — the Business Term *Status Code* tells it exactly what code 1 means
- Question 9: Bob returns all three New York options (DL404 → JFK, UA892 → EWR, AA334 → LGA) with full status labels instead of raw numbers

---

## Reflection

> Metadata is the bridge between technical data and human meaning. The same question, asked twice in two different modes, gives a fundamentally different quality of answer.

---

## Optional Deepdive

Ask Bob: **"What is the difference between `dep_planned` and `new_dep`?"**

Observe how Bob looks up both fields in the glossary: *dep_planned* maps to **Planned Departure** — the original schedule that never changes. *new_dep* maps to **New Departure** — the revised time from the latest real-time event (null if no update has been received). This demonstrates that metadata explains the *semantics* of fields, not just their names.

---

When you are ready, continue with [exercise-3.md](exercise-3.md).
