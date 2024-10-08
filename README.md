# Modèle de Scoring Crédit - Projet 4

## Contexte

Ce projet a été réalisé dans le cadre de la formation **AI Engineer**. L'objectif est de développer un modèle de scoring crédit pour une société financière fictive, **Prêt à Dépenser**, qui propose des crédits à la consommation pour des clients avec peu ou pas d’historique de prêt.

## Objectif du Projet

-   **But principal** : Prédire la probabilité qu'un client rembourse ou non son prêt.
-   **Classifications** :
    -   Crédit accordé
    -   Crédit refusé
-   **Méthodologie** : Modéliser un outil de scoring performant et facilement interprétable pour les chargés de relation client.

## Données Utilisées

-   **application_train.csv & application_test.csv** : Informations principales sur les clients et leurs demandes de prêt (âge, revenus, historique financier, etc.).
-   **Fichiers complémentaires** :
    -   `bureau.csv` & `bureau_balance.csv`
    -   `credit_card_balance.csv`
    -   `installments_payments.csv`
    -   `POS_CASH_balance.csv`
    -   `previous_application.csv`

Ces fichiers contiennent des informations supplémentaires telles que les crédits précédents auprès d’autres institutions, les soldes de cartes de crédit, les versements effectués, et plus encore.

## Approche Méthodologique

### 1. **Exploration et Préparation des Données**

-   Analyse exploratoire pour détecter les anomalies, comme les valeurs incohérentes dans `DAYS_EMPLOYED`.
-   Traitement des données manquantes et des variables catégorielles via un encodage approprié (Label Encoding et One-Hot Encoding).
-   Calcul des corrélations entre les variables explicatives et la cible (`TARGET`).

### 2. **Feature Engineering**

Création de nouvelles variables pour améliorer la prédiction, par exemple :

-   `DAYS_EMPLOYED_PERC` : Ratio entre le nombre de jours travaillés et l'âge du client.
-   `AVG_FAM_MEMBER_AGE` : Moyenne d’âge des membres de la famille.
-   `EXT_SOURCE_1_YEARS_BIRTH` : Combinaison de scores externes et de l’âge pour mieux évaluer le profil de risque.

### 3. **Modélisation**

-   Modèles testés : Plusieurs modèles de machine learning ont été testés.
-   Gestion du déséquilibre de classes via des techniques comme l'**undersampling**.
-   Optimisation des hyperparamètres pour maximiser l'efficacité tout en minimisant les erreurs coûteuses (faux positifs et faux négatifs).

### 4. **Interprétabilité**

-   Utilisation des valeurs SHAP et de l’importance des features pour comprendre quelles variables influencent le plus les décisions du modèle.

## Résultats

-   Un modèle performant qui permet de prendre des décisions de crédit éclairées.
-   Optimisation du coût métier en réduisant les erreurs coûteuses (faux négatifs).

## Conclusion

Le modèle final atteint les objectifs en offrant une prédiction précise et une bonne interprétabilité. Il pourra être amélioré avec des données mises à jour régulièrement et des techniques d'interprétabilité plus avancées.

## Installation

1. Cloner le dépôt Git :

    ```bash
    git clone https://github.com/ton-repo/projet-4-scoring.git
    ```

2. Installer les dépendances :

    ```bash
    pip install -r requirements.txt
    ```

3. Exécuter le script de préparation des données et d'entraînement du modèle :

    ```bash
     pip install papermill  # Installer papermill si ce n’est pas déjà fait
     papermill notebook_analyse_exploratoire_feature_enginering.ipynb output_analyse_exploratoire.ipynb
     papermill notebook_modelisation.ipynb output_modelisation.ipynb

    ```

## Usage

Après avoir installé les dépendances et préparé les données, vous pouvez exécuter les prédictions sur de nouvelles données en utilisant le modèle entraîné.
