## Exercise 2 — Access to Flight Information and Governance Data

**Goal:** Explore how access to governance metadata helps the AI agent interpret the planned flight data. In this phase, Bob can query both watsonx.data and watsonx.data Intelligence, but it does not yet use the real-time Kafka messages.

**Mode:** Select **Flight-info with Metadata** in Bob.

### How to run the exercise

Ask the following questions one by one in the same Bob conversation. Submit each question and review both the answer and the tools Bob used.

### Question 2.1

> What is the status of flight DL404?

#### What to observe

- Bob recognizes that governance information is available.
- It queries the governance layer for information about the flight status codes.
- Bob maps status code `3` to **Delayed** and provides a more precise, human-readable answer.
- Compare this answer with the result from Exercise 1, where the numeric code could not be interpreted.

### Question 2.2

> Which flights are currently boarding?

#### What to observe

- Bob uses the governance information to determine which numeric status code means **Boarding**.
- It then queries the planned flight data using that code.
- Bob may reuse status-code information already retrieved in the current conversation.
- The planned data contains one flight that is currently marked as boarding.

### Question 2.3

> I am flying to New York. Where and when is my flight?

#### What to observe

- Bob returns the available New York flight options with understandable status information.
- The answer is more useful than in Exercise 1 because the numeric status codes can now be interpreted.
- Bob is still querying only the static flight tables. Gate assignments and flight status may therefore no longer reflect the current airport situation.

### Question 2.4

> Give me a list of possible status codes for flights.

#### What to observe

- Bob queries the governance metadata directly.
- It returns the available flight status codes together with their meanings.
- This demonstrates that Bob can use watsonx.data Intelligence not only to interpret query results, but also to answer questions about the metadata itself.

### Reflection

The governance layer turns technical values into business meaning. Bob can now explain flight status codes and use natural-language concepts such as **Boarding** when querying the planned data. However, the result is still based on static information. Real-time events are added in the next exercise.

When you are ready, continue with [exercise-3.md](exercise-3.md).
