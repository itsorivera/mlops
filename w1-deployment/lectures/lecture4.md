# Monitoring Deployed ML Systems

Monitoring is an **iterative process** that ensures the system meets performance expectations over time.

### 1. Metric Selection Strategy

- **Brainstorming**: Identify everything that could go wrong and define statistics/metrics to detect those failures.
- **Start Broad**: Monitor a large set of metrics initially; remove those that prove unnecessary over time.
- **Thresholds & Alarms**: Set specific limits (e.g., Server Load > 0.9) to trigger notifications for the team.

### 2. Types of Monitoring Metrics

#### A. Software Metrics

- Health of the infrastructure: Memory, compute, latency, throughput, and server load.
- Often provided by default in MLOps tools.

#### B. Input Metrics ($X$)

Measure changes in the input distribution:

- **Average length/volume**: (e.g., audio clip length).
- **Missing values**: Critical for structured data tasks.
- **Image characteristics**: (e.g., average brightness for visual inspection).

#### C. Output Metrics ($Y$)

Measure the performance or health of the model's predictions:

- **Null outputs**: Frequency of empty/null strings.
- **User Behavior**: Signs of failure (e.g., quick re-searches, switching from voice to typing).
- **Business Metrics**: Click-Through Rate (CTR).

### 3. Iterative Deployment Loop

Deployment follows a cycle similar to modeling:

1.  **Deployment**: Launch the system with monitoring.
2.  **Real Traffic**: Gather live user data.
3.  **Performance Analysis**: Deep dive into how the model behaves.
4.  **Update**: Adjust the model or infrastructure based on findings.

### 4. Model Maintenance & Retraining

- **Manual Retraining**: Most common; an engineer trains, performs error analysis/vetting, and pushes the update.
- **Automatic Retraining**: Common in high-scale consumer internet applications, but requires high trust in the pipeline.

### 5. Takeaway

Monitoring is the only way to spot problems (software or statistical) that necessitate model updates or deeper error analysis to maintain performance in production.
