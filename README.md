# KMeans vs DBSCAN — Clustering Shape Comparison

A visual comparison of **KMeans** and **DBSCAN** clustering algorithms
across three datasets with different geometric structures,
demonstrating where each algorithm succeeds and fails.

---

## Datasets

| File | Features | Shape |
|------|----------|-------|
| `cluster_data.csv` | `Feature 1`, `Feature 2` | Blobs (globular clusters) |
| `cluster_moons.csv` | `X1`, `X2` | Two crescent moon shapes |
| `circles.csv` | `x`, `y` | Concentric circles |

---

## Raw Data Visualizations

- **Blobs** — 3 well-separated globular clusters
- **Moons** — two interleaved crescent shapes
- **Circles** — concentric ring structures

---

## KMeans Results

### Blobs — ✅ Works Well
```python
KMeans(n_clusters=3)
```
> KMeans correctly separates the 3 compact, globular clusters.
> This is the ideal use case for KMeans.

---

### Moons — ❌ Fails
```python
KMeans(n_clusters=2)
```
> KMeans draws straight linear boundaries — it cannot capture
> the curved crescent shapes. Both moons get incorrectly split.

---

### Circles — ❌ Fails
```python
KMeans(n_clusters=2)
```
> KMeans splits the circles into left/right halves instead of
> inner/outer rings. The algorithm has no concept of density or shape.

---

## DBSCAN Results

### Blobs — ✅ Works Well
```python
DBSCAN()  # default eps=0.5, min_samples=5
```
> DBSCAN correctly identifies the 3 clusters using density.
> Works well here since clusters are compact and well-separated.

---

### Moons — ✅ Works Well
```python
DBSCAN(eps=0.15)
```
> DBSCAN follows the density of each crescent and correctly
> separates both moon shapes — something KMeans cannot do.

---

### Circles — ✅ Works Well
```python
DBSCAN(eps=0.15)
```
> DBSCAN traces the ring structures by density and correctly
> identifies the concentric circles as separate clusters.

---

## Summary Comparison

| Dataset | KMeans | DBSCAN |
|---------|--------|--------|
| Blobs | ✅ Correct | ✅ Correct |
| Moons | ❌ Wrong | ✅ Correct |
| Circles | ❌ Wrong | ✅ Correct |

---

## Libraries Used

- `numpy`, `pandas` — data handling
- `matplotlib`, `seaborn` — scatterplot visualization
- `scikit-learn`:
  - `KMeans` — centroid-based clustering
  - `DBSCAN` — density-based clustering

---

## Key Takeaways

> **KMeans** assumes clusters are convex and roughly equal in size.
> It draws straight boundaries between centroids — it will always
> fail on curved or ring-shaped data no matter how you tune K.

> **DBSCAN** makes no shape assumptions — it groups points
> by density, so it naturally handles curves, rings, and
> irregular shapes that KMeans cannot.

> **Choosing between them:**
> - Use **KMeans** when you expect compact, globular clusters
>   and need to specify the number of clusters in advance.
> - Use **DBSCAN** when cluster shapes are unknown, irregular,
>   or when you need automatic outlier detection.
