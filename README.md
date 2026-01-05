# 🚲 Analyse du Réseau de Vélos en Libre-Service de Londres

##  Description

Ce projet analyse le réseau de vélos en libre-service (Santander Cycles) de Londres en utilisant des techniques avancées d'analyse de graphes et d'apprentissage automatique. L'objectif est de comprendre la structure du réseau, identifier des patterns de mobilité et modéliser les connexions entre stations.

##  Objectifs

- **Explorer** les données de trajets et stations du réseau cyclable londonien
- **Construire** et analyser la matrice de connectivité du réseau
- **Réduire la dimension** des données avec l'ACP Probabiliste (PPCA)
- **Identifier des clusters** de stations aux comportements similaires
- **Modéliser** la probabilité de connexion entre stations
- **Analyser** les propriétés topologiques du réseau (centralité, densité, etc.)

## Technologies Utilisées

- **Python 3.x**
- **NumPy** & **Pandas** - Manipulation des données
- **Matplotlib** & **Seaborn** - Visualisation
- **Scikit-learn** - ACP, K-Means, GMM
- **NetworkX** - Analyse de graphes
- **SciPy** - Calculs scientifiques

##  Structure du Projet

```
projet-analyse-reseau-london-bike/
│
├── data/
│   ├── stations.csv          # Informations sur les stations
│   ├── journeys.csv          # Données des trajets
│   ├── A_npy.npy             # Matrice de connectivité
│   └── mu_z.npy              # Variables latentes pré-calculées
│
├── notebooks/
│   └── analyse_complete.ipynb # Notebook d'analyse principal
│
├── results/                   # Visualisations générées
│   ├── carte_stations.png
│   ├── clusters_geo.png
│   ├── graphe_clusters.png
│   └── ...
│
└── README.md
```

##  Résultats Clés

| Métrique | Valeur |
|----------|--------|
| Nombre de stations | ~750 |
| Nombre de trajets analysés | 100k+ |
| Dimension latente (PPCA) | 17 |
| Nombre de clusters identifiés | 5 |
| Score Silhouette | ~0.3 |

##  Méthodologie

1. **Exploration des données** : Analyse des distributions, visualisation géographique
2. **Construction du graphe** : Matrice d'adjacence pondérée par le nombre de trajets
3. **Réduction de dimension** : ACP Probabiliste pour représenter chaque station en dimension réduite
4. **Clustering** : K-Means et Gaussian Mixture Model pour identifier des groupes de stations
5. **Modélisation probabiliste** : Régression logistique pour prédire les connexions
6. **Analyse de réseau** : Calcul des centralités (degré, betweenness, closeness)

##  Installation

```bash
# Cloner le repository
git clone https://github.com/votre-username/projet-analyse-reseau-london-bike.git
cd projet-analyse-reseau-london-bike

# Installer les dépendances
pip install numpy pandas matplotlib seaborn scikit-learn networkx scipy

# Lancer le notebook
jupyter notebook notebooks/analyse_complete.ipynb
```

##  Visualisations

Le projet génère plusieurs visualisations :
- Carte géographique des stations avec capacité
- Matrice de connectivité du réseau
- Projection 2D de l'espace latent
- Clusters sur carte géographique
- Graphe du réseau avec centralités
- Modèle probabiliste de connexion

