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


## Attention : si vous utilisez HTTPS, il se peut que la page n'apparaisse pas. Dans tous les cas, testez http://localhost:8080/.


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

- Ces requêtes vous permettront de voir les données présentes dans les tables **CITY** et **STUDENT**.


### 🎯 Création et Manipulation de la Base de Données `HAYTHEM`

Vous pouvez également tester la création et l'insertion de données dans une nouvelle table `HAYTHEM` pour comprendre comment H2 gère les bases de données en mémoire. Suivez les étapes ci-dessous :

1. **Connectez-vous à la Console H2** : Accédez à la console H2 en utilisant l'URL suivante : [http://localhost:8080/h2-console/](http://localhost:8080/h2-console/). Utilisez les informations de connexion appropriées.

2. **Création de la Table `HAYTHEM`** : Une fois connecté, vous pouvez exécuter la commande SQL suivante pour créer une table `HAYTHEM` :

   ```sql
   CREATE TABLE HAYTHEM (
       ID INT PRIMARY KEY,
       NAME VARCHAR(255)
   );
   ```

3. **Insertion de Données dans la Table `HAYTHEM`** : Ajoutez des données dans la table `HAYTHEM` en utilisant les commandes suivantes :

   ```sql
   INSERT INTO HAYTHEM (ID, NAME) VALUES (1, 'Alice');
   INSERT INTO HAYTHEM (ID, NAME) VALUES (2, 'Bob');
   INSERT INTO HAYTHEM (ID, NAME) VALUES (3, 'Charlie');
   ```

4. **Consultation des Données** : Vérifiez que les données ont été insérées correctement en exécutant la requête suivante :

   ```sql
   SELECT * FROM HAYTHEM;
   ```

⚠️ **Remarque Importante** : La base de données en mémoire, y compris les tables et les données que vous créez, est temporaire et sera effacée lorsque vous vous déconnecterez ou arrêterez l'application.

### 🔄 Déconnexion et Reconnexion

Après avoir créé la table `HAYTHEM` et inséré des données, suivez ces étapes pour observer le comportement de la base de données en mémoire :

1. **Déconnexion** : Déconnectez-vous de la console H2 en cliquant sur le bouton **Disconnect**.

2. **Reconnexion** : Reconnectez-vous immédiatement en utilisant les mêmes informations de connexion.

   ➡️ **Observation** : Vous remarquerez que la table `HAYTHEM` et les données insérées ne sont plus présentes après la reconnexion. Cela s'explique par le fait que H2 est configuré pour fonctionner en mémoire (`in-memory`), ce qui signifie que toutes les bases de données et les données créées dans cette session sont temporaires et non persistées.

### 📝 Explication

Pour bien comprendre pourquoi certaines données persistent et d'autres non, voici une explication détaillée :

- **Bases de données `CITY` et `STUDENT`** : Ces tables existent parce qu'elles sont définies dans les fichiers `schema.sql` et `data.sql`. Ces fichiers sont chargés automatiquement par Spring Boot lors du démarrage de l'application. Les tables sont initialisées à chaque démarrage, ce qui leur permet de toujours être présentes en mémoire tant que l'application est en cours d'exécution.

- **Table `HAYTHEM`** : Contrairement aux tables `CITY` et `STUDENT`, la table `HAYTHEM` que vous avez créée manuellement est stockée uniquement en mémoire. Elle disparaît lorsque l'application est arrêtée ou lorsque vous vous déconnectez de la console H2.





