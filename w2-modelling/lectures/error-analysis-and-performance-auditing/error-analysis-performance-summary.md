# Summary: Error Analysis & Performance Auditing

This document synthesizes the key concepts from the first three lectures on improving model performance through systematic error analysis, handling skewed datasets, and conducting final performance audits.

---

## 1. The Core of Error Analysis: Tagging & Prioritization

Error analysis is the iterative "detective work" that identifies exactly where an algorithm is failing.

### The Investigative Workflow

1.  **Selection:** Sample 100-500 mislabeled examples from your dev set.
2.  **Iterative Tagging:** Categorize errors (e.g., "Car Noise", "Background Chatter") in a spreadsheet. Adjust tags as new patterns emerge.
3.  **Prioritization:** Sum the tags to identify which category offers the most significant potential for overall improvement.

### The Impact Calculation

Focusing on the largest accuracy gap isn't always efficient. You must consider the **prevalence** of the error category.

> **Potential Gain** = `(% of Total Data with Tag)` × `(Accuracy Gap to HLP)`

**Conclusion:** Target categories that are both common and have a large gap to Human-Level Performance (HLP).

---

## 2. Handling Skewed Datasets

In datasets where one class is much more frequent than another (e.g., 99% Negative vs. 1% Positive), raw accuracy is a misleading metric.

### The Confusion Matrix & Key Metrics

|                  | **Actual: 1 (Positive)** | **Actual: 0 (Negative)** |
| ---------------- | ------------------------ | ------------------------ |
| **Predicted: 1** | **True Positive (TP)**   | **False Positive (FP)**  |
| **Predicted: 0** | **False Negative (FN)**  | **True Negative (TN)**   |

- **Precision:** Of all predicted positives, how many were actually positive? ($TP / (TP + FP)$)
- **Recall:** Of all actual positives, how many did we catch? ($TP / (TP + FN)$)
- **F1 Score:** The harmonic mean of Precision and Recall. It penalizes models that have very low performance in either metric.

### Manufacturing & Multi-Class

In domains like manufacturing, **High Recall** is often prioritized to ensure no defects reach the customer, even if it leads to more "false alarms" (lower precision) for human re-inspection.

---

## 3. Performance Auditing & Fairness

Before production deployment, a final audit ensures the model is robust and fair across all segments of the real-world data.

### The 3-Step Audit Framework

1.  **Brainstorm Failure Modes:** Identity how the system might fail (e.g., bias against certain genders or accents).
2.  **Analyze Data Slices:** Evaluate metrics on specific subsets (slices) of data rather than just the aggregate dataset. Tools like _TensorFlow Model Analysis (TFMA)_ help automate this.
3.  **Get Business Buy-In:** Ensure the auditing metrics align with the product's ethical and business standards.

### Ethical & Technical Pitfalls

- **Acoustic/Demographic Bias:** Models may perform differently across user groups or devices.
- **Rude Mistranscriptions:** Critical errors (e.g., mistaking a technical term for an offensive word) are significantly more damaging than "neutral" misses and must be prioritized.

---

## Final Takeaway: The MLOps Loop

Error analysis is not a one-time task but a continuous loop:

1.  **Audit** the model for specific failures.
2.  **Prioritize** based on prevalence and impact.
3.  **Improve Data** specifically for those problematic categories via targeted collection or augmentation.

![ML Cycle](/w2-modelling/lectures/assets/ml-cycle.png)
