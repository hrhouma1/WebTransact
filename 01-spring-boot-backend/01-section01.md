
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📘 **Projet 1 - Hello World** 📘
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🚀 **Bienvenue dans le premier projet !**

Dans ce projet, nous allons créer un simple service web "Hello World" en utilisant Spring Boot et Spring Framework. Ce projet vous permettra de vous familiariser avec les concepts de base, tels que Maven, pom.xml, PostgreSQL, Docker, et Git.

🎯 **Objectifs :**
- Configurer le projet initial
- Ajouter des dépendances
- Créer les classes principales
- Tester l'application
- Ajouter une base de données
- Travailler avec Lombok

🎉 **Préparez-vous à coder !**
```

-------
# 1 - Introduction : 
-------

1. Utiliser Spring Initializr pour créer et configurer rapidement un projet Spring Boot.  
2. Ajouter les dépendances nécessaires dans le fichier pom.xml.  
3. Importer le fichier pom.xml dans l'environnement de développement Maven.
4. Créer les classes `Greeting.java` et `GreetingController.java` pour gérer les données et les contrôleurs de l'application.
5. Exécuter l'application pour vérifier son bon fonctionnement.
6. Résoudre les éventuels problèmes, comme un port 8080 déjà occupé.
7. Ajouter les dépendances PostgreSQL et JPA dans le fichier pom.xml.
8. Configurer les propriétés de connexion dans le fichier application.properties.
9. Ajouter les annotations JPA à la classe `Greeting.java` pour assurer la persistance des données.
10. Vérifier que la classe `Greeting.java` respecte les exigences de Spring Data.
11. Créer une base de données PostgreSQL (par exemple nommée "haythem") et attribuer les privilèges nécessaires à l'utilisateur désigné.
12. Utiliser Lombok pour simplifier le code en générant automatiquement des méthodes courantes comme les getters et setters.


-------
# 2- Étapes et concepts :
-------

### PROJET 1 - Projet Hello World

| **Étape**                                 | **Description**                                                                                                          |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Démarrage du premier projet**           | Nous allons créer un service web "Hello World" en utilisant Spring Boot et Spring.                                        |
| **Exploration des concepts de base**      | Introduction à Maven, pom.xml, PostgreSQL, Docker, Git pour la gestion des dépendances, bases de données, conteneurs, etc.|
|                                           |                                                                                                                          |
| **1. Rappel rapide et mise en place initiale** |                                                                                                                      |
| - Mise en place du projet                 | Configuration initiale du projet Spring Boot.                                                                             |
| - Ajout des dépendances                   | Ajout des dépendances nécessaires dans le fichier `pom.xml`.                                                             |
| - Importer le projet                      | Importation du fichier `pom.xml` dans l'IDE pour démarrer le développement.                                               |
| - Création des classes                    | Création de `Greeting.java` et `GreetingController.java` pour gérer les données et les requêtes HTTP.                    |
| - Test de l'application                   | Exécution de l'application et résolution des problèmes (par exemple, port 8080 occupé).                                   |
| **2. Ajout d'une base de données**        |                                                                                                                          |
| - Dépendances pour PostgreSQL             | Ajout des dépendances PostgreSQL et JPA dans le fichier `pom.xml`.                                                       |
| - Configuration de la connexion           | Configuration des propriétés de connexion dans `application.properties`.                                                 |
| - Annotations JPA                         | Ajout des annotations JPA dans `Greeting.java` pour la persistance des données.                                           |
| - Vérification du modèle                  | Vérification que `Greeting.java` respecte les exigences de Spring Data.                                                   |
| - Création de la base de données          | Création d'une base de données dans PostgreSQL et assignation des droits à l'utilisateur.                                 |
| **3. Travail avec Lombok**                |                                                                                                                          |
| - Introduction de Lombok                  | Utilisation de Lombok pour générer automatiquement les méthodes comme les getters et setters.                             |


-------
# 3 - Conclusion: 
-------

Dans le cadre du projet 1 intitulé "Hello World", nous commencerons par la mise en place initiale du projet en utilisant Spring Initializr, où nous ajouterons les dépendances nécessaires dans le fichier pom.xml et importerons ce dernier dans l'environnement de développement Maven. Ensuite, nous procéderons à la création des classes `Greeting.java` et `GreetingController.java`, qui seront utilisées pour gérer les données et les contrôleurs de l'application Spring Boot. Après avoir testé l'application et résolu les éventuels problèmes, comme un port 8080 déjà occupé, nous intégrerons une base de données PostgreSQL en ajoutant les dépendances PostgreSQL et JPA au fichier pom.xml. Nous configurerons ensuite les propriétés de connexion dans le fichier application.properties et ajouterons les annotations JPA à la classe `Greeting.java` pour assurer la persistance des données. La vérification des getters, setters, et constructeurs sera effectuée pour garantir que la classe respecte les exigences de Spring Data. Par la suite, nous créerons une base de données PostgreSQL, par exemple nommée "haythem", et attribuerons les privilèges nécessaires à l'utilisateur désigné. Enfin, nous travaillerons avec Lombok pour simplifier le code en générant automatiquement des méthodes courantes comme les getters et setters. Ces étapes constituent la structure principale du projet, vous guidant depuis la configuration initiale de Spring Boot jusqu'à l'ajout d'une base de données et l'utilisation de Lombok pour rendre le développement plus efficace.
