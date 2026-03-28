# Analyse de Survie : Modèle de Cox (Cancer du Poumon)

Ce projet présente une analyse de survie complète en utilisant le **modèle à risques proportionnels de Cox** et l'estimateur de **Kaplan-Meier**. L'étude porte sur les données de survie de patients atteints d'un cancer du poumon avancé (NCCTG Lung Cancer Data).

## 📌 Objectifs de l'Analyse

- Estimer les probabilités de survie en fonction du temps.
- Comparer la survie entre différents groupes (hommes vs femmes).
- Identifier les facteurs de risque significatifs influençant la survie des patients.
- Valider les hypothèses fondamentales du modèle de Cox.

## 🛠️ Prérequis et Installation

### Logiciels requis
- [R](https://www.r-project.org/) (version >= 4.0 recommandée)
- [RStudio](https://rstudio.com/) (optionnel, mais recommandé)

### Bibliothèques R nécessaires
Le script `load_libraries.R` permet de charger les dépendances suivantes :
- `survival` : Outils principaux pour l'analyse de survie.
- `survminer` : Visualisation avancée des courbes de survie.
- `tidyverse` : Manipulation des données (dplyr, ggplot2).
- `parameters` : Mise en forme des résultats du modèle.
- `GGally` : Visualisation des coefficients de régression.

Pour installer les packages manquants, vous pouvez exécuter :
```R
install.packages(c("survival", "survminer", "tidyverse", "parameters", "GGally", "broom.helpers"))
```

## 📂 Structure du Projet

```text
.
├── cox-model-colon.rmd      # Script principal d'analyse (RMarkdown)
├── cox-model-colon.nb.html  # Version HTML compilée du notebook
├── load_libraries.R         # Chargement des dépendances R
├── img/                     # Dossier contenant les visualisations générées
│   ├── survie_kaplan_meier_sexe.png
│   ├── coefficients_cox.png
│   ├── test_proportionnalite_risques.png
│   └── ...
└── README.md                # Documentation du projet
```

## 📊 Méthodologie

### 1. Analyse de Kaplan-Meier
Utilisée pour estimer la fonction de survie $S(t)$. Les courbes de survie permettent une première comparaison visuelle entre les groupes (par exemple, par sexe).

### 2. Test du Log-Rank
Un test non-paramétrique comparant les distributions de survie de deux ou plusieurs groupes indépendants. 
- **$H_0$** : Pas de différence entre les groupes.
- **$H_1$** : Différence significative de survie.

### 3. Modèle de Régression de Cox
Le modèle de Cox permet d'analyser l'effet de plusieurs variables simultanément :
$$h(t \mid X) = h_0(t) \exp(\sum \beta_i X_i)$$
Les variables analysées incluent : l'âge, le sexe, le score ECOG (`ph.ecog`), le score de Karnofsky (`ph.karno`, `pat.karno`), l'apport calorique (`meal.cal`) et la perte de poids (`wt.loss`).

## 📈 Résultats Clés

- **Sexe** : Les femmes présentent un risque de décès significativement plus bas que les hommes ($HR \approx 0.57$).
- **Score ECOG** : Un score de performance ECOG élevé est un facteur de risque majeur ($HR \approx 2.21$), doublant presque le risque de décès à chaque unité supplémentaire.
- **Validation** : Les hypothèses de **proportionnalité des risques** (test de Schoenfeld) et de **log-linéarité** (résidus de Martingale) ont été vérifiées et ne sont pas rejetées.

## 🚀 Utilisation

1. Ouvrez le fichier `cox-model-colon.rmd` dans RStudio.
2. Exécutez les blocs de code (chunks) séquentiellement ou cliquez sur le bouton **Knit** pour générer le rapport complet.
3. Les graphiques seront automatiquement sauvegardés dans le dossier `img/`.

---
*Note : Bien que le fichier soit nommé `cox-model-colon.rmd`, l'analyse traite des données du cancer du poumon (`survival::cancer`).*
