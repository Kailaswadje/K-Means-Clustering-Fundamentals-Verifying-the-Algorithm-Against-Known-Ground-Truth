# K-Means Clustering Fundamentals — Verified on Synthetic Ground Truth

A compact, visual demonstration of **K-Means clustering** on synthetic data with *known* structure — 1,000 points generated in 5 clusters via `make_blobs` — so the algorithm's output can be verified against ground truth rather than guessed at.

## Objective

Most clustering tutorials run K-Means on real data where nobody knows the "right" answer. This demo inverts that: by generating data with exactly 5 known centres (`make_blobs`, `random_state=42`), we can check whether K-Means actually *recovers* the true structure — centroids, assignments, and all. It's the cleanest way to build intuition for how the algorithm behaves before trusting it on real data.

## What the Notebook Does

| Step | Detail |
|---|---|
| **Generate** | `make_blobs(n_samples=1000, centers=5, random_state=42)` → 1,000 points in 2-D with 5 true clusters |
| **Fit** | `KMeans(n_clusters=5, random_state=42)` |
| **Extract** | `kmeans.labels_` (cluster assignment for each point) and `kmeans.cluster_centers_` (5 learned centroids) |
| **Visualize** | Scatter plot colour-coded by cluster, with red **✕** markers on the learned centroids |

## Result — Recovered Centroids

K-Means converged on 5 well-separated centroids in the 2-D feature space:

| Cluster | Centroid (x, y) |
|---|---|
| 0 | (−6.69, −6.81) |
| 1 | (2.04, 4.27) |
| 2 | (−2.50, 9.04) |
| 3 | (−8.81, 7.40) |
| 4 | (4.67, 1.87) |

The learned centroids sit at the visual centres of the five generated blobs — the algorithm recovers the known structure, confirmed by the colour-separated scatter plot.

## Key Concepts Demonstrated

- **Centroid-based partitioning** — K-Means alternates between assigning points to their nearest centroid and moving each centroid to its cluster's mean, until assignments stabilize
- **Reproducibility** — fixed `random_state` on both data generation and clustering, since K-Means results depend on centroid initialization
- **Unsupervised evaluation by construction** — synthetic ground truth substitutes for the labels real-world clustering never has

## Known Limitation (by design)

Here *k* = 5 was known in advance. On real data it never is — choosing *k* requires the **elbow method** (within-cluster sum of squares vs *k*) and **silhouette analysis**, which are the planned extensions of this repo, along with a real customer-segmentation dataset.

## Tech Stack

`Python` · `scikit-learn` (KMeans, make_blobs) · `pandas` · `NumPy` · `matplotlib` / `seaborn`

## Repository Structure

```
├── KMeans_Clustering_Demo.ipynb   # Clustering fundamentals notebook
└── README.md
```

## How to Run

```bash
pip install scikit-learn pandas numpy matplotlib seaborn
jupyter notebook KMeans_Clustering_Demo.ipynb
```

---

*Author: Kailas Wadje — MSc Data Science & AI, University of Liverpool*
