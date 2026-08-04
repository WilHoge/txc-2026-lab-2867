# Exercise 1 — Raw Data Only

**Goal:** Experience what an AI assistant can (and cannot) do with raw, uncontextualized data.

Bob has SQL access to the flight data in `iceberg_catalog.lab2867` but has **no metadata context**. The watsonx.data Intelligence MCP server is disabled. Status codes are opaque numbers — no glossary, no data classes.

**Mode:** use the **Flight-Info** mode.

---

## Questions to ask Bob

Ask these questions one by one in Bob Chat:

1. **"I am flying to New York. Where and when is my flight?"**

2. **"What is the status of flight UA892?"**

3. **"What is the status of flight DL404?"**

4. **"What airline operates flight UA892 and where is their desk?"**

5. **"What gate should I go to for flight DL404 to JFK?"**

---

## What to observe

- For question 1: Bob finds three New York flights (DL404 → JFK, UA892 → EWR, AA334 → LGA) and returns gate and departure time — but shows raw `status_code` numbers. No human-readable status.
- For questions 2 and 3: Bob returns a numeric code (e.g. `3`). It may guess the meaning, but it cannot be certain. This is the core limitation of Exercise 1.
- For question 4: Bob can join the `airlines` table and return the desk location — showing the limit is code-specific, not a general SQL failure.
- For question 5: Bob returns the planned gate (B12) — the static answer is correct. The `status_code 3` (Delayed) is present but unlabelled.

---

## Reflection

> Raw data without meaning is not AI-ready. Numeric codes are invisible walls between data and decision.

When you are ready, continue with [exercise-2.md](exercise-2.md).
