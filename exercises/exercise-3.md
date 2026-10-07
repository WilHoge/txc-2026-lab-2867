## Exercise 3 — Access to Complete Flight Context

**Goal:** Explore how real-time events complement planned flight data and governance metadata. In this phase, Bob can use watsonx.data, watsonx.data Intelligence, and live Kafka messages to answer questions based on the latest available information.

**Mode:** Select **Flight-info with Complete Context** in Bob.

### How to run the exercise

Ask the following questions at the indicated points in the event sequence. The instructor will show which Kafka messages have already been sent. Review both Bob's answer and the tools it used.

### Question 3.1 — No message required

> I am flying to New York — show me all options.

#### What to observe

- Bob recognizes that it has access to the planned data, governance metadata, and real-time messages.
- It queries the available context layers and combines the results.
- If no Kafka messages have arrived, the answer is based on the planned flight data.
- Your result may differ if live messages are already present.

### Question 3.2 — After message 1

> Why does UA892 have a delay?

#### What to observe

- Bob combines the planned flight data with the live update for UA892.
- It uses the governance metadata to interpret reason code `5` as **Late arriving aircraft from previous leg**.

### Question 3.3 — After message 2

> What gate should I go to for flight DL404?

#### What to observe

- Bob finds a live gate-change message for DL404.
- It uses the current gate from the real-time event rather than relying only on the planned gate.

### Question 3.4 — After message 3

> How much total delay does UA892 have now?

#### What to observe

- Multiple delay messages exist for UA892.
- Bob uses the latest applicable message to determine the current delay.

### Question 3.5 — Before message 9

> Is flight AA101 to Dallas still operating?

#### What to observe

- Before message 9, the available information indicates that AA101 is still operating.
- This creates a baseline for comparison after the cancellation message arrives.

### Question 3.6 — After message 4 and before message 10

> What is the current status of my flight UA892?

#### What to observe

- Bob combines the available updates for UA892.
- At this point, the flight has a delay, a gate change, and an updated reason for the delay.

### Question 3.7 — After message 4

> Which flights are boarding right now?

#### What to observe

- Bob evaluates the live messages to identify flights currently boarding.
- Depending on which messages have arrived, the answer contains two or three boarding flights.

### Question 3.8 — Anytime

> Show me a current overview of all flights.

#### What to observe

- Bob combines all information available at the time of the query.
- The overview reflects planned flight information, governance meaning, and the latest real-time updates.

### Question 3.9 — After message 10

> What is the current status of my flight UA892?

#### What to observe

- Bob uses the most recent event and reports that UA892 is cancelled.
- Compare this answer with Question 3.6, which was asked before message 10.

### Question 3.10 — After message 10

> My flight UA892 was cancelled — what other flights to New York are there?

#### What to observe

- Bob searches the available flights for alternatives to New York.
- It reports the current status of the alternatives using all available context layers.

### Question 3.11 — After message 11

> Is there food near the gate for AA334, and do I still have time to grab something?

#### What to observe

- Bob combines gate information with the latest boarding information for AA334.
- Because boarding has already begun, it recommends going to the gate rather than spending time getting food.

### Reflection

Planned data provides the authoritative schedule, governance metadata explains what the data means, and real-time events show what is happening now. Together, these layers allow Bob to answer using the latest known operational context rather than an outdated snapshot.

### You are done!

Feel free to ask Bob additional flight-related questions and explore what it can and cannot answer from the available context.
