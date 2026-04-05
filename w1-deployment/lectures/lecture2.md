# Challenges in ML Deployment

Deployment involves two major categories of challenges: **Machine Learning (Statistical)** and **Software Engineering**.

### 1. Machine Learning & Statistical Issues

These involve changes in the data after the model is in production.

- **Data Drift**: Change in the input distribution **$P(X)$**.
  - _Examples_: New microphone models in speech, changes in factory lighting, or new celebrities being mentioned.
- **Concept Drift**: Change in the mapping from input to output **$P(Y|X)$**.
  - _Examples_: House prices increasing despite identical house sizes; credit card fraud patterns shifting due to major events like COVID-19.
- **Rate of Change**:
  - _Gradual_: Natural evolution of language.
  - _Sudden_: Immediate shifts due to external shocks (e.g., pandemics).

### 2. Software Engineering Issues

Decisions regarding the implementation of the prediction service.

- **Real-time vs. Batch**:
  - _Real-time_: Requires response in milliseconds (e.g., speech recognition).
  - _Batch_: Periodic processing (e.g., overnight hospital records).
- **Cloud vs. Edge**:
  - _Cloud_: Large compute resources, but requires internet.
  - _Edge_: Runs locally (car, phone, factory). High reliability and low latency, but limited compute.
- **Compute Resources**: Consider GPU, CPU, and Memory constraints. Models might need compression to fit on deployment hardware.
- **Metrics**:
  - **Latency**: Time budget for a single prediction.
  - **Throughput (QPS)**: Number of queries the system can handle per second.
- **Logging**: Essential for performance analysis and future retraining data.
- **Security & Privacy**: Dependent on data sensitivity (e.g., Healthcare/EHR vs. public data).

### 3. Deployment Maturity

- **First Deployment**: Only about 50% of the project.
- **Maintenance & Updates**: The second half of the work starts after the first deployment. It involves monitoring for drift and feeding live data back into the system to retrain and update models.
