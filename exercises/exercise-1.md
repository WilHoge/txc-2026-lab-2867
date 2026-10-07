## Exercise 1 — Access to Planned Flight Information

**Goal:** Explore what the AI agent can answer when it has access only to the planned flight data stored in watsonx.data. In this phase, the agent does not have access to the governance metadata or real-time Kafka messages.

**Mode:** Select **Flight-info** in Bob.

### How to run the exercise

Ask the following questions one by one in Bob. Submit each question and review both the answer and the tools Bob used.

### Question 1.1

> I am flying to New York. Where and when is my flight?

#### What to observe

- Bob uses the watsonx.data MCP server to discover the available tables and their structures.
- Bob queries the planned flight data to find flights to New York.
- The available table data does not explain the meaning of the numeric status codes.
- Bob should provide the flight details it can retrieve and clearly state that the status information cannot be interpreted with the available context.

### Question 1.2

> What is the status of flight DL404?

#### What to observe

- Bob retrieves the status value from the flight data.
- The result contains a numeric status code.
- Bob cannot determine the business meaning of that code because the governance layer is not available.
- The mode rules prevent Bob from guessing or supplementing the answer from general knowledge.
- To inspect the SQL query, expand **Ran Execute Select (watsonxdata)** in Bob.

### Question 1.3

> What airline operates flight UA892 and where is their desk?

#### What to observe

- Bob can answer questions that require information from more than one table.
- It discovers the required table structures and combines the available flight and airline data.
- This shows that the limitation in this phase is missing business meaning for coded values, not a general inability to query or join data.
- To review the table discovery steps, expand the relevant **Called MCP** entries in Bob.

### Question 1.4

> What tables do you have access to?

#### What to observe

- Bob returns the tables available in the watsonx.data lakehouse under catalog `iceberg_catalog` and schema `lab2867`.
- This question demonstrates that Bob can also answer technical questions about the connected data source.

### Reflection

The planned flight data provides an authoritative source for flight numbers, destinations, departure times, gates, and airline information. However, numeric codes remain ambiguous without the governance metadata that explains their business meaning.

When you are ready, continue with [exercise-2.md](exercise-2.md).
