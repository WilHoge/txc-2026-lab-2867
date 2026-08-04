# LAB-2867 — From Data to Meaning

Welcome to the lab. Follow the steps below to get started.

---

## Setup

### Step 1 — Clone the repository

```bash
git clone https://git.ibm.com/<org>/lab-2867.git
cd lab-2867
```

### Step 2 — Configure the MCP servers

The file `.bob/mcp.json.template` contains the MCP server configuration with placeholders for your credentials.

1. Copy the template:
   ```bash
   cp .bob/mcp.json.template .bob/mcp.json
   ```

2. Open `.bob/mcp.json` and fill in the placeholder values — the facilitator will hand these out on the day:

   | Block | Placeholder | Value |
   |-------|-------------|-------|
   | `watsonxdata` | `<your-ibm-cloud-api-key>` | IBM Cloud API key |
   | `watsonxdata` | `https://<your-instance>.lakehouse.saas.ibm.com/lakehouse/api` | watsonx.data instance base URL |
   | `watsonxdata` | `<your-instance-crn>` | CRN of the watsonx.data instance |
   | `wxdi-mcp-server` | `<your-ibm-cloud-api-key>` | IBM Cloud API key |
   | `wxdi-mcp-server` | `https://api.<region>.dai.cloud.ibm.com` | watsonx.data Intelligence service URL |

   > Leave `"disabled": true` on the `wxdi-mcp-server` block for now — you will remove it in Exercise 2.

3. Copy `.bob/mcp.json` into your Bob config directory:
   ```bash
   cp .bob/mcp.json ~/.bob/mcp.json   # adjust path to your Bob installation
   ```

### Step 3 — Install the custom Bob modes

Copy the custom mode definitions into your Bob config directory:

```bash
cp .bob/custom_modes.yaml ~/.bob/custom_modes.yaml   # adjust path if needed
```

This adds three modes to Bob:

| Mode | Used in |
|------|---------|
| **Flight-Info** | Exercise 1 |
| **Flight-Info with Metadata** | Exercise 2 |
| **Flight-Info with Complete Context** | Exercise 3 |

### Step 4 — Restart Bob

Restart Bob so it picks up the new MCP configuration and custom modes.

### Step 5 — Start the lab

Switch to the **Flight-Info** mode in Bob and open [exercises/exercise-1.md](exercises/exercise-1.md).

---

## Data sources

All flight data lives in the watsonx.data catalog:

| Table / View | Description |
|-------------|-------------|
| `iceberg_catalog.lab2867.flights` | Scheduled flight data (20 flights from ATL) |
| `iceberg_catalog.lab2867.airlines` | Airline codes, names, and desk locations |
| `iceberg_catalog.lab2867.gates` | Gate IDs, concourses, and amenities |
| `realtime_data.default.atl_flight_updates` | Live Kafka events (gate changes, delays, cancellations) |
| `iceberg_catalog.lab2867.v_current_flight_status` | Combined view: static data + latest live events |

---

## Exercise overview

| Exercise | Goal | Bob Mode |
|----------|------|----------|
| [Exercise 1](exercises/exercise-1.md) | Raw data only — observe the limits of uncontextualized data | **Flight-Info** |
| [Exercise 2](exercises/exercise-2.md) | Add metadata — the same data becomes meaningful | **Flight-Info with Metadata** |
| [Exercise 3](exercises/exercise-3.md) | Add real-time events — live context completes the picture | **Flight-Info with Complete Context** |
