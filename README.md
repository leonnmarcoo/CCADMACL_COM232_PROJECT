<div align="center">
  <h1>🎬 From Indie to Blockbuster</h1>
</div>

> **What kinds of movies are out there?**  
> Sorting 4,765 films into groups with K-Means, hierarchical clustering, and Gaussian mixtures, no labels required.

---

## 🍿 What Is This Project?

This is an unsupervised machine learning study of a Kaggle movie dataset. Instead of predicting anything, it asks the data to group itself, then compares three clustering algorithms to see which one does it best. The full write-up is in **[Final_Paper.pdf](Final_Paper.pdf)**, _From Indie to Blockbuster Films: A Clustering-Based Analysis of Movie Characteristics_.

---

## 🔬 The Pipeline

**1. Clean (`data_preprocessing.ipynb`)**
Starts from 4,803 movies and 24 columns. It explores genres, languages, studios, countries, cast, and directors, then drops them because they're imbalanced and create too many columns once one-hot encoded. `homepage` becomes a simple yes/no.

**2. Explore and scale (`eda.ipynb`)**
Log-transforms the skewed columns, turns release date into `Age_of_Movie`, removes zero-length movies and anything over 300 minutes, and standardizes budget, popularity, revenue, runtime, and vote average. That leaves **4,765 movies and 8 features**.

**3. Cluster (`model_training.ipynb`)**
Reduces the features to two principal components, which keep 98.2% of the variance, then fits and compares:

- 📍 **K-Means** with 5 clusters, chosen with the elbow method
- 🌳 **Hierarchical clustering** (Ward linkage) with 3 clusters, chosen from the dendrogram
- 🔔 **Gaussian Mixture Model** with 3 components

---

## 🏆 Results

| Model | Clusters | Silhouette ↑ | Davies-Bouldin ↓ | Calinski-Harabasz ↑ |
| --- | --- | --- | --- | --- |
| K-Means | 5 | 0.4144 | 0.7078 | **9858.89** |
| Hierarchical | 3 | 0.4429 | 0.6827 | 6530.04 |
| **GMM** | 3 | **0.4750** | **0.6824** | 7120.97 |

**GMM wins** on two of the three metrics, so it's the model the study interprets. Its three clusters line up with three eras of film:

| Cluster | Movies | Average age | Character |
| --- | --- | --- | --- |
| 🎞️ **Classic Acclaimed Cinema** | 576 (12%) | 50 years | Older, longer, and higher rated |
| 🎬 **Mid-Era Balanced Films** | 1,976 (41%) | 25 years | Moderate across the board |
| 🍿 **Modern Commercial Blockbusters** | 2,213 (46%) | 15 years | Recent, popular, and heavily marketed |

> 📝 **Why eras?** `Age_of_Movie` wasn't standardized, so its range (9 to 110) dwarfs the other features. That makes the first principal component almost entirely movie age, and it's why the clusters split so cleanly by era.

---

## 🛠️ Tech Stack

| | |
| --- | --- |
| **Language** | Python |
| **Data** | pandas and NumPy |
| **Modeling** | scikit-learn and SciPy |
| **Charts** | Matplotlib and seaborn |
| **Environment** | Jupyter or Google Colab |

---

## 🚀 How to Run

There's no `requirements.txt` here, so install the packages directly:

```bash
git clone https://github.com/leonnmarcoo/CCADMACL_COM232_PROJECT.git
cd CCADMACL_COM232_PROJECT
python3 -m venv .venv
source .venv/bin/activate
pip install numpy pandas matplotlib seaborn scikit-learn scipy notebook
jupyter notebook
```

Run the notebooks in order: `data_preprocessing.ipynb`, `eda.ipynb`, then `model_training.ipynb`. Each one saves the CSV the next one needs, and those CSVs are already in the repo, so you can also jump straight to any notebook.

Prefer the cloud? Each notebook has an **Open in Colab** badge at the top. Upload the CSV it reads into your Colab session first.

---

## 🗂️ What's in Here

| File | What it is |
| --- | --- |
| `movie_dataset.csv` | The original dataset, from Kaggle: [Movies Dataset](https://www.kaggle.com/datasets/utkarshx27/movies-dataset) |
| `cleaned_data.csv` | Output of the cleaning notebook |
| `standardized_data.csv` | Output of the EDA notebook, used for clustering |
| `Final_Paper.pdf` | The final research paper |
| `Paper.pdf` | An earlier draft of the paper |

---

## 🤝 Authors

**Leon Marco Devela** and **Rae Paulos**, College of Computing and Information Technologies, National University, Manila.
