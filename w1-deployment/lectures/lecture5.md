# Monitoring ML Pipelines

Many AI systems consist of multiple linked components rather than a single model. Understanding how these pipelines behave is critical for effective monitoring.

### 1. What is an ML Pipeline?

A sequence of multiple machine learning and non-ML steps.

- **Example (Speech)**: `Audio` → `VAD (Voice Activity Detection)` → `Speech Recognition` → `Transcript`.
  - _Role of VAD_: Clips audio to save bandwidth by only sending portions where speech is detected.
- **Example (E-commerce)**: `Clickstream Data` → `User Profile` (e.g., "Does user own a car?") → `Recommender System`.

### 2. Cascading Effects

A problem in one part of the pipeline can flow downstream and degrade the entire system.

- If the **VAD** starts clipping audio differently (due to a new microphone), the **Speech Recognition** system may fail because its input distribution has changed.
- If a **User Profile** starts outputting "Unknown" for certain attributes, the **Recommender System** will produce lower-quality suggestions.

### 3. Monitoring Strategies for Pipelines

- **Brainstorm per Component**: Don't just monitor the final output. Analyze what can go wrong at **each stage**.
- **Metric Types**: Track software, input, and output metrics for **every individual module** in the pipeline.
- **Alerting**: Set alerts for intermediate stages (e.g., "Percentage of 'Unknown' tags in User Profiles has increased") to catch cascading failures early.

### 4. Rate of Data Change

The frequency of data drift varies by application:

- **Slow Change (B2C/User Data)**: Usually changes over months/years. It's rare for millions of users to shift behavior simultaneously (exceptions: COVID-19, major viral trends).
- **Fast Change (B2B/Enterprise Data)**: Can shift in minutes.
  - _Manufacturing_: A new batch of material changes product appearance instantly.
  - _Business Logic_: A CEO's decision can immediately change how business data is generated.
- **Face Recognition**: Generally slow, as human appearance and fashion change gradually.

### 5. Takeaway

Monitoring an ML pipeline requires tracking the "statistical health" of every step to detect and isolate where a cascading failure originates.
