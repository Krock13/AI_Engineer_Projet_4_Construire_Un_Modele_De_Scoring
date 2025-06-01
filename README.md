# Crédit Scoring Interprétable – Projet « Prêt à dépenser »

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?logo=python">
  <img src="https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter">
  <img src="https://img.shields.io/badge/Code%20Style-PEP8-green">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey">
</p>

## Objectif

Développer un **algorithme de scoring crédit** capable de :

* prédire la probabilité de défaut d’un client (`P(default)=1`) ;
* classifier la demande : **accord** ou **refus** de prêt ;
* **minimiser le risque métier** en tenant compte d’un **coût FN 10 × supérieur** au coût FP ;
* rester **interprétable** pour les chargés de relation client (importance globale & locale des variables).

---

## Jeu de données

Données publiques **Home Credit Default Risk** :

* 307 511 lignes d’entraînement, 122 variables brutes (client & historique prêt).
* Fichier description détaillée des colonnes.

---

## Arborescence

```
.
├── .gitignore
├── 00.description.ipynb              # Contexte & description du dataset
├── 01.notebook_analyse_exploratoire_feature_engineering.ipynb
├── 02.notebook_modelisation.ipynb
├── Projet 4.pdf                      # Slides de présentation
├── requirements.txt
└── (README.md)                       # <- VOUS ÊTES ICI
```

---

## Installation rapide

### Pré‑requis

* Python ≥ 3.10  
* `git`, `pip`, et **optionnel** : Docker ou VS Code Dev Container

### Setup

```bash
# Cloner le dépôt
git clone https://github.com/Krock13/AI_Engineer_Projet_4_Construire_Un_Modele_De_Scoring.git
cd AI_Engineer_Projet_4_Construire_Un_Modele_De_Scoring

# Linux / macOS
python -m venv .venv && source .venv/bin/activate

# Windows (PowerShell)
python -m venv .venv; .\.venv\Scripts\Activate.ps1

# Installation des dépendances
pip install -r requirements.txt

# Lancer JupyterLab
jupyter lab
```

---

## Reproduire l’étude

1. **Exploration & Feature Engineering**
   *Notebook : `01_exploration_feature_eng.ipynb`*
   * traitement des valeurs manquantes, encodage cat → num, création **3+ variables** dérivées pertinentes.

2. **Modélisation & Sélection**
   *Notebook : `02_modelisation.ipynb`*
   * prise en compte du **déséquilibre** (undersampling) ;
   * **score métier** : `cost = 10 × FN + 1 × FP`, optimisé via **GridSearchCV** & **cross‑validation 5‑fold** ;
   * comparaison : Dummy, Logistic Reg., Random Forest, Gradient Boosting, XGBoost, **LightGBM**.

3. **Optimisation du seuil**
   * maximisation du score métier (≠ seuil 0,5) pour le meilleur modèle.

4. **Interprétabilité**
   * importance globale : gain LightGBM + **SHAP summary plot** ;
   * explication locale pour un client : **SHAP waterfall**.

---

## Résultats clés

| Métrique                     | Meilleur modèle (LightGBM + undersampling) |
|------------------------------|--------------------------------------------|
| **Score métier (↘)**        | **≈ 30 k** |
| AUC ROC (CV)                | 0,785 |
| F1                          | 0,289 |
| Précision                   | 0,181 |
| Rappel (sensibilité)        | 0,712 |
| Seuil optimisé              | 0,23 |

> ℹ️  Le modèle réduit de **40 %** le coût métier vs. baseline Dummy, tout en dépassant l’AUC > 0,78 (proche du top 5 % Kaggle).

---

## Pistes d’amélioration

* **MLOps** : MLflow + DVC pour tracking data/model.
* **API temps réel** : FastAPI + Docker → endpoint de prédiction.
* **Explainability dashboard** : Streamlit ou Gradio pour visualiser SHAP en front‑office.
* **Calibration** : Platt/Beta calibration pour aligner probas prêtes à l’usage métier.

---

## 📄 Licence

Code sous licence **MIT**.

---

> _« All models are wrong, but some are useful. »_ – George Box
