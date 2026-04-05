# Module 1: ML Deployment Master Summary

This document synthesizes the key concepts and strategies for deploying machine learning systems in production.

---

### 1. Challenges in ML Deployment

Deployment involves managing two distinct categories of issues:

#### A. Machine Learning & Statistical (Data Drift)

- **Data Drift**: Change in the input distribution **$P(X)$** (e.g., new microphones, new demographic).
- **Concept Drift**: Change in the mapping **$P(Y|X)$** (e.g., house prices rising while square footage stays same).
- **Rate of Change**: Can be **Gradual** (language evolution) or **Sudden** (external shocks like COVID-19).

#### B. Software Engineering Decisions

- **Real-time vs. Batch**: Low latency (<500ms) vs. periodic/overnight processing.
- **Cloud vs. Edge**: Balancing compute power with reliability and connectivity.
- **Logistical Metrics**: Memory, CPU/GPU constraints, Throughput (QPS), and Latency.
- **Compliance**: Security and privacy (especially in fields like Healthcare).

---

### 2. Deployment Strategies & Patterns

Risk is managed through gradual rollout and the ability to revert quickly.

- **Shadow Mode**: Model runs in parallel; outputs are logged but **no decisions** are made. Highest safety.
- **Canary Deployment**: Initial rollout to a **tiny fraction** (e.g., 5%) of traffic.
- **Blue-Green Deployment**: Routing switch between old (Blue) and new (Green) versions for **instant rollback**.
- **Maturity**: Deployment is only 50% of the work; maintenance is the second half.

---

### 3. Degrees of Automation (Human-in-the-loop)

Automation is a spectrum, not binary:

1.  **AI Assistance**: Human decides; AI highlights regions or provides info.
2.  **Partial Automation**: AI handles **confident** cases; humans handle **uncertain** cases.
3.  **Full Automation**: AI handles every decision (common for consumer internet).

---

### 4. Monitoring Systems & Dashboards

Monitoring must be **iterative**: `Live Traffic → Performance Analysis → Update Deployment`.

#### Metric Types:

- **Software Metrics**: Server load, memory, compute health.
- **Input Metrics ($X$)**: Average length, brightness, missing values.
- **Output Metrics ($Y$)**: Frequency of nulls, user behavior (e.g., re-searching/switching to manual input).
- **Iterative Thresholds**: Start broad with multiple metrics and prune over time. Set alarms for critical breaches.

---

### 5. Monitoring ML Pipelines

Many systems use a sequence of models (e.g., `Audio → VAD → Speech Rec → Transcript`).

- **Cascading Effects**: Failures in early modules (e.g., VAD) flow downstream and degrade the entire pipeline.
- **Component-Level Monitoring**: Each stage should have dedicated software, input, and output metrics.
- **Rate of Data Change**:
  - **B2C (User Data)**: Usually changes **slowly** (hard for millions to shift behavior).
  - **B2B (Enterprise Data)**: Can shift **suddenly** (e.g., a factory/CEO decision).
