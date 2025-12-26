⚡ Pulsegen Trend Analysis Agent

Role: Senior AI Engineer Assignment  
Tech Stack: Vanilla JavaScript, HTML5, CSS3 (No external libraries)

---

## 📋 Problem Statement

The objective of this assignment was to design an AI agent that consumes
daily batches of Google Play Store reviews (simulated for Swiggy/Zomato)
and produces a rolling trend analysis report from T-30 to T.

The key challenges highlighted in the problem were:
- Using an **agentic approach** instead of static topic models (LDA/BERT)
- Achieving **high recall topic deduplication**
- Supporting **new and evolving topics** over time

---

## 🧠 Solution Overview

I implemented a **Heuristic Agentic Engine** entirely in the browser.
The goal was not to build a production LLM system, but to demonstrate
how agent-like reasoning, memory, and consolidation can be achieved
without external dependencies.

This makes the solution easy to review, run, and reason about.

---

## ⚙️ Agent Workflow

The system operates as a multi-stage agent pipeline:

1. **Ingestion**
   - Simulates daily batch ingestion of app reviews
   - Each day is treated as an independent batch

2. **Processing & Topic Assignment**
   - Normalizes review text
   - Maps reviews to canonical topics using a taxonomy
   - Avoids direct string matching to improve recall

3. **Aggregation & Reporting**
   - Builds a topic × date frequency matrix
   - Generates trends for the range T-30 → T

---

## 🔁 Solving Topic Deduplication (High Recall)

One of the main challenges is preventing topic fragmentation caused by
slightly different user phrasing.

Examples:
- “Delivery guy was rude”
- “Delivery partner behaved badly”
- “Delivery person was impolite”

To solve this, I implemented a **Synonym–Taxonomy Knowledge Base**.

Instead of treating each phrase as a new topic, the agent:
- Detects intent keywords (e.g., rude, misbehaved, impolite)
- Maps them to a single canonical topic:
  **“Delivery partner rude”**

This ensures similar complaints contribute to the same trend line,
resulting in more accurate analytics.

---

## 🌱 Evolving Topic Detection

The agent also monitors reviews that do not match existing seed topics.
If certain keywords begin appearing consistently in recent days
(e.g., “UI update”, “refund pending”), the agent dynamically creates
a new topic category and starts tracking it.

This allows the system to adapt to **new product issues** without
manual intervention.

---

## 🚀 How to Run

No build tools or backend services are required.

1. Clone this repository
2. Open `index.html` in any modern web browser
3. Select:
   - Target App (Swiggy / Zomato)
   - Target Date (T)
4. Click **Run Agent Analysis**

The dashboard displays:
- Agent decision logs
- Top issue trend visualization
- Detailed topic frequency matrix

---

## 📂 Repository Contents

- `index.html` – Complete self-contained dashboard and agent logic  
- `README.md` – Design explanation and reasoning  

---

## 🎨 Design Decisions

- **Heatmap-style table**: Helps product teams quickly identify high-impact issues
- **Agent Console logs**: Makes the agent’s reasoning transparent and easier to trust
- **No external libraries**: Keeps the solution lightweight and easy to evaluate
