# TP1 – Hive

One Paragraph of project description goes here

## Data Description

J'ai utilisé la base de donnée "Titanic" de  [kaggle](https://www.kaggle.com/c/titanic/data). Cette base de données est composée principalement de deux fichiers, "train.csv" et "test.csv". Pour mon TP j'ai utilisé le fichier "train.csv". Ce dernier contient des données sur les passagers de Titanic en 891 ligne et 11 colonnes (passengerId, survival, pclass, sex, age, sibsp, parch, ticket, fare, cabin, embarked)

## Lacement de beeline

Par la commande suivate :

```
beeline
```

## Connection 

Par la commande suivante

```
!connect jdbc:hive2://
```

## Création de la base de données "Titanic"

```
la commande
```

## Création de mon tableau


```
la commande
```

## chargement de données



```
la commande
```

## Optimisation par ORC
### Création du tab ORC
### Chargement du tab ORC

## Structure de mon tableau ORC

Image
![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/passenger_orc.png)

## Quelques requêtes
* Total de voyageurs par sex
* **Requête**

```
SELECT COUNT(passengerid) as Passenger_ID, sex FROM passenger_orc GROUP BY sex;
```
* **Réponse**




