# Error Analysis in Machine Learning Development

Error analysis is the heart of the machine learning development process. When done effectively, it guides developers toward the most efficient use of their time by identifying exactly what needs to be improved to boost model performance.

### 1. The "Detective Work" of AI Tagging

Creating tags effectively means categorizing **why** the algorithm failed. Think of yourself as a detective investigating AI failures; instead of just saying "it made a mistake," you open a spreadsheet and log the specific cause for each case. Those "tags" are the columns in your investigation.

The process follows three simple steps:

1.  **Review:** Examine the mislabeled example (e.g., listen to the audio or view the image).
2.  **Identify:** Determine the specific problem (e.g., car noise, background chatter, or a strong accent).
3.  **Tag:** Mark the error in the corresponding column of your spreadsheet.

![Speech Recognition Error Analysis Example](/w2-modelling/lectures/assets/speech-recog-example.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

While manual review provides the **initial intuition**, emerging MLOps tools eventually allow developers to scale these findings to thousands of examples.

### 2. The Investigative Workflow

Instead of just noting that the AI failed, you must investigate **why**. The standard workflow for an engineer follows these stages:

1.  **Selection:** Take a random sample (typically 100-500 examples) of mislabeled data from your dev set.
2.  **Iterative Tagging:** Start with a few initial tags. If you spot a new pattern—like "Quiet Audio"—create a new column and re-evaluate previous examples.
3.  **Prioritization:** Sum the tags to see the big picture. If 40% of errors are due to a specific issue, focus the team's efforts there for the next cycle.

### 3. Metrics for Strategic Decisions

The goal of tagging is to produce actionable data. To decide which error category to tackle first, evaluate these key metrics:

- **Fraction of Errors with Tag:** What is the maximum possible improvement if this issue is resolved?
- **Misclassification Rate per Tag:** Indicates the difficulty of that specific segment.
- **Prevalence & Difficulty:** How common is this tag in the overall dataset?
- **Room for Improvement:** Comparison between model performance and human-level performance (HLP).

### 4. Prioritizing Improvements: The Impact Calculation

Identifying a large gap to HLP in a specific category doesn't always make it the top priority. To maximize efficiency, you must consider the **prevalence** of that category to determine its potential impact on overall accuracy.

- **Formula for Potential Gain:** `(% of Total Data with Tag)` × `(Accuracy Gap to HLP)`.
- **Case Study Example:**
  - **Clean Speech:** 60% of data with a 1% gap to HLP → **0.60%** potential overall improvement.
  - **Car Noise:** 4% of data with a 4% gap to HLP → **0.16%** potential overall improvement.
- **Insight:** Even if the "Car Noise" gap is larger, focusing on "Clean Speech" yields a much higher net gain for the total system due to its frequency.

### 5. Multi-Factor Prioritization

Beyond the math, three other factors should influence your decision:

- **Ease of Improvement:** Do you have clear ideas (e.g., data augmentation) to fix this specific category?
- **Category Importance:** Is performance in this segment critical for the user? (e.g., search functionality while driving).
- **Resource Efficiency:** Targeted data collection is often cheaper and faster than a generic "more data" approach.

### 6. Targeted Data Improvement

Once a category is prioritized, the goal is to improve the data quality for just that segment:

- **Focused Collection:** Target only the prioritized tags (e.g., collecting more "People Noise" samples).
- **Data Augmentation:** Generate more training examples for the specific problematic category.

![ML Cycle](/w2-modelling/lectures/assets/ml-cycle.png)

_Source: [Machine Learning in production by Andrew Ng - DeepLearning.AI](https://www.deeplearning.ai/courses/machine-learning-in-production/)_

- **Efficiency:** This focused iterative loop ensures you are not wasting time on segments that won't significantly move the needle.

---

Next, one of the most common challenges we run into is skewed data sets. Let's go on to the next lecture to go through some techniques for managing skewed data sets.
