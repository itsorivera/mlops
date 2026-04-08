# Does Adding Data Ever Hurt Performance?

This lecture explores whether adding data (especially through augmentation) can negatively impact a model, focusing on the relationship between data distribution, model capacity, and label ambiguity.

## 1. The General Rule for Unstructured Data

For unstructured data (images, audio, etc.), adding accurately labeled data **rarely hurts performance**, even if it skews the training distribution significantly away from the dev/test sets.

### Conditions for Safety:

1.  **Large Model Capacity**: The model (e.g., a large neural network) must be big enough to learn from a diverse set of data sources without "forgetting" or being overwhelmed by the new distribution.
2.  **Clear $X \rightarrow Y$ Mapping**: Humans must be able to make an accurate prediction given only the input $X$.

## 2. When Adding Data _Can_ Hurt (Rare Cases)

Adding data can be counterproductive in rare "corner cases" where the mapping from $X$ to $Y$ is ambiguous.

### The OCR Example ("1" vs "I")

- **The Scenario**: In Google Street View house numbers, "1" is significantly more common than the letter "I".
- **The Ambiguity**: Some images are visually identical for both "1" and "I".
- **The Risk**: If you use data augmentation to add a massive amount of "I" examples, you skew the model's prior. In the real world (dev/test set), an ambiguous image is almost certainly a "1", but a model trained on skewed data might incorrectly guess "I".

![OCR Example](/w2-modelling/lectures/assets/ocr-example.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

> [!NOTE]
> This is rare. Most practical problems have clear mappings where humans don't struggle with ambiguity.

## 3. Training vs. Dev/Test Distributions

- It is common for the training set distribution ($P(X)$) to differ from the dev/test sets after targeted augmentation (e.g., training becomes 50% "cafe noise" while dev set is only 20%).
- As long as the model has **large capacity**, it can learn to perform well on both the augmented categories and the original categories simultaneously.

## 4. Key Takeaways

- **Confidence in Augmentation**: You should feel comfortable using augmentation to improve performance on specific tags identified in error analysis.
- **Model Size Matters**: Ensure your model is large enough to absorb the extra data.
- **Unstructured Priority**: These rules primarily apply to unstructured data. Structured data requires different strategies.

---

**Next Step:** Techniques for improving data iteration in **Structured Data** problems.
