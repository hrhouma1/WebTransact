
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📘 **Projet 2 - Projet Pré-développé** 📘

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🚀 **Bienvenue dans le deuxième projet !**

Dans ce projet, nous allons travailler sur un projet pré-développé qui contient trois classes principales. Ce projet vous permettra d'explorer, de configurer, et d'étendre une application existante en y ajoutant des fonctionnalités telles que les services web avec Spring Boot, la journalisation, et la documentation API avec Swagger.

🎯 **Objectifs :**
- Cloner et configurer un projet existant
- Exécuter l'application sans IDE
- Utiliser SQL over HTTP avec Spring Boot
- Tester et manipuler les endpoints avec Postman
- Implémenter une journalisation détaillée
- Documenter l'API avec Swagger

🎉 **Préparez-vous à explorer et à améliorer !**

-----------------------------------
# 🛠️ 1 - Introduction :
-----------------------------------

1. **Cloner le projet pré-développé** : Utiliser Git pour cloner un projet existant contenant trois classes principales.
2. **Configurer le projet** : Vérifier et ajuster les configurations dans le fichier `application.properties` pour assurer une connexion correcte à la base de données PostgreSQL.
3. **Créer l'utilisateur et la base de données PostgreSQL** : Configurer l'utilisateur et la base de données `microDemo1` dans PostgreSQL.
4. **Exécuter l'application sans IDE** : Lancer l'application à partir de la ligne de commande en utilisant Maven ou Gradle.
5. **Résolution des erreurs potentielles** : Diagnostic et correction des erreurs courantes lors de l'exécution du projet.
6. **Vérifier le bon fonctionnement** : Accéder à l'application via le navigateur pour s'assurer que tout fonctionne correctement.

-----------------------------------
# 📝 2 - Étapes et concepts :
-----------------------------------

### **PROJET 2 - Projet Pré-développé**

| **Étape**                                  | **Description**                                                                                                          |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Clonage et configuration du projet**     | Cloner le projet existant avec Git, puis configurer les paramètres de connexion à la base de données dans `application.properties`.  |
| **Création de l'utilisateur et de la base de données** | Créer l'utilisateur `hrgres` et la base de données `microDemo1` dans PostgreSQL.                                          |
| **1. Exécution de l'application sans IDE** |                                                                                                                          |
| - Exécuter le projet avec Maven ou Gradle  | Lancer l'application directement depuis la ligne de commande sans utiliser d'IDE.                                        |
| - Résolution des erreurs potentielles      | Résoudre les erreurs d'exécution courantes comme un port 8080 déjà occupé.                                                |
| **2. SQL Over HTTP et services web avec Spring Boot** |                                                                                                                          |
| - Comprendre les relations entre clients et comptes | Avant de commencer, comprendre les relations entre les entités `Customer` et `Account`.                                   |
| - Insertion des clients dans la base de données | Insérer 20 clients dans la base de données PostgreSQL via des scripts SQL.                                               |
| - Création de comptes via HTTP POST        | Utiliser des requêtes HTTP POST pour créer des comptes tout en respectant les relations définies entre les entités.        |
| **3. Tester et manipuler les endpoints avec Postman** |                                                                                                                          |
| - Tester l'API avec Postman                | Tester les différents endpoints (GET, POST, PUT, DELETE) de l'API avec Postman.                                           |
| - Valider les données dans la base de données | Vérifier que les opérations effectuées via l'API sont bien reflétées dans la base de données.                            |
| **4. Implémentation de la journalisation** |                                                                                                                          |
| - Configurer la journalisation             | Ajouter et configurer la journalisation dans l'application pour suivre les actions importantes.                           |
| - Utiliser des niveaux de log spécifiques  | Configurer des niveaux de journalisation (INFO, WARN, ERROR) pour capturer les informations pertinentes.                  |
| **5. Documentation de l'API avec Swagger** |                                                                                                                          |
| - Ajouter les dépendances Swagger          | Ajouter les dépendances nécessaires pour activer Swagger dans le projet.                                                  |
| - Annoter les endpoints                    | Annoter les contrôleurs avec Swagger pour générer automatiquement la documentation API.                                   |
| - Accéder à Swagger                        | Tester l'interface de documentation Swagger via le navigateur.                                                           |

-----------------------------------
# 🏁 3 - Conclusion :
-----------------------------------

- Dans ce projet, nous avons commencé par cloner et configurer un projet pré-développé en ajustant les paramètres de connexion dans `application.properties` et en créant l'utilisateur et la base de données PostgreSQL nécessaires. Ensuite, nous avons exécuté l'application sans utiliser d'IDE, en utilisant les commandes Maven ou Gradle depuis la ligne de commande, et nous avons résolu les erreurs potentielles qui pouvaient survenir.

- Nous avons ensuite exploré l'utilisation de SQL over HTTP avec Spring Boot en insérant des clients et en créant des comptes via des requêtes HTTP POST. Les étapes suivantes ont consisté à tester et manipuler les endpoints de l'API avec Postman, en validant que les données étaient correctement enregistrées dans la base de données PostgreSQL.

- Pour assurer une traçabilité efficace des actions dans l'application, nous avons configuré un système de journalisation avec différents niveaux de log (INFO, WARN, ERROR). Enfin, nous avons documenté l'API en utilisant Swagger, permettant ainsi une meilleure compréhension et utilisation des endpoints disponibles dans l'application.

- Ces étapes constituent la base solide pour travailler avec des projets Spring Boot pré-développés, en ajoutant progressivement des fonctionnalités et en améliorant la maintenabilité de l'application grâce à une bonne documentation et journalisation.
