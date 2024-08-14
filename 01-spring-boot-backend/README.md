# 🎓 **Bienvenue dans votre parcours d'apprentissage par projet !**

---

## 📝 **Introduction générale**

Dans le cadre de votre apprentissage du développement avec Spring Boot, nous avons structuré ce cours autour de deux projets principaux. Cette approche par projet vous permettra de mettre en pratique les concepts clés tout en apprenant à résoudre des problèmes concrets. L'objectif est de vous offrir une immersion progressive dans l'univers de Spring Boot et de ses différentes fonctionnalités, tout en renforçant votre compréhension théorique grâce à un dossier dédié.

### 🧠 **Concept d'apprentissage par projet**

Nous avons choisi de baser votre apprentissage sur des projets concrets. Cela signifie que vous allez :
- **Construire un projet de A à Z** : Le premier projet est une simple application "Hello World", qui vous permettra de vous familiariser avec les concepts de base de Spring Boot.
- **Modifier et étendre un projet pré-développé** : Le second projet est un projet existant, que vous allez explorer, comprendre, puis améliorer en y ajoutant des fonctionnalités étape par étape.

### 📂 **Dossier Théorie**

En complément des projets, un **dossier Théorie** a été ajouté à ce cours. Ce dossier contient des explications détaillées sur les concepts abordés dans les projets. Il est conçu pour être une ressource de référence à laquelle vous pourrez revenir chaque fois que vous rencontrerez une notion que vous souhaitez approfondir ou clarifier.

---

## 📘 **Projet 1 - Hello World**

### 🚀 **Bienvenue dans le premier projet !**

Dans ce premier projet, vous allez créer un simple service web "Hello World" en utilisant Spring Boot et Spring Framework. Ce projet vous permettra de vous familiariser avec les concepts de base, tels que Maven, pom.xml, PostgreSQL, Docker, et Git.

### 🎯 **Objectifs :**
- Configurer le projet initial.
- Ajouter des dépendances.
- Créer les classes principales.
- Tester l'application.
- Ajouter une base de données.
- Travailler avec Lombok.

### **Étapes et concepts :**

| **Étape**                                  | **Description**                                                                                                          |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Démarrage du premier projet**            | Création d'un service web "Hello World" en utilisant Spring Boot et Spring Framework.                                      |
| **Exploration des concepts de base**       | Introduction à Maven, `pom.xml`, PostgreSQL, Docker, Git pour la gestion des dépendances, bases de données, conteneurs, etc. |
| **1. Rappel rapide et mise en place initiale** |                                                                                                                          |
| - Mise en place du projet                  | Configuration initiale du projet Spring Boot.                                                                             |
| - Ajout des dépendances                    | Ajout des dépendances nécessaires dans le fichier `pom.xml`.                                                             |
| - Importer le projet                       | Importation du fichier `pom.xml` dans l'IDE pour démarrer le développement.                                               |
| - Création des classes                     | Création de `Greeting.java` et `GreetingController.java` pour gérer les données et les requêtes HTTP.                    |
| - Test de l'application                    | Exécution de l'application et résolution des problèmes (par exemple, port 8080 occupé).                                   |
| **2. Ajout d'une base de données**         |                                                                                                                          |
| - Dépendances pour PostgreSQL              | Ajout des dépendances PostgreSQL et JPA dans le fichier `pom.xml`.                                                       |
| - Configuration de la connexion            | Configuration des propriétés de connexion dans `application.properties`.                                                 |
| - Annotations JPA                          | Ajout des annotations JPA dans `Greeting.java` pour la persistance des données.                                           |
| - Vérification du modèle                   | Vérification que `Greeting.java` respecte les exigences de Spring Data.                                                   |
| - Création de la base de données           | Création d'une base de données dans PostgreSQL et assignation des droits à l'utilisateur.                                 |
| **3. Travail avec Lombok**                 |                                                                                                                          |
| - Introduction de Lombok                   | Utilisation de Lombok pour générer automatiquement les méthodes comme les getters et setters.                             |

