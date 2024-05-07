# Semi-Supervised Learning

Supervised learning relies on labelled data, yet a vast majority of available data remains unlabeled. Labelling data is a resource-intensive task that demands considerable time and effort.

### Insights from Unlabeled Data

Unlabeled data, while lacking explicit annotations, still holds valuable insights. By leveraging *unsupervised learning* techniques, such as clustering, we can uncover underlying structures within the data. For instance, clustering algorithms group similar data points together, implicitly suggesting potential class memberships.

In clustering, each cluster may represent a distinct class, with the centroids serving as prototypical representations of these classes. Given the assumption that data points within the same cluster share similar characteristics, we can infer the likely class label for unlabeled data points based on their proximity to cluster centroids.

### Leveraging Unlabeled Data for Labeling Strategies

With this knowledge in mind, we can devise strategies for efficiently labelling a subset of the dataset rather than random selection, we can prioritize sampling examples from each identified cluster, ensuring a diverse representation of classes in the labelled subset.

### Datasets used
1) [fashion-mnist-dataset](https://www.kaggle.com/datasets/zalando-research/fashionmnist)
2) [overhead-mnist-dataset](https://www.kaggle.com/datasets/datamunge/overheadmnist)

### Experiment Setup

To validate the effectiveness of this approach, we conducted the following experiment:

1. **Benchmark Training:** We initially trained an `MLPClassifier` on the entire dataset for benchmarking purposes.
  
2. **Clustering and Single training example:** Next, we applied clustering to the dataset and selected the nearest data point to each cluster centroid as labelled training data. We trained on this dataset.

3. **Label Propagation to the whole dataset:**  We propagated these cluster labels to the entire dataset. And train a model on this dataset.

4. **Partial Label Propagation:** Additionally, we propagated cluster labels to only 25% of the clustered dataset and trained the model on this subset.

In each training scenario, we only utilized a limited number of labelled examples (equal to the number of clusters) to assess the performance improvement.

By strategically leveraging clustering and label propagation techniques, we achieved noteworthy enhancements in model performance while minimizing the labelling effort required for supervised learning tasks.

#### **NOTE**
We observed improved results when propagating labels to only $25\%$ of the cluster examples. This phenomenon can be attributed to the nature of clustering, where each cluster represents examples from the same class. However, it's important to note that clusters may contain a small proportion of examples from other classes as well.

By limiting label propagation to only a quarter of the clustered dataset, we ensure a purer split that better captures the intrinsic class structure within the data. This selective approach prevents potential contamination from examples of other classes that might exist within the clusters, thereby leading to more accurate and effective labelling.
