# Balanced Train/Dev/Test Splits

When working with limited data, the standard practice of random splitting can lead to significant problems. This lecture explains why **balanced splits** are essential for small data problems.

## 1. The Risk of Random Splitting in Small Data

In large-scale machine learning, random splits are usually representative of the true data distribution due to the volume of examples. However, in "small data" regimes:

- **Non-Representative Splits:** By pure chance, a small dev or test set might end up with a disproportionately low (or high) number of positive examples.
- **Example:** If a dataset of 100 images has 30% defects, a random 20% dev split could easily end up with only 10% defects (2 images) instead of the expected 6.
- **Unreliable Metrics:** When a dev set is non-representative, it becomes an unreliable measure of your model's actual performance, potentially leading you to make poor project decisions.

## 2. The Solution: Balanced Splits (Stratification)

For small datasets, you should explicitly ensure that each split (Train, Dev, and Test) maintains the same class distribution as the original dataset.

- **Goal:** If your overall data is 30% positive, ensure train, dev, and test are each exactly 30% positive.
- **Benefit:** This makes your performance metrics much more stable and representative of the "real world," providing a clearer signal for machine learning development.

## 3. Summary of the Data Section

This concludes the deep dive into the **Data** portion of the MLOps lifecycle. You have now covered:

1.  **Modeling:** Selecting and tuning algorithms.
2.  **Deployment:** Taking models into production.
3.  **Data:** Defining, acquiring, cleaning, and organizing high-quality data.

_A final optional section on **Scoping**—how to select the right projects to work on—is available for those who want to complete the full series._
