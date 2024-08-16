# 📚 Application Spring Boot avec Base de Données H2 Persistante - version 3

- Cette version du projet est une amélioration significative par rapport aux versions précédentes. 
- Elle utilise une base de données H2 persistante, permettant de conserver les données entre les redémarrages de l'application, contrairement à la version 1  qui utilisait uniquement  une base de données en mémoire.

## 🚀 Instructions pour Exécuter cette Version du Projet

### 1. 📥 Cloner le Dépôt Git

Commencez par cloner le dépôt Git correspondant à cette version :

```bash
git clone <votre-url-depot>
```

### 2. 🔍 Vérification des Fichiers Nécessaires

Dans cette version, les fichiers `schema.sql` et `data.sql` ont été renommés en `xxschemaCity.sql` et `xxdataCity.sql`. Ce renommage empêche Spring Boot de les détecter et de les exécuter automatiquement lors du démarrage de l'application. Cela vous permet de contrôler manuellement la création et l'initialisation de la base de données.

Assurez-vous que les fichiers suivants sont présents dans le répertoire `src/main/resources` de votre projet :

- **xxschemaCity.sql** : Ce fichier est utilisé pour la création de la base de données.
- **xxdataCity.sql** : Ce fichier ajoute des données initiales (seed data) à la base de données.

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
spring.datasource.url=jdbc:h2:C:/data/sampledata;DB_CLOSE_ON_EXIT=FALSE;AUTO_RECONNECT=TRUE
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=   
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update
```

**Remarque :** Le paramètre `DB_CLOSE_ON_EXIT=FALSE` permet de s'assurer que la base de données reste accessible même après la fermeture de l'application, tandis que `AUTO_RECONNECT=TRUE` permet de rétablir automatiquement la connexion si elle est perdue.

### 5. 🌐 Connexion à la Console H2

Accédez à la console H2 via l'URL suivante : [http://localhost:8080/h2/](http://localhost:8080/h2/). Lors de la connexion, utilisez l'URL JDBC configurée dans `application.properties` :

- **JDBC URL** : `jdbc:h2:C:/data/sampledata`

### 6. 🔎 Exécution des Requêtes SQL

Une fois connecté, vous pouvez exécuter les requêtes SQL suivantes pour interagir avec votre base de données persistante :

- Pour vérifier les données existantes dans la table **CITY** (chargées à partir de `xxdataCity.sql`) :

  ```sql
  SELECT * FROM CITY;
  ```

- Pour insérer de nouvelles données dans la table **TBL_EMPLOYEES** (si vous avez une telle table) :

  ```sql
  INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST NAME, EMAIL) VALUES ('Emily', 'Clark', 'emily.clark@example.com');
  ```

- Pour vérifier que les nouvelles données ont bien été insérées :

  ```sql
  SELECT * FROM TBL_EMPLOYEES;
  ```

### 7. 🎯 Création d'une Nouvelle Base de Données

Vous pouvez tester la création d'une nouvelle base de données en exécutant la commande suivante :

```sql
CREATE DATABASE HAYTHEM;
```

### 8. 🔄 Déconnexion et Reconnexion

1. **Déconnexion** : Déconnectez-vous de la console H2. **Attention : N'arrêtez pas l'exécution de l'application**, sinon la base de données sera recréée à partir de `xxschemaCity.sql`.

2. **Reconnexion** : Reconnectez-vous et vérifiez si la base de données `HAYTHEM` et les autres données sont toujours présentes.

   ➡️ **Observation** : Si `HAYTHEM` est toujours là, cela signifie que la persistance fonctionne correctement. Sinon, cela indique que la base de données a été réinitialisée à partir de `xxschemaCity.sql`.

### 9. 🛑 Arrêt et Redémarrage de l'Application

1. **Arrêt** : Arrêtez l'exécution de l'application.

2. **Redémarrage** : Redémarrez l'application. Vous remarquerez que la base de données est recréée à partir de `xxschemaCity.sql`. Pour éviter cela, il peut être nécessaire de supprimer ou de modifier `xxschemaCity.sql` et `xxdataCity.sql`.

### 10. 💡 Initialisation avec des Données (SEED DATA)

Si vous souhaitez initialiser la base de données avec des données spécifiques à chaque démarrage, ajoutez les requêtes d'insertion directement dans le fichier `xxdataCity.sql`.

----
# Important:
----

- Si nous avons renommé les fichiers `schema.sql` et `data.sql` en `xxschemaCity.sql` et `xxdataCity.sql`, cela signifie que nous ne souhaitons pas que Spring Boot les détecte automatiquement et les utilise pour créer ou initialiser la base de données au démarrage de l'application.

- Spring Boot, par défaut, détecte les fichiers nommés `schema.sql` et `data.sql` dans le répertoire `src/main/resources` et les exécute automatiquement pour configurer la base de données.
- En les renommant, nous empêchons cette exécution automatique, ce qui nous permet de contrôler manuellement quand et comment ces scripts SQL sont utilisés.
