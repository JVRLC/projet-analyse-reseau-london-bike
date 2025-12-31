# Analyse d’un réseau – London Bike Sharing

## 1. Contexte du projet

Ce projet vise à analyser un **réseau de stations de vélos en libre-service à Londres** à partir des données de trajets entre stations. Le problème est formulé comme une **analyse de réseau** combinant :

* construction d’une matrice de connectivité,
* réduction de dimension,
* clustering (k-means, GMM),
* modélisation probabiliste latente.

Le projet met en œuvre des outils de **statistique**, **machine learning** et **théorie des graphes**, principalement en Python.

---

## 2. Données

### 2.1 Description

* **Nombre d’individus (stations)** : ( N = 777 )
* **Station** : position géographique des stations (latitude, longitude)
* **Journey** : trajets de vélos d’une station ( i ) vers une station ( j )

On définit :

[
A_{ij} = \text{nombre de trajets de la station } i \text{ vers la station } j
]

La matrice de connectivité est donc :

[
A \in \mathbb{N}^{777 \times 777}
]

### Hypothèses

* ( A ) est **symétrique**
* diagonale nulle : ( A_{ii} = 0 )

---

## 3. Modélisation du réseau

### 3.1 Matrice binaire d’adjacence

On introduit une matrice binaire :

[
A^{binaire}_{ij} \in {0,1}
]

avec :

[
A^{binaire}*{ij} = 1 \iff A*{ij} > 0
]

Elle représente l’existence d’une interaction entre deux stations.

---

## 4. Représentation latente

Chaque station ( i ) est associée à une représentation latente :

[
Z_i \in \mathbb{R}^2
]

La distance latente entre deux stations est :

[
d_{ij} = | Z_i - Z_j |_2
]

On modélise ensuite les interactions par :

[
A_{ij} \sim \mathcal{B}(p = f(d_{ij}))
]

avec :

* ( f ) une fonction **décroissante** de la distance (ex : fonction logistique ou exponentielle)

---

## 5. Phase intermédiaire (agrégation)

Afin de simplifier le problème, on construit une matrice agrégée :

[
A \in \mathbb{N}^{777 \times 17}
]

* 17 variables résumant l’activité des stations
* Modélisation via une **loi de Poisson**

[
A_{ik} \sim \mathcal{P}(\lambda_{ik})
]

---

## 6. Réduction de dimension

### 6.1 ACP probabiliste (PPCA)

Objectif : associer à chaque station une variable latente

[
Z_i \in \mathbb{R}^p, \quad p \ll 777
]

Méthodes possibles :

* ACP probabiliste sur la matrice ( A )
* ACP classique sur ( Z )
* Utilisation du fichier fourni `mu_z.npy`

---

## 7. Clustering

### 7.1 K-means

* Appliqué sur l’espace latent ( Z )
* Sert également à **initialiser les paramètres du GMM**

### 7.2 Gaussian Mixture Model (GMM)

* Modèle probabiliste de clustering
* Paramètres estimés par **EM (Expectation-Maximization)**
* Initialisation : centres issus de k-means

---

## 8. Modélisation probabiliste sur Z

### 8.1 Vraisemblance

Pour un GMM à ( K ) composantes :

[
p(Z_i) = \sum_{k=1}^K \pi_k , \mathcal{N}(Z_i ,|, \mu_k, \Sigma_k)
]

### 8.2 Inférence

* Maximisation de la log-vraisemblance
* Algorithme EM :

  * **E-step** : calcul des responsabilités
  * **M-step** : mise à jour des paramètres

---

## 9. Analyse et interprétation

* Interprétation des clusters de stations
* Lien avec la géographie (zones centrales vs périphériques)
* Comparaison k-means / GMM
* Analyse de la structure du réseau

---

## 10. Visualisation

Outils utilisés :

* **NetworkX** : graphe de connectivité
* **Matplotlib / Seaborn** :

  * graphe du réseau
  * projection ACP
  * clusters sur carte géographique

---

## 11. Structure du dépôt Git

```
projet-analyse-reseau-london-bike/
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
├── requirements.txt
├── README.md
└── rapport.pdf
```

---

## 12. Technologies

* Python 3
* pandas, numpy
* scikit-learn
* networkx
* matplotlib, seaborn

---

## 13. Objectifs pédagogiques

* Comprendre la modélisation des réseaux
* Lien entre graphes et variables latentes
* Maîtriser ACP, k-means, GMM
* Interpréter des résultats statistiques complexes

---

## 14. Perspectives

* Modèle de graphes latents (Latent Space Model)
* Extension à des graphes dirigés
* Prise en compte du temps (réseau dynamique)
