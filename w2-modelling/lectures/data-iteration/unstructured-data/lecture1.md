# Data-Centric AI Development: Improving Performance

This lecture discusses the shift from a model-centric to a data-centric approach in AI development and provides a conceptual framework for improving model performance through targeted data improvement.

## 1. Model-Centric vs. Data-Centric AI

| Approach          | Focus            | Strategy                                           | Context                                     |
| :---------------- | :--------------- | :------------------------------------------------- | :------------------------------------------ |
| **Model-Centric** | The Algorithm    | Hold data fixed, iteratively improve code/model.   | Common in academic research (benchmarks).   |
| **Data-Centric**  | The Data Quality | Hold code fixed, iteratively improve data quality. | Effective for many real-world applications. |

> [!TIP]
> If your data is high quality, multiple models will often perform well. Instead of searching for the "perfect" architecture, focus on making your dataset better.

## 2. Improving Data Quality

Systematic improvement is achieved by:

- **Error Analysis:** Identifying specific categories or tags where the model underperforms (e.g., "speech with cafe noise").
- **Data Augmentation:** Synthetically creating more data for those specific problem areas.
- **Data Collection:** Specifically gathering more real-world examples for the identified tags.

## 3. The Rubber Sheet Analogy

Performance across different input types can be visualized as a **"rubber sheet"** or rubber band:

- **The Visualization:** The vertical axis is performance (accuracy), and the horizontal axis represents the space of possible inputs (e.g., car noise, cafe noise, library noise).
- **Pulling the Sheet:** When you add more data for a specific category (e.g., "cafe noise"), you are "pulling up" that point on the rubber sheet toward **Human-Level Performance (HLP)**.
- **Generalization:** Pulling up one point tends to pull up performance for _nearby_ (similar) points as well (e.g., improving "cafe noise" likely improves "library noise").
- **Minimal Regressions:** For unstructured data, improving one area is unlikely to significantly degrade performance in far-away, unrelated areas.

![Model Performance vs Human Level Performance](/w2-modelling/lectures/assets/model-vs-hlp.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

## 4. The Iterative Process

1.  **Perform Error Analysis:** Locate the biggest gap between current model performance and HLP.
2.  **Target the Gap:** Use data augmentation or collection to "pull up" the rubber sheet at that specific location.
3.  **Repeat:** As performance improves, the "biggest gap" will shift to a new category. Use error analysis again to identify the next priority.

---

**Next Step:** Learn specific techniques and best practices for **Data Augmentation**.
