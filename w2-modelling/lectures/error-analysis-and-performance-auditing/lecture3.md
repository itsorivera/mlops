# Performance Auditing & Fairness in ML

Even if an algorithm performs well on aggregate metrics (Accuracy, F1), a final **Performance Audit** is essential before production deployment to prevent post-deployment issues and ensure fairness.

![ML Cycle](/w2-modelling/lectures/assets/mlcycle.png)
_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

## 1. Performance Auditing Framework

A structured audit follows three main steps:

1.  **Brainstorm failure modes**: Identify what could go wrong.
    - Does it fail on specific subsets (e.g., certain genders or ethnicities)?
    - Does it produce problematic false positives/negatives?
    - How does it handle rare but critical classes?
2.  **Establish Metrics for Data Slices**: Instead of looking at the whole dataset, analyze performance on specific "slices" (e.g., only "scratch" defects or only "users with accents").
    - **Automation:** Tools like _TensorFlow Model Analysis (TFMA)_ can automate this by triggering evaluations on predefined slices for every new model.
3.  **Get Business Buy-In**: Consult with product owners to ensure the metrics and prioritized issues align with business goals and ethical standards.

---

## 2. Case Study: Speech Recognition Errors

A speech system may have high overall accuracy but fail in specific ways:

- **Acoustic Variability:** Poor performance on certain devices or microphones.
- **Demographic Bias:** Mistakes across different accents, genders, or ethnicities.
- **Rude Mistranscriptions:** A critical failure where a technical term is mistranscribed as an offensive word (e.g., mistaking _"GANs"_ for _"guns"_ or _"gangs"_), which can be much more damaging than a neutral error.

---

## 3. Best Practices for High-Stakes Applications

- **Collaboration:** High-stakes systems benefit from multi-person brainstorming (including external advisors) to catch blind spots.
- **Evolution of Standards:** Standards for fairness and bias are constantly evolving. It is crucial to stay current with industry-specific norms.
- **Proactive Solving:** Identify and solve these issues _before_ deployment to avoid "unpleasant surprises" and legal or ethical repercussions later.

---

> **Summary:** Performance auditing moves beyond simple numbers to ensure a system is robust, fair, and reliable across all segments of the real world.
