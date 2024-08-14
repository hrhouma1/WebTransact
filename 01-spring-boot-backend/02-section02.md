
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📘 **Projet 2 - Projet Pré-développé** 📘

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🚀 **Bienvenue dans le deuxième projet !**

Dans ce projet, nous allons travailler sur un projet pré-développé qui contient trois classes principales. L'objectif est de vous familiariser avec l'analyse d'un code existant, sa configuration, et l'ajout de nouvelles fonctionnalités étape par étape. Ce projet met l'accent sur l'utilisation des services web, l'interaction avec une base de données via des requêtes HTTP, la documentation de l'API, et la journalisation pour assurer une traçabilité optimale des opérations.

🎯 **Objectifs :**
- Cloner et configurer un projet existant
- Exécuter le projet sans IDE
- Utiliser SQL over HTTP et les services web avec Spring Boot
- Documenter l'API avec Swagger
- Implémenter une journalisation détaillée
- Tester et manipuler les endpoints avec Postman
- Conclure avec une compréhension approfondie des bonnes pratiques en développement web

🎉 **Préparez-vous à explorer et à améliorer !**

-----------------------------------
# 🛠️ 1 - Introduction :
-----------------------------------

1. **Cloner le projet pré-développé** : Utiliser Git pour cloner le projet existant. Ce projet contient trois classes principales que vous allez explorer et analyser afin de comprendre leur rôle et leur interaction.
   
2. **Explorer et analyser le projet** : Prenez le temps d'explorer les classes, les services, et les contrôleurs déjà en place. Identifiez les dépendances, les annotations utilisées, et le flux de données entre les différentes couches de l'application.

3. **Configurer le projet** : Ouvrez le fichier `application.properties` pour vérifier et, si nécessaire, ajuster les configurations telles que la connexion à la base de données. Assurez-vous que les paramètres correspondent à votre environnement local.

4. **Créer l'utilisateur et la base de données PostgreSQL** : Avant de lancer l'application, créez l'utilisateur `hrgres` et la base de données `microDemo1` dans PostgreSQL. Configurez les droits d'accès appropriés pour garantir que l'application puisse interagir avec la base de données.

5. **Exécuter l'application sans IDE** : Placez-vous dans le répertoire du projet contenant le fichier `pom.xml` et exécutez le projet en utilisant Maven ou Gradle, en fonction de votre environnement de développement. Ceci vous permettra de lancer l'application directement depuis la ligne de commande.

6. **Résolution des erreurs potentielles** : En cas d'erreurs lors de l'exécution (par exemple, un port 8080 déjà occupé), utilisez des commandes spécifiques comme `mvn clean install -DskipTests` pour contourner les tests et assurer l'exécution. Cela vous permettra de diagnostiquer et de corriger rapidement les problèmes rencontrés.

7. **Vérification du bon fonctionnement** : Une fois l'application exécutée, vérifiez que tous les services démarrent correctement en accédant à l'URL `http://localhost:8080/`. Assurez-vous qu'il n'y a pas d'erreurs critiques dans les logs.

-----------------------------------
# 📝 2 - Étapes et concepts :
-----------------------------------

### **PROJET 2 - Projet Pré-développé**

| **Étape**                                  | **Description**                                                                                                          |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Clonage et configuration du projet**     | Cloner le projet en utilisant Git, explorer les classes existantes, et configurer le fichier `application.properties`.    |
| **Création de l'utilisateur et de la base de données** | Créer l'utilisateur `hrgres` et la base de données `microDemo1` dans PostgreSQL.                                          |
| **1. Exécution de l'application sans IDE** |                                                                                                                          |
| - Exécuter le projet avec Maven ou Gradle  | Utiliser les commandes Maven (`mvn spring-boot:run`) ou Gradle pour lancer l'application sans IDE.                        |
| - Résolution des erreurs potentielles      | En cas d'erreurs, utiliser des commandes alternatives comme `mvn clean install -DskipTests`.                              |
| **2. SQL Over HTTP et services web avec Spring Boot** |                                                                                                                          |
| - Comprendre les relations entre comptes et clients | Avant de commencer, comprendre que les comptes dépendent des clients pour leur création.                                  |
| - Insertion des clients dans la base de données | Insérer 20 clients dans la base de données via des requêtes SQL, en utilisant les scripts générés par PostgreSQL.         |
| - Création de comptes via HTTP POST        | Créer des comptes en utilisant des requêtes HTTP POST, en respectant les relations clients-comptes spécifiées.            |
| **3. Documentation de l'API avec Swagger** |                                                                                                                          |
| - Ajout des dépendances Swagger            | Ajouter la dépendance `springdoc-openapi` dans le `pom.xml` pour activer la documentation Swagger.                         |
| - Annotation des endpoints                 | Annoter les méthodes du contrôleur avec `@Operation(summary = "description")` pour générer la documentation Swagger.     |
| - Test de Swagger                          | Accéder à la documentation générée à l'URL `http://localhost:8080/swagger-ui/index.html`.                                |
| **4. Implémentation de la journalisation** |                                                                                                                          |
| - Configuration basique du logging         | Ajouter et configurer la journalisation avec SLF4J et Logback dans `application.properties`.                             |
| - Utilisation de Logger dans le code       | Intégrer la journalisation dans `AccountsService` pour suivre les actions importantes, telles que la création, la mise à jour et la suppression des comptes.                                    |
| - Gestion avancée du logging               | Configurer Logback pour séparer les logs par niveau de sévérité (INFO, WARN, ERROR) afin de garantir une traçabilité optimale.                                      |
| **5. Test et manipulation des endpoints**  |                                                                                                                          |
| - Utilisation de Postman pour tester l'API | Tester les endpoints GET, POST, PUT, et DELETE en utilisant Postman pour interagir avec l'API Spring Boot.                |

