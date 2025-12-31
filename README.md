# London Bike Sharing Network Analysis

Analyse statistique et machine learning d'un réseau de 777 stations de vélos en libre-service à Londres

## Table des matières

- [À propos](#à-propos)
- [Contexte du projet](#contexte-du-projet)
- [Méthodologie](#méthodologie)
- [Structure du projet](#structure-du-projet)
- [Technologies](#technologies)
- [Résultats](#résultats)

## À propos

Ce projet analyse le réseau de stations de vélos en libre-service de Londres en combinant théorie des graphes, statistique et machine learning. L'objectif est de découvrir la structure latente du réseau et d'identifier des groupes de stations ayant des comportements similaires.

### Caractéristiques principales

- 777 stations géolocalisées à Londres
- Analyse de réseau via matrice de connectivité
- Réduction de dimension avec ACP probabiliste
- Clustering via K-means et GMM
- Modélisation probabiliste avec variables latentes

## Contexte du projet

Le système de vélos partagés de Londres génère des milliers de trajets quotidiens. Ce projet vise à :

1. Modéliser les interactions entre stations via une matrice de connectivité de dimension $777 \times 777$
2. Découvrir une représentation latente $\mathbf{Z}$ pour chaque station dans $\mathbb{R}^d$
3. Identifier des clusters de stations ayant des profils d'utilisation similaires
4. Interpréter géographiquement les résultats obtenus

### Hypothèses

- La matrice $\mathbf{A}$ est symétrique : $A_{ij} = A_{ji}$
- Pas d'auto-boucles : $A_{ii} = 0$
- Les interactions dépendent de la distance latente entre stations

## Méthodologie

### 1. Construction de la matrice de connectivité

$A_{ij}$ représente le nombre de trajets de la station $i$ vers la station $j$

### 2. Matrice binaire d'adjacence

$$A_{ij}^{\text{binaire}} = \begin{cases} 1 & \text{si } A_{ij} > 0 \\ 0 & \text{sinon} \end{cases}$$

### 3. Réduction de dimension

- ACP probabiliste (PPCA) pour extraire les variables latentes $\mathbf{Z}_i \in \mathbb{R}^d$
- Projection dans un espace latent de faible dimension

### 4. Clustering

**K-means** : regroupement des stations dans l'espace latent, initialisation du GMM

**Gaussian Mixture Model** : modèle de mélange gaussien avec $K$ composantes, estimation par algorithme EM

### 5. Modélisation probabiliste

Lien entre distance latente et probabilité d'interaction :

$$d_{ij} = \|\mathbf{Z}_i - \mathbf{Z}_j\|_2$$

$$P(A_{ij} = 1 | \mathbf{Z}_i, \mathbf{Z}_j) = \sigma(-\alpha \cdot d_{ij} + \beta)$$

où $\sigma$ est la fonction sigmoïde.

## Structure du projet
```
london-bike-network-analysis/
│
├── data/
│   ├── data.csv
│   └── mu_z.npy
│
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_matrice_connectivite.ipynb
│   ├── 03_acp_ppca.ipynb
│   ├── 04_clustering_kmeans_gmm.ipynb
│   └── 05_analyse_reseau.ipynb
│
├── src/
│   ├── preprocessing.py
│   ├── network.py
│   ├── reduction_dimension.py
│   ├── clustering.py
│   └── visualization.py
│
├── results/
│   ├── figures/
│   └── models/
│
├── requirements.txt
├── README.md
└── rapport.pdf
```

## Technologies

- Python 3.8+
- NumPy, Pandas
- Scikit-learn
- Matplotlib, Seaborn
- NetworkX

## Résultats

Les résultats détaillés sont disponibles dans le rapport final et les notebooks d'analyse.
