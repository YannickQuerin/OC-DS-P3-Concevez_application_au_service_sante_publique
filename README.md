# Application de Recommandation Alimentaire Basée sur la Similarité des Caractéristiques Nutritionnelles  

---

## **Objectif du Projet**  

Ce projet vise à concevoir une application permettant de recommander des produits alimentaires similaires en fonction de leurs caractéristiques nutritionnelles (protéines, sucres, graisses, fibres, etc.) afin de favoriser une alimentation saine et équilibrée.  

L'application se base sur la base de données libre [Open Food Facts](https://world.openfoodfacts.org/).  

---

## **Sommaire**  
1. [Données](#données)  
2. [Nettoyage des Données](#nettoyage-des-données)  
3. [Analyse des Données](#analyse-des-données)  
4. [Conception de l'Application](#conception-de-lapplication)  
5. [Conclusion et Perspectives](#conclusion-et-perspectives)  

---

## **Données**  

- **Source** : Open Food Facts  
- **Volume initial** : 320 772 lignes, 162 variables  
- **Taux de valeurs manquantes** : Plus de 76 % des valeurs sont manquantes  

Les données sont réparties en 5 sections principales :  
1. Informations générales  
2. Tags  
3. Ingrédients  
4. Données nutritionnelles  
5. Autres  

![Exploration des données](./images/exploration_donnees.png)

---

## **Nettoyage des Données**  

### Étapes principales :  
1. Suppression des variables avec plus de 80 % de valeurs manquantes  
2. Formatage des noms de variables (`-` remplacé par `_`)  
3. Suppression des doublons basés sur les codes produit  
4. Filtrage des produits avec informations nutritionnelles complètes  

### **Résumé final des données**  
- **Taille finale** : 58 812 lignes, 16 variables  

![Nettoyage des données](./images/nettoyage_donnees.png)

---

## **Analyse des Données**  

### Analyse Univariée  
- Distribution des nutriments : protéines, glucides, matières grasses  
- Variabilité des nutri-scores  

![Analyse univariée](./images/analyse_univariee.png)

### Analyse Multivariée  
- Test de Kruskal-Wallis (ANOVA non paramétrique) :  
  - H = 918,21, p = 0 (différence significative détectée)  
  - Conclusion : Aucune différence significative des moyennes de protéines selon les catégories de nutri-scores  
- Analyse en Composantes Principales (ACP) :  
  - Contribution expliquée à 95 % sur les 7 premières composantes  
  - Identification de clusters :  
    - Produits riches en protéines  
    - Produits gras et caloriques  
    - Produits peu gras et peu caloriques  

![ACP - Clusters Nutritionnels](./images/acp_clusters.png)

---

## **Conception de l'Application**  

### **Scoring des Produits**  
- Variables utilisées :  
  - `proteins_100g`, `fat_100g`, `carbohydrates_100g`, `fiber_100g`, `salt_100g`  
- Pondération des caractéristiques nutritionnelles :  
  - Protéines : 50  
  - Gras : 2  
  - Glucides : 3  
  - Fibres : 5  
  - Sel : 7  

![Pondération des scores](./images/ponderation_scores.png)

### **Moteur de Recommandation**  
- Prétraitement des noms de produits :  
  - Suppression des stopwords (NLTK)  
  - Vectorisation avec `TfidfVectorizer`  
- Calcul de similarité :  
  - Distance de cosinus entre caractéristiques nutritionnelles  
  - Algorithme KNN pour le tri des produits recommandés  

![Architecture de l'application](./images/moteur_recommendation.png)

---

## **Conclusion et Perspectives**  

### **Résumé**  
- Données nettoyées et analysées  
- Moteur de recommandation basé sur la similarité nutritionnelle  

![Bilan](./images/bilan_conclusion.png)

### **Limites**  
- Fiabilité de la similarité sur l'ensemble des produits  
- Manque de données pour les produits vendus hors de France  

### **Propositions d'amélioration**  
1. Ajout de liens vers les photos manquantes  
2. Fonctionnalité de scan des produits pour vérifier leur conformité (ex : produits interdits)  
3. Calcul automatisé du bilan protéique journalier/mensuel  

---

## **Contact**  

Pour toute question ou demande de collaboration :  
- **Email** : yannickquerin@gmail.com  
- **LinkedIn** : [Yannick Quérin](https://linkedin.com/in/yannick-quérin/)  
- **GitHub** : [YannickQuerin](https://github.com/YannickQuerin)  
