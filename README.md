# WEB_scraping
# Rapport de Projet : Analyse de Sentiment des Avis Clients avec Résumé Automatique
# Réalisé par : 
- BOUACEM OUSSAMA

## 1. Introduction
L'objectif de ce projet est de développer une application permettant de :
- Scraper des avis clients depuis un site e-commerce ( Amazon ).
- Analyser leur sentiment (positif, neutre, négatif) à l'aide d'un modèle d'apprentissage automatique.
- Générer un résumé synthétique des avis collectés.

Le projet est divisé en deux parties :
1. **Partie avec Docker** : Scraping de toutes les pages de commentaires avec une interface Flask.
2. **Partie sans Docker** : Scraping de toutes les pages de commentaires avec une interface Flask + l'analyse de sentiment, la recherche vectorielle et la génération de résumés.

## 2. Technologies et Outils Utilisés

### 2.1 Web Scraping
- **Selenium** : Utilisé pour extraire les avis depuis Amazon.
- **Gestion des erreurs** : Mise en place de timeout et de vérifications pour éviter les blocages.

### 2.2 Analyse de Sentiment
- **VADER (Valence Aware Dictionary and sEntiment Reasoner)** : Calcul du score émotionnel du texte.
- **Classification des avis** :
  - **Positif** : score ≥ 0.05
  - **Neutre** : -0.05 < score < 0.05
  - **Négatif** : score ≤ -0.05
- **Ajustement par la note utilisateur** : Correction du score en fonction de la note attribuée par l'utilisateur.

### 2.3 Stockage et Recherche
- **FAISS** : Indexation et recherche rapide des avis similaires grâce à l'embedding des avis.
- **Sentence Transformer** : Modèle "all-MiniLM-L6-v2" utilisé pour la vectorisation des commentaires.

### 2.4 Génération de Résumé
- **BART** : Modèle "sshleifer/distilbart-cnn-12-6" pour produire un résumé des avis collectés.
- **Prétraitement du texte** : Normalisation et découpage pour optimiser le résumé généré.

### 2.5 API Backend
- **Flask** : Création d'une API REST exposant plusieurs endpoints.

## 3. Implémentation

### 3.1 Partie 1 : Scraping avec Docker et Interface Flask
- **Mise en place d'un serveur Flask** pour permettre le scraping via une interface utilisateur.
- **Scraping automatisé** de toutes les pages de commentaires d'un produit.
- **Stockage des données** dans un fichier JSON.
- **Dockerisation de l’application** : Cette partie est conteneurisée pour faciliter le déploiement et éviter les conflits d’environnement.

### 3.2 Partie 2 : Analyse, Stockage et Résumé (Sans Docker)
- **Lecture des avis stockés** pour analyse et recherche.
- **Analyse des sentiments et stockage dans FAISS**.
- **Génération d’un résumé automatique des avis collectés**.

## 4. API REST
Les endpoints disponibles sont :
- `/scrape` : Récupère les avis d'un produit.
- `/reviews` : Renvoie les avis stockés.
- ![image](https://github.com/user-attachments/assets/f94bb081-768d-4ce2-9abc-f7c1bad242c7)

- `/search` : Recherche des avis similaires.
- `/summary` : Génère un résumé des avis.
- `/faiss_status` : Indique le nombre d'entrées indexées.
- ![image](https://github.com/user-attachments/assets/3361093f-85c6-4f2c-8767-5e0dd3aaf00e)


## 5. Tests et Résultats
Les tests ont été réalisés sur plusieurs produits Amazon. Les résultats obtenus montrent une bonne précision dans :
- L’extraction et le stockage des avis.
- L’analyse des sentiments avec une classification fiable.
- La génération des résumés compréhensibles.

## 6. Améliorations et Perspectives
- **Support multi-langue** avec mBERT.
- **Stockage en base de données** pour une meilleure gestion des avis.
- **Interface interactive avec Streamlit ou Dash** pour un affichage des résultats en temps réel.
- **Amélioration du modèle de résumé** pour des résultats plus précis.

## 7. Conclusion
Ce projet démontre l’efficacité de l’automatisation du scraping, de l’analyse des avis et de la génération de résumés. La séparation en deux parties (scraping conteneurisé et analyse hors conteneur) permet une meilleure flexibilité et optimisation des ressources.

## 8. Captures d'Écran
Des captures d’écran seront ajoutées pour illustrer :

L’interface Flask permettant le scraping, et l'interface affichant le résumé des avis.

![image](https://github.com/user-attachments/assets/1af32c2f-1c58-49af-9704-870bacfa320c)
![image](https://github.com/user-attachments/assets/9791e627-fc4e-4646-8480-13519e517b91)


Les résultats des différents endpoints (avis, recherche, résumé).
![image](https://github.com/user-attachments/assets/843137ab-622f-4ad0-975e-166abfe114c6)
![image](https://github.com/user-attachments/assets/a19d5eaa-905d-440f-8819-ad046ad564f5)



L'affichage des statistiques FAISS.
![image](https://github.com/user-attachments/assets/5ca63843-e532-4bd0-866e-b956c3ab01a6)



Cela permettra de mieux visualiser le fonctionnement global du projet.

