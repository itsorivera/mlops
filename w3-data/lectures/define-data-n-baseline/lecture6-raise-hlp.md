# Raising Human-Level Performance (HLP)

While many academic papers focus on _beating_ HLP, practical ML applications benefit most from _raising_ HLP. This lecture explains how improving label consistency transforms HLP from a static benchmark into a driver for model improvement.

## 1. External vs. Human-Defined Ground Truth

The utility of HLP depends on whether you are predicting an objective physical reality or a subjective human opinion:

- **Externally Defined Ground Truth (Objective):**
  - **What it is:** The correct answer exists independently of human judgment (e.g., a biopsy confirms if a tumor is malignant, or a radar sensor confirms the exact distance to an object).
  - **HLP's Role:** Here, HLP measures the human’s ability to **predict reality**. If humans are only correct 80% of the time compared to the biopsy, that 20% error represents the baseline difficulty that the AI aims to overcome.
- **Human-Defined Ground Truth (Subjective):**
  - **What it is:** The "truth" is simply whatever the expert says it is (e.g., classifying a comment as "offensive" or a doctor’s opinion on an x-ray without a physical test to confirm).
  - **HLP's Role:** In this case, HLP measures **consensus**, not absolute truth. A low HLP (e.g., 60%) doesn't mean the task is impossible; it signifies that humans do not agree because the labeling instructions are vague.

**In Summary:** If there is an external source, HLP shows the inherent **difficulty** of the problem. If humans are the source, low HLP signals a need for **better labeling rules**.

## 2. The Strategy: Raising HLP

Instead of proving a model is better than a noisy human baseline, prioritize **raising HLP**.

- **The Process:** Sitting down with labelers to agree on objective thresholds (e.g., "a defect is exactly ≥ 0.3mm").

![Raising HLP](/w3-data/lectures/assets/raising-hlp.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

- **The Result:** This can raise measured HLP from ~67% to 100%. While this makes it "harder" to beat HLP, it yields higher quality data that directly translates to better model performance in production.

## 3. HLP in Structured Data

Though less common, HLP is vital for complex structured data tasks requiring expert judgment:

- **Security:** Network intrusion detection and fraud classification.
- **Identity:** User ID merging and bot/spam detection.
- **Inference:** Predicting modes of transport (bus vs. car) from GPS traces.

In all these cases, if human experts disagree, the priority should be developing a consistent labeling standard to provide the model with a clear signal.

## Summary: HLP as a Diagnostic Tool

HLP should be used as a reference to drive error analysis. If you find a significant gap between HLP and 100% accuracy, treat it as a signal to investigate and improve your labeling instructions.

### Technical Definitions

- **HLP (Human Level Performance):** Primarily a measure of **human agreement**. A low HLP indicates "dirty" data or subjective labeling rules.
- **Accuracy Gap ($HLP - Accuracy$):**
  - **Large Gap:** Suggests an **algorithmic problem** (the model is failing to learn from valid data).
  - **Low HLP (regardless of gap):** Suggests a **process problem** (the labeling instructions are ambiguous).

> [!IMPORTANT]
> **Key Insight:** A model cannot be more accurate than the consistency of the data used to train it.

### Case Study: Scratch vs. Discoloration

| Type of Defect    | Accuracy | HLP | Gap | % of Data | Analysis                                                                                                                                               |
| :---------------- | :------- | :-- | :-- | :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Scratch**       | 95%      | 98% | 3%  | 50%       | **Model Problem:** Data is high-quality (98% HLP). Improving this 3% requires technical changes to code/architecture.                                  |
| **Discoloration** | 90%      | 90% | 0%  | 50%       | **Data Problem:** The model has reached the "ceiling" of an inconsistent system. Improving this is cheaper by clarifying labels than by changing code. |

**Engineering Strategy:** It is much more efficient to increase system accuracy by raising HLP (e.g., from 90% to 98% through clearer rules) than by attempting to force an algorithm to learn from inconsistent data.