---

## 📘 **Projet 2 - Projet Account (Pré-développé)**

### 🚀 **Bienvenue dans le deuxième projet !**

Dans ce projet, vous allez travailler sur un projet pré-développé qui contient trois classes principales. Ce projet vous permettra d'explorer, de configurer, et d'étendre une application existante en y ajoutant des fonctionnalités telles que les services web avec Spring Boot, la journalisation, et la documentation API avec Swagger.

### 🎯 **Objectifs :**
- Cloner et configurer un projet existant.
- Exécuter l'application sans IDE.
- Utiliser SQL over HTTP avec Spring Boot.
- Tester et manipuler les endpoints avec Postman.
- Implémenter une journalisation détaillée.
- Documenter l'API avec Swagger.

### **Étapes et concepts :**

| **Étape**                                  | **Description**                                                                                                          |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Clonage et configuration du projet**     | Cloner le projet existant avec Git, puis configurer les paramètres de connexion à la base de données dans `application.properties`.  |
| **Création de l'utilisateur et de la base de données** | Créer l'utilisateur `hrgres` et la base de données `microDemo1` dans PostgreSQL.                                          |
| **Exécution de l'application sans IDE**    |                                                                                                                          |
| - Exécuter le projet avec Maven ou Gradle  | Lancer l'application directement depuis la ligne de commande sans utiliser d'IDE.                                        |
| - Résolution des erreurs potentielles      | Résoudre les erreurs d'exécution courantes comme un port 8080 déjà occupé.                                                |
| **SQL Over HTTP et services web avec Spring Boot** |                                                                                                                          |
| - Comprendre les relations entre clients et comptes | Avant de commencer, comprendre les relations entre les entités `Customer` et `Account`.                                   |
| - Insertion des clients dans la base de données | Insérer 20 clients dans la base de données PostgreSQL via des scripts SQL.                                               |
| - Création de comptes via HTTP POST        | Utiliser des requêtes HTTP POST pour créer des comptes tout en respectant les relations définies entre les entités.        |
| **Tester et manipuler les endpoints avec Postman** |                                                                                                                          |
| - Tester l'API avec Postman                | Tester les différents endpoints (GET, POST, PUT, DELETE) de l'API avec Postman.                                           |
| - Valider les données dans la base de données | Vérifier que les opérations effectuées via l'API sont bien reflétées dans la base de données.                            |
| **Implémentation de la journalisation**    |                                                                                                                          |
| - Configurer la journalisation             | Ajouter et configurer la journalisation dans l'application pour suivre les actions importantes.                           |
| - Utiliser des niveaux de log spécifiques  | Configurer des niveaux de journalisation (INFO, WARN, ERROR) pour capturer les informations pertinentes.                  |
| **Documentation de l'API avec Swagger**    |                                                                                                                          |
| - Ajouter les dépendances Swagger          | Ajouter les dépendances nécessaires pour activer Swagger dans le projet.                                                  |
| - Annoter les endpoints                    | Annoter les contrôleurs avec Swagger pour générer automatiquement la documentation API.                                   |
| - Accéder à Swagger                        | Tester l'interface de documentation Swagger via le navigateur.                                                           |

---

## 🏁 **Conclusion**

- Le parcours d'apprentissage par projet vous permettra de développer vos compétences en travaillant sur des cas concrets. Vous commencerez par un projet simple, "Hello World", que vous construirez de A à Z, et continuerez avec un projet plus complexe déjà développé, que vous modifierez et améliorerez au fil des étapes.
- N'oubliez pas d'explorer le **dossier Théorie** pour approfondir les concepts lorsque vous en ressentez le besoin. Ce dossier est là pour compléter votre apprentissage pratique avec des explications théoriques détaillées.
- Bonne chance dans votre apprentissage, et surtout, amusez-vous bien en codant !

---

# DRIVE DU COURS : 
- https://drive.google.com/drive/folders/1S1X65L3orErShoWQQxu9oOcKu7knLtDB?usp=sharing



