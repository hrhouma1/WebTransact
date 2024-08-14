
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

