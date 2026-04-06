# Error Analysis & Performance Metrics for Skewed Datasets

When working with datasets where the ratio of positive to negative examples is heavily imbalanced (e.g., 99.7% vs 0.3%), **raw accuracy** is a misleading metric. A model that always predicts "negative" would achieve 99.7% accuracy but fail to detect any actual cases of interest.

## 1. The Confusion Matrix

To properly evaluate imbalanced data, we use a confusion matrix to categorize predictions into four buckets:

![Confusion Matrix](/w2-modelling/lectures/assets/confusion-matrix.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

|                  | **Actual: 0 (Negative)** | **Actual: 1 (Positive)** |
| ---------------- | ------------------------ | ------------------------ |
| **Predicted: 0** | **True Negative (TN)**   | **False Negative (FN)**  |
| **Predicted: 1** | **False Positive (FP)**  | **True Positive (TP)**   |

- **True Negatives (TN):** Correctly predicted negative.
- **True Positives (TP):** Correctly predicted positive.
- **False Negatives (FN):** Predicted negative, but was actually positive (Misses).
- **False Positives (FP):** Predicted positive, but was actually negative (False alarms).

---

## 2. Key Performance Metrics

Precision and Recall offer a more nuanced view of model performance than simple accuracy.

### Precision

**Definition:** Of all examples the algorithm predicted as positive, what fraction were actually positive?

> **Formula:** $Precision = \frac{TP}{TP + FP}$

### Recall

**Definition:** Of all actual positive examples, what fraction did the algorithm successfully catch?

> **Formula:** $Recall = \frac{TP}{TP + FN}$

### F1 Score

A single-number metric that combines Precision and Recall using their **harmonic mean**. It is particularly useful because it heavily penalizes the total score if either Precision or Recall is very low.

> **Formula:** $F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$

---

## 3. Application in Multi-Class & Manufacturing

In fields like manufacturing (e.g., detecting defects in smartphones), multiple rare classes may exist (scratches, dents, pits).

![Multi-Class Error Analysis](/w2-modelling/lectures/assets/multiclass-metrics.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_


- **Prioritizing Recall:** Factories often emphasize **high recall** because letting a defective product reach a customer is much costlier than a human re-examining a "false alarm" (False Positive).
- **Benchmarking:** F1 scores can be calculated for each defect type individually to benchmark against human-level performance and prioritize which area needs the most improvement.

---

## Conclusion: Performance Auditing

Beyond tracking metrics, the final step before production deployment is **Performance Auditing**. This ensures the algorithm is robust enough for real-world application, which we will explore next.
