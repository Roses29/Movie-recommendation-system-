🌍 [Read in English](README.md) | 📓 [See PDF](./RobinRubangura_Recommendation_Systems.ipynb)

# Système de recommendations de films

## Présentation

Ce projet construit un **Système de Recommandation de Films** inspiré de plateformes comme Netflix. À partir d'un dataset de notes utilisateur-film, trois approches de recommandation distinctes sont implémentées et comparées, allant des méthodes simples basées sur la popularité aux techniques avancées de factorisation matricielle.

## Jeu de données

Le fichier `ratings.csv` contient **100 004 interactions** entre **671 utilisateurs uniques** et **9 066 films uniques**, avec les colonnes suivantes :

- `userId` – identifiant unique de l'utilisateur
- `movieId` – identifiant unique du film
- `rating` – note donnée par l'utilisateur (échelle 0–5)
- `timestamp` – supprimé car non nécessaire à l'analyse

**Observations clés :** les notes de 4 sont les plus fréquentes ; la distribution des interactions par utilisateur est asymétrique à droite, indiquant que la plupart des utilisateurs notent relativement peu de films.

## Modèles Développés

#### 1. 🏆 Système de Recommandation basé sur le Classement (Rank-Based)
Recommande les films les plus populaires selon leur note moyenne, avec un seuil minimum d'interactions configurable. Utile pour résoudre le problème du **cold-start** (nouveaux utilisateurs sans historique).

#### 2. 👥 Filtrage Collaboratif Utilisateur-Utilisateur (KNN)
Identifie des utilisateurs aux goûts similaires et recommande les films qu'ils ont appréciés. Utilise la **similarité cosinus** et **KNN**, optimisé via GridSearchCV.

| | Baseline | Optimisé |
|---|---|---|
| RMSE | 0,9925 | 0,9871 |

#### 3. 🎞️ Filtrage Collaboratif Item-Item (KNN)
Recommande des films similaires à ceux déjà bien notés par l'utilisateur. L'optimisation améliore significativement les résultats.

| | Baseline | Optimisé |
|---|---|---|
| RMSE | 1,0032 | 0,9495 |

#### 4. 🧮 Factorisation Matricielle – SVD (Décomposition en Valeurs Singulières)
Décompose la matrice utilisateur-item en facteurs latents, capturant des patterns cachés. Meilleures performances globales.

| | Baseline | Optimisé |
|---|---|---|
| RMSE | 0,9054 | 0,8953 |

## Comparaison des Modèles (Précision & Rappel @ k=5 et k=10)

Le SVD obtient le meilleur RMSE global. Après optimisation, le modèle item-item surpasse l'user-user en RMSE (0,9495 vs 0,9871). Les valeurs de précision et rappel sont comparables entre les modèles optimisés.

## Points Clés

- Le **SVD surpasse** les méthodes KNN en RMSE grâce à l'extraction de caractéristiques latentes et une meilleure gestion des données creuses.
- L'**optimisation des hyperparamètres** a un impact plus fort sur les modèles item-item que sur les modèles user-user.
- Des **tests A/B** sont recommandés pour mesurer l'efficacité réelle d'un modèle déployé.

## Stack Technique

- **Python** – pandas, NumPy, Matplotlib, Seaborn
- **Surprise** – KNNBasic, SVD, GridSearchCV, KFold, precision_recall_at_k
