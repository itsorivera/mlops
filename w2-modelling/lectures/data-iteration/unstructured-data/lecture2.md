# Data Augmentation and Data Iteration

This lecture covers best practices for data augmentation and introduces the concept of the "Data Iteration Loop" as a more efficient way to improve model performance.

## 1. Data Augmentation for Unstructured Data

Data augmentation is highly efficient for unstructured data like images, audio, and text.

- **Audio**: Create synthetic examples by summing original speech waveforms with background noise (cafe, music, etc.).
- **Images**:
  - **Geometric**: Flipping horizontally.
  - **Photometric**: Adjusting contrast or brightness.
  - **Synthetic Features**: Manually adding artifacts (e.g., using Photoshop to draw a realistic scratch on a phone image).
  - **Advanced**: Using GANs (though often "overkill" compared to simpler methods).

## 2. The Systematic Decision Framework

Avoid inefficient "trial and error" training. Before adding augmented data to your training set, verify it against this checklist:

![Image Example](/w2-modelling/lectures/assets/image-example.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_
1.  **Realistic?**: Does the augmented data look or sound like real-world inputs?
2.  **Clear X $\rightarrow$ Y Mapping?**: Can a human (or baseline) still easily determine the correct label?
    - _Example_: If an image is too dark for a human to see the scratch, it is not a useful training example.
3.  **Algorithm Failure?**: Does the model currently perform poorly on these types of examples?
    - If the model already succeeds, there is less for it to learn. Focus on examples that bridge the gap to human performance.

## 3. Data Iteration Loop

While academic machine learning often focuses on **Model Iteration**, production MLOps benefits significantly from **Data Iteration**.

| Loop Type           | Focus             | Process                                                                          |
| :------------------ | :---------------- | :------------------------------------------------------------------------------- |
| **Model Iteration** | Architecture/Code | Change model $\rightarrow$ Train $\rightarrow$ Error Analysis                    |
| **Data Iteration**  | Dataset Quality   | Error Analysis $\rightarrow$ Target Data (Augment/Collect) $\rightarrow$ Retrain |

> [!IMPORTANT]
> The **Data Iteration Loop** is often the fastest path to improvement. Instead of changing the model, focus on iteratively adding or improving data for categories identified by error analysis.

## 4. Key Takeaways

- Targeted augmentation is more effective than random data increases.
- For unstructured data, adding more (high-quality) data rarely hurts performance.
- Synthesizing data that is "hard but possible" for humans is the most efficient way to "pull up" the performance rubber sheet.

---

**Next Step:** Explore whether adding data can ever hurt model performance.
