# Exercise 3 — Adding Real-Time Context

**Goal:** Understand that even perfect metadata cannot replace current state. Real-time events change the answer.

The facilitator is now firing live events into the system via Kafka. Flight statuses, gates, and departure times are changing as you work through this exercise.

**Mode:** switch to the **Flight-Info with Complete Context** mode.

---

## The Story

You are booked on **UA892 → Newark (EWR)**. Three New York flights exist in the schedule:

| Flight | Destination | Planned Gate | Initial Status |
|--------|-------------|-------------|----------------|
| DL404  | JFK         | B12         | DELAYED        |
| UA892  | EWR         | B4          | DELAYED        |
| AA334  | LGA         | C11         | ON TIME        |

Watch what happens to your flight — and what Bob can tell you at each step.

---

## Before the first event — baseline

10. **"I am flying to New York — show me all options."**

    Bob lists all three NY flights with static data. No Kafka events have fired yet.

11. **"What gate should I go to for flight UA892?"**

    Bob answers Gate **B4** from the static `flights` table.

---

## After Event 1 — UA892 first delay (+30 min)

12. **"Why does UA892 have a delay?"**

    Bob reads the Kafka event: reason code 5 = *"Late arriving aircraft from previous leg"*. Departure pushed back +30 min. The metadata resolves the reason code to plain English.

---

## After Event 2 — DL404 gate change B12 → C7

13. **"What gate should I go to for flight DL404?"**

    Bob now answers Gate **C7** — the live gate-change event overrides the static B12. Without Kafka, the answer would still be B12.

---

## After Event 3 — UA892 second delay (+20 min more)

14. **"How much total delay does UA892 have now?"**

    Bob reads the latest Kafka event: cumulative +50 min delay. New reason: *reason code 4 = "Crew availability or rest requirement"*. Both reason codes are decoded via metadata.

---

## After Events 4–9 — background activity

15. **"Which flights are boarding right now?"**

    Bob reads the BOARDING events: NK712 (Gate A8) and SW210 (Gate A4) are boarding.

16. **"Is flight AA101 to Dallas still operating?"**

    After event 9: Bob reports AA101 as **CANCELLED**.

---

## ⭐ After Event 10 — UA892 CANCELLED (climax)

17. **"What is the current status of my flight UA892?"**

    Bob reads the most recent Kafka event: UA892 is **CANCELLED**. Status code 2 resolved via metadata: *"Flight has been cancelled — contact airline for rebooking."*

18. **"My flight UA892 was cancelled — what other flights to New York are there?"**

    Bob identifies JFK / EWR / LGA as New York airports and returns: **DL404 → JFK** (slightly delayed, Gate C7) and **AA334 → LGA** (on time, Gate C11) — all status labels decoded via metadata.

19. **"Which of the two remaining New York flights departs soonest?"**

    Bob compares current departure times: DL404 is earlier but delayed; AA334 is on time. AA334 is the safer rebooking option.

---

## After Event 11 — AA334 boarding confirmed

20. **"When do I need to be at the gate for AA334?"**

    Bob reads the BOARDING event for AA334: Gate C11, boarding now. Advises to go immediately.

---

## What to observe

- The same question (*"What gate for DL404?"*) gives different answers before and after Event 2 — the static data has not changed, but the live Kafka event overrides it
- At the climax (Event 10), Bob uses all three layers simultaneously: SQL data for the flight list, Intelligence metadata to decode status codes, Kafka events for current state
- The rebooking scenario is resolved by Bob's own reasoning — no hard-coded lookup is needed

---

## Reflection

> Real-time context is the final layer. It answers "what is true *right now*" — something that even the richest metadata cannot provide alone.
>
> All three layers together — raw data, metadata, real-time events — are what make an AI assistant genuinely useful at the moment of decision.

---

## Optional Deepdive

- Ask Bob: **"Is there food near the gate for AA334, and do I still have time to grab something?"**  
  Bob checks the `gates` table for Gate C11 amenities and the BOARDING event time.

- Ask Bob: **"Which flights are delayed because of weather?"**  
  After event 12: SW388 delayed +10 min, reason code 1 = *"Weather conditions at origin or destination"* — decoded via metadata.

- Ask Bob: **"Has anything changed for the Delta flight to Los Angeles?"**  
  After event 8: DL872 gate changed from T1 to T3.

---

## You are done!

Feel free to ask Bob any other flight-related question and explore what it can (and cannot) answer.
