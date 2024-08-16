# 📚 Bases de données en mémoire vive H2 - partie 1

- Ce travail est une version modifiée et améliorée du tutoriel disponible sur TutorialPoint.com.

## 🚀 Étapes pour Exécuter ce Projet

### 1. 📥 Cloner le Dépôt Git

Commencez par cloner le dépôt Git suivant :

```bash
git clone https://github.com/hrhouma1/h2-memoire-EX1.git
```

### 2. 🔍 Vérification des Fichiers Nécessaires

Assurez-vous d'avoir les deux fichiers suivants dans votre projet :

- **schema.sql** : Ce fichier est utilisé pour la création de la base de données.
- **data.sql** : Ce fichier ajoute des données initiales (seed data) à la base de données.

### 3. 🛠️ Compilation et Exécution du Projet

Utilisez les commandes Maven suivantes pour nettoyer, installer, et exécuter l'application :

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

### 4. ⚙️ Configuration de l'Application

Les informations de connexion à la base de données H2 sont définies dans le fichier `application.properties`. Assurez-vous que les paramètres suivants sont configurés correctement :

```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:javatpoint
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update
```

### 5. 🌐 Connexion à la Console H2

Une fois l'application démarrée, connectez-vous à la console H2 en accédant à l'URL suivante dans votre navigateur :

[http://localhost:8080/h2-console/](http://localhost:8080/h2-console/)

Lorsque vous y êtes, utilisez les informations suivantes pour vous connecter :

- **JDBC URL** : `jdbc:h2:mem:testdb`
- **User Name** : `sa`
- **Password** : (laissez vide)

### 6. 🔎 Exécution des Requêtes SQL

Une fois connecté, vous pouvez exécuter les commandes SQL suivantes :

```sql
SELECT * FROM CITY;
SELECT * FROM STUDENT;
```

Ces requêtes vous permettront de voir les données présentes dans les tables **CITY** et **STUDENT**.

### 🎯 Création d'une Nouvelle Base de Données

Vous pouvez également tester la création d'une nouvelle base de données pour comprendre comment H2 gère les bases de données en mémoire. Suivez les étapes ci-dessous :

1. **Connectez-vous à la Console H2** : Accédez à la console H2 en utilisant l'URL suivante : [http://localhost:8080/h2-console/](http://localhost:8080/h2-console/). Utilisez les informations de connexion appropriées.

2. **Exécution de la Commande SQL** : Une fois connecté, vous pouvez exécuter la commande SQL suivante pour créer une nouvelle base de données appelée `HAYTHEM` :

   ```sql
   CREATE DATABASE HAYTHEM;
   ```

   ⚠️ **Remarque Importante** : La commande ci-dessus est acceptée par H2, mais il est important de noter que dans le mode en mémoire, la création d'une base de données distincte comme `HAYTHEM` n'est pas persistée au-delà de la session actuelle. Cette base de données existera uniquement durant la session en cours et sera effacée lorsque vous vous déconnecterez.

### 🔄 Déconnexion et Reconnexion

Après avoir créé la base de données `HAYTHEM`, suivez ces étapes pour observer le comportement de la base de données en mémoire :

1. **Déconnexion** : Déconnectez-vous de la console H2 en cliquant sur le bouton **Disconnect**.

2. **Reconnexion** : Reconnectez-vous immédiatement en utilisant les mêmes informations de connexion.

   ➡️ **Observation** : Vous remarquerez que la base de données `HAYTHEM` n'est plus présente. Cela s'explique par le fait que H2 est configuré pour fonctionner en mémoire (`in-memory`), ce qui signifie que toutes les bases de données créées dans cette session sont temporaires et non persistées.

### 📝 Explication

Pour bien comprendre pourquoi certaines données persistent et d'autres non, voici une explication détaillée :

- **Bases de données `CITY` et `STUDENT`** : Ces tables existent parce qu'elles sont définies dans les fichiers `schema.sql` et `data.sql`. Ces fichiers sont chargés automatiquement par Spring Boot lors du démarrage de l'application. Les tables sont initialisées à chaque démarrage, ce qui leur permet de toujours être présentes en mémoire tant que l'application est en cours d'exécution.
  
- **Base de données `HAYTHEM`** : Contrairement aux tables `CITY` et `STUDENT`, la base de données `HAYTHEM` que vous avez créée manuellement n'est pas définie dans les fichiers d'initialisation `schema.sql` et `data.sql`. Elle est créée uniquement en mémoire et n'est pas sauvegardée sur le disque, ce qui explique pourquoi elle disparaît une fois que vous vous déconnectez de la console H2.
