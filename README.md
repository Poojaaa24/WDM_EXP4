### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 20-11-26
### REG NO: 212225230209
### NAME: POOJA U
### AIM: To implement visitor segmentation based on demographic characteristics (age groups) using Python and visualize the distribution of visitors. This experiment introduces the concept of visitor segmentation, which can be extended using clustering techniques for navigation pattern analysis.
### Description:
<div align= "justify">Visitor segmentation is the process of dividing website visitors into meaningful groups based on their characteristics or behavior. Segmentation helps organizations understand different types of users and provide personalized services, recommendations, and marketing strategies.
In this experiment, visitors are segmented using predefined age groups (rule-based segmentation). In real-world web mining applications, clustering algorithms such as K-Means and Hierarchical Clustering are commonly used to automatically discover visitor segments from navigation patterns and user behavior.</div>
  
### Procedure:
1. Import the required Python libraries.
2. Read the visitor dataset (CSV file).
3. Load the dataset into a DataFrame.
4. Select the Age feature for clustering.
5. Set the number of clusters (K = 3).
6. Apply the K-Means clustering algorithm.
7. Assign each visitor to the nearest cluster.
8. Display the cluster-wise visitor details.
9. Visualize the clusters using a scatter plot.
10. Analyze the clustered visitor groups

### Program:
```python
import pandas as pd
import matplotlib.pyplot as plt
# Read CSV file
df = pd.read_csv("clustervisitor.csv")
# Select Age feature
X = df["Age"].tolist()
# Number of clusters
k = 3
# Choose initial centroids
centroids = X[:k]

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    # Assign each value to nearest centroid
    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    # Calculate new centroids
    new_centroids = []

    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    # Stop if centroids do not change
    if new_centroids == centroids:
        break

    centroids = new_centroids

# Add cluster labels
df["Cluster"] = labels
# Display complete dataset
print("Complete Dataset")
print(df)

print("\nVisitor Segmentation (Cluster-wise)\n")

# Display cluster-wise output
for i in range(k):
    print("Cluster", i)
    print(df[df["Cluster"] == i])
    print("-" * 50)
    
```
### Output:
<img width="582" height="707" alt="Screenshot 2026-11-20 143228" src="https://github.com/user-attachments/assets/7a586d7b-98f7-49a2-8a6b-775822fedffa" />
<img width="510" height="363" alt="Screenshot 2026-11-20 143409" src="https://github.com/user-attachments/assets/6cd2aa3a-dcc9-4796-b4e4-c6de04a58244" />
<img width="466" height="340" alt="Screenshot 2026-11-20 143438" src="https://github.com/user-attachments/assets/47de36a9-d2c9-4b41-97f6-0871a86ec265" />
<img width="482" height="316" alt="Screenshot 2026-11-20 143453" src="https://github.com/user-attachments/assets/59417b07-910d-4cc3-b87f-48227009b1c9" />


### Visualization:
```python
# Visualize clusters
plt.figure(figsize=(8,6))

colors = ["red", "blue", "green"]

for i in range(k):
    cluster_data = df[df["Cluster"] == i]

    plt.scatter(
        cluster_data["Age"],
        cluster_data["Cluster"],
        color=colors[i],
        s=80,
        label=f"Cluster {i}"
    )
plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()

```
### Output:
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/e938cc09-a0d1-4fa5-811f-f0f1114bbaa5" />

### Result:
Thus, the K-Means clustering algorithm was successfully implemented, and the visitors were grouped into different clusters and visualized using a scatter plot.