### Détails sur les services web et les opérations SQL over HTTP

- **Compréhension des services web** : Les services web permettent l'interaction entre l'application et d'autres systèmes en utilisant des protocoles comme HTTP. Dans ce projet, les services web sont principalement utilisés pour effectuer des opérations CRUD (Create, Read, Update, Delete) sur les comptes et clients. L'utilisation de ces services vous permet de créer des clients et des comptes via des requêtes HTTP, d'effectuer des mises à jour, et de récupérer des données en interrogeant les endpoints définis dans le `AccountsController`.

- **Insertion des clients et des comptes via HTTP** : Utilisez Postman pour envoyer des requêtes HTTP POST qui créeront des entrées dans la base de données. Par exemple, vous pouvez insérer 20 clients en utilisant un script SQL, puis créer des comptes pour ces clients en envoyant des requêtes POST vers l'API. Les relations entre les entités clients et comptes doivent être respectées, comme spécifié dans les exigences du projet.

- **Documentation avec Swagger** : Swagger simplifie la documentation des API en générant automatiquement une interface utilisateur à partir de vos annotations dans le code. Vous pouvez naviguer facilement dans les différents endpoints, tester les requêtes directement depuis l'interface Swagger, et vérifier que votre API fonctionne comme prévu.

- **Journalisation des opérations** : Pour assurer une bonne traçabilité et faciliter le débogage, la journalisation est essentielle. En utilisant SLF4J et Logback, vous pouvez capturer et enregistrer les actions effectuées par votre application. Vous configurerez des appenders pour écrire les logs dans différents fichiers en fonction du niveau de sévérité (INFO, WARN, ERROR), ce qui vous aidera à analyser les comportements de l'application et à identifier les erreurs potentielles.

-----------------------------------
# 🏁 3 - Conclusion :
-----------------------------------

- Dans ce projet, vous avez appris à travailler avec un projet existant, en commençant par le cloner et le configurer pour votre environnement local. Vous avez mis en place un utilisateur et une base de données PostgreSQL, puis exécuté l'application sans l'aide d'un IDE, renforçant ainsi votre maîtrise des outils en ligne de commande comme Maven et Gradle. Vous avez ensuite approfondi votre compréhension des services web en utilisant SQL over HTTP pour manipuler les données clients et comptes via des requêtes HTTP, en respectant les relations entre ces entités.
- Un autre aspect crucial de ce projet a été la documentation de l'API avec Swagger, qui vous a permis de générer automatiquement une documentation interactive et facile à utiliser pour tester et explorer les endpoints de l'application. De plus, l'implémentation d'une journalisation détaillée avec SLF4J et Logback a permis de suivre les actions importantes dans l'application, garantissant ainsi une traçabilité efficace et facilitant le débogage en cas de problèmes.
- En utilisant Postman, vous avez testé les différents endpoints de l'API, validant ainsi le bon fonctionnement de l'application et vous assurant que toutes les opérations CRUD pouvaient être effectuées via des services web. Ce projet vous a permis de comprendre l'importance de la documentation, de la journalisation, et des tests dans le développement d'applications web robustes et maintenables.
- En conclusion, vous avez acquis une vue d'ensemble complète des processus de configuration, d'exécution, de documentation, de journalisation, et de test dans un projet Spring Boot, vous préparant ainsi à aborder des projets encore plus complexes à l'avenir. Vous avez également renforcé vos compétences dans l'utilisation des services web pour interagir avec des bases de données, vous assurant ainsi une maîtrise solide des concepts fondamentaux nécessaires à tout développeur moderne.
