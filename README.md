
# FP-Growth for Association Rule Mining

This project demonstrates the application of **FP-Growth** (Frequent Pattern Growth) for **market basket analysis** using a transactional dataset. The goal is to uncover frequent itemsets (groups of items that frequently appear together), which can help businesses make informed decisions on product placement, promotions, and recommendations.

## Project Overview

In this project, I worked with a transactional dataset that contains information about grocery items purchased together in various transactions. The aim was to analyze the data using the **FP-Growth** algorithm to find frequent itemsets and generate **association rules**.

### Why FP-Growth?

FP-Growth was chosen for its efficiency in mining large datasets. Unlike the **Apriori** algorithm, which generates candidate itemsets and scans the dataset multiple times, **FP-Growth** constructs a **compact FP-Tree**, which allows for faster mining of frequent itemsets.

### Key Benefits of FP-Growth:
- **Efficiency**: Avoids candidate itemsets, reducing computational overhead.
- **Scalability**: Suitable for large datasets.
- **Compact Representation**: Stores frequent patterns in a compact tree structure.

### Drawbacks of FP-Growth:
- **Memory Intensive**: The FP-Tree can grow large if the dataset contains many frequent patterns.
- **Complexity in Implementation**: Building and mining the FP-Tree can be more complex compared to simpler methods like Apriori.

## Tools Used

- **mlxtend**: A library that provides an efficient implementation of the FP-Growth algorithm.
- **pandas**: A powerful data manipulation library used to convert the dataset into a **one-hot encoded format**.

## Steps

### 1. Data Preprocessing: One-Hot Encoding

To prepare the dataset for FP-Growth, each item in the transactions was represented as a binary feature (1 if present, 0 if absent). Below is an example of the one-hot encoded dataset:

```
Ghee | Coffee Powder | Butter | Yogurt | Cheese
-----------------------------------------------
 1   |       1        |   0    |    0   |    0
 0   |       1        |   1    |    1   |    0
 0   |       0        |   1    |    0   |    1
```

### 2. Mining Frequent Itemsets with FP-Growth

The `fpgrowth` function from **mlxtend** was used to mine frequent itemsets from the one-hot encoded transaction data. The minimum support threshold was set to **0.2**, meaning only itemsets appearing in at least 20% of the transactions were considered frequent.

```python
from mlxtend.frequent_patterns import fpgrowth
frequent_itemsets = fpgrowth(transaction_data, min_support=0.2, use_colnames=True)
```

### 3. Generating Association Rules

Once the frequent itemsets were mined, the next step was to generate **association rules** using the **confidence** metric. The minimum confidence threshold was set to **0.7**, meaning that the confidence of the rules must be at least 70%.

```python
from mlxtend.frequent_patterns import association_rules
rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=0.7)
```

## Key Concepts

- **Support**: The frequency of an itemset appearing in the dataset. It is calculated as the ratio of transactions containing the itemset to the total number of transactions.
- **Confidence**: The probability that item B appears in a transaction, given that item A is already present. It is calculated as:

  \[
  Confidence(A \to B) = \frac{Support(A \cup B)}{Support(A)}
  \]

- **FP-Tree**: A compact tree structure used in FP-Growth to store the frequent itemsets, which helps reduce the number of dataset scans.

## Example Results

After mining frequent itemsets and generating association rules, the following were the results:

- Frequent Itemsets:
  - Ghee
  - Coffee Powder
  - Cheese
  - Butter

- Sample Association Rules:
  - **(Coffee Powder) → (Ghee)**: Confidence = 0.65, Support = 0.23
  - **(Butter) → (Cheese)**: Confidence = 0.74, Support = 0.35

## Conclusion

FP-Growth proved to be an efficient method for extracting frequent itemsets and generating association rules from the transactional dataset. The insights derived from this process are valuable for **market basket analysis**, product recommendations, and sales strategies.
