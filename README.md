This README covers the implementation of MinHash and Locality Sensitive Hashing (LSH) for document similarity and movie recommendation systems as found in my repository.

 MinHash and LSH Similarity Analysis

This repository contains Python implementations of MinHash and Locality Sensitive Hashing (LSH) applied to two distinct datasets: a collection of text documents and the MovieLens 100k dataset. The goal is to efficiently estimate Jaccard similarity and find similar items without exhaustive pairwise comparisons.

 Project Structure

script.py`: Handles text document analysis using k-grams, MinHash signatures, and LSH probability calculations.
movie_minhash.py: Implements MinHash on the MovieLens 100k dataset to find similar users based on their movie ratings.
movie_lsh.py`: Implements LSH on the MovieLens dataset to further optimize the search for similar users using bands and rows.
minhash/: Directory containing the source text documents (`D1.txt` through `D4.txt`).
results/: Contains summary logs (`movielens_minhash_summary.txt`, `movielens_lsh_summary.txt`) and generated lists of similar pairs.

 Key Components

 1. Text Document Similarity (`script.py`)

This script performs granular analysis on four text documents:

K-Grams: Generates character-level (2-gram, 3-gram) and word-level (2-gram) representations.
Exact Jaccard: Calculates the ground-truth similarity for all document pairs.
MinHash Approximation: Estimates similarity using signature lengths ranging from $t=20$ to $t=600$.
LSH Strategy: Determines the optimal number of rows ($r$) and bands ($b$) for a specific similarity threshold ($\tau=0.7$).

2. MovieLens User Similarity (`movie_minhash.py` & `movie_lsh.py`)

These scripts analyze user behavior in the MovieLens 100k dataset:

Dataset: Uses `u.data` containing user-movie interactions.
MinHash Performance: Evaluates the impact of signature sizes ($t=50, 100, 200$) on False Positives (FP) and False Negatives (FN).
LSH Configuration: Tests multiple $(t, r, b)$ configurations to find the most efficient balance for thresholds of $0.6$ and $0.8$.

 Results Summary

 MovieLens MinHash Analysis (Threshold 0.5)

As the signature length ($t$) increases, the number of False Positives significantly decreases, improving accuracy:

$t=50$: Avg FP: 129.80 | Avg FN: 2.40
$t=100$: Avg FP: 25.80 | Avg FN: 3.20
$t=200$: Avg FP: 5.80 | Avg FN: 2.80

 MovieLens LSH Analysis (Threshold 0.6)

LSH configurations provide a way to filter candidates efficiently:

Config $t=100, r=5, b=20$: Achieved a low error rate with Avg FP of 0.60 and Avg FN of 0.20.
Config $t=200, r=10, b=20$: Reduced False Positives to 0.00, though False Negatives increased to 1.60.

How to Run

1. Data Setup: Ensure the MovieLens 100k dataset is placed at `data/ml-100k/u.data`.
2. Run Document Analysis:
```bash
python script.py

```


3. Run MovieLens MinHash:
```bash
python movie_minhash.py

```


4. Run MovieLens LSH:
```bash
python movie_lsh.py

```
