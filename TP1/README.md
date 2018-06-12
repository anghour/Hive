# TP1 – Hive


## Data Description

J'ai utilisé la base de donnée "Titanic" de  [kaggle](https://www.kaggle.com/c/titanic/data). Cette base de données est composée principalement de deux fichiers, "train.csv" et "test.csv". Pour mon TP j'ai utilisé le fichier "train.csv". Ce dernier contient des données sur les passagers de Titanic en 891 ligne et 12 colonnes (passengerId, survival, pclass, name, sex, age, sibsp, parch, ticket, fare, cabin, embarked)

## Lacement de beeline

Par la commande suivate :

```
beeline
```

## Connexion au hive du cluster

Par la commande suivante

```
!connect jdbc:hive2://
```

## Création de la base de données ``` Titanic ```

```
create database titanic;
```

## Création de la table ``` Passenger ```

```
CREATE TABLE IF NOT EXISTS Passenger(  
  PassengerId INT,  
  Survived INT,  
  Pclass INT,
  Name STRING,  
  Sex STRING,  
  Age INT,  
  SibSp INT,  
  Parch INT,
  Ticket STRING,  
  Fare DOUBLE,  
  Cabin STRING,  
  Embarked STRING  
) ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'  
WITH SERDEPROPERTIES (  
  "separatorChar" = ",",  
  "quoteChar"     = '"'  
) STORED AS TEXTFILE;  
```
## Structure de la table ``` Passenger```

![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/Passenger_struct.png)

## chargement du fichier ``` train.csv``` dans la table ``` Passenger ```

```
LOAD DATA LOCAL INPATH '/home/ubuntu/data/train.csv' OVERWRITE INTO TABLE Passenger;
```

## Optimisation par ORC
### Création de la table Passenger_ORC
```
CREATE TABLE Passenger_ORC (  
PassengerId INT,  
  Survived INT,  
  Pclass INT,
  Name STRING,  
  Sex STRING,  
  Age INT,  
  SibSp INT,  
  Parch INT,
  Ticket STRING,  
  Fare DOUBLE,  
  Cabin STRING,  
  Embarked STRING  
) STORED AS ORC tblproperties ("orc.compress" = "SNAPPY");
```
### Insertion de données dans la table ``` Passenger_ORC``` à partir de la table ``` Passenger ```

```
INSERT INTO TABLE Passenger_ORC SELECT * FROM Passenger;
```

## Quelques requêtes
### Total de voyageurs par sex
* **Requête**

```
SELECT COUNT(passengerid) as Nombre_Passagers, sex FROM passenger_orc GROUP BY sex;
```
* **Réponse**  

![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/req_1.png)

### Les survivants par sex

* **Requête**

```
SELECT sex, COUNT(passengerid) as Survived_Number FROM passenger_orc WHERE survived = 1 GROUP BY sex;
```
* **Réponse**  
![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/req_2.png)

### Les morts par classe
* **Requête**
```
SELECT COUNT(passengerid) as nombre_morts, pclass as Classe FROM passenger_orc WHERE survived = 0 GROUP BY pclass;
```
* **Réponse**  
![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/req_3.png)
### Les morts par age et sex
* **Requête**
```
SELECT COUNT(passengerid) as nombre_morts, age, sex FROM passenger_orc WHERE survived = 0 GROUP BY age, sex;
```
* **Réponse**  
![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/req_4.png)  
...  
![alt text](https://github.com/anghour/Hive/blob/master/TP1/img/req_4.1.png)
