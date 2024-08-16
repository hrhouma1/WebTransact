# 📚 Application Spring Boot avec Base de Données H2 Persistante - Version 3

Cette version du projet est une amélioration significative par rapport aux versions précédentes. Elle utilise une base de données H2 persistante, permettant de conserver les données entre les redémarrages de l'application, contrairement à la version 1 qui utilisait uniquement une base de données en mémoire.

## 🚀 Instructions pour Exécuter cette Version du Projet

### 1. 📥 Cloner le Dépôt Git

Commencez par cloner le dépôt contenant le projet :

```bash
git clone https://github.com/hrhouma1/h2-persistance-EX3.git
cd h2-persistance-EX3
```

### 2. 🔍 Vérification et Renommage des Fichiers Nécessaires

#### 2.1 Comprendre le Rôle des Fichiers SQL

Dans cette version, les fichiers `schema.sql` et `data.sql` ont été renommés en `xxschemaCity.sql` et `xxdataCity.sql`. Ce renommage empêche Spring Boot de les détecter et de les exécuter automatiquement lors du démarrage de l'application.

**Pourquoi ?** Cela vous permet de contrôler manuellement la création et l'initialisation de la base de données, ce qui est essentiel pour comprendre comment les scripts SQL interagissent avec votre application.

#### 2.2 Renommer les Fichiers pour Initialisation

1. **Renommez `xxschemaCity.sql` en `schema.sql`** : Cela permettra à Spring Boot de détecter et d'exécuter ce fichier au démarrage de l'application pour créer la structure de la base de données.

2. **Renommez `xxdataCity.sql` en `data.sql`** : De la même manière, ce fichier sera détecté et exécuté pour insérer les données initiales dans la base de données.

3. **Ajoutez vos propres modifications** : Avant d'exécuter l'application, ajoutez la création des tables supplémentaires que vous souhaitez, comme `TBL_EMPLOYEES` et `DIRECTEURS`, dans `schema.sql`. De plus, vous pouvez insérer des données supplémentaires dans `data.sql`.

Voici un exemple de contenu que vous pourriez ajouter :

- **Ajout dans `schema.sql` :**

  ```sql
  CREATE TABLE TBL_EMPLOYEES (
      id INT AUTO_INCREMENT PRIMARY KEY,
      first_name VARCHAR(250) NOT NULL,
      last_name VARCHAR(250) NOT NULL,
      email VARCHAR(250) DEFAULT NULL
  );

  CREATE TABLE DIRECTEURS (
      ID INT PRIMARY KEY,
      NAME VARCHAR(255)
  );
  ```

- **Ajout dans `data.sql` :**

  ```sql
  INSERT INTO TBL_EMPLOYEES (first_name, last_name, email) VALUES ('Emily', 'Clark', 'emily.clark@example.com');
  INSERT INTO TBL_EMPLOYEES (first_name, last_name, email) VALUES ('David', 'Taylor', 'david.taylor@example.com');

  INSERT INTO DIRECTEURS (ID, NAME) VALUES (1, 'Alice');
  INSERT INTO DIRECTEURS (ID, NAME) VALUES (2, 'Bob');
  ```

#### 2.3 Renommer les Fichiers Après l'Initialisation

Une fois que vous avez exécuté l'application pour la première fois et que les tables sont créées, vous ne voudrez peut-être plus que Spring Boot exécute ces fichiers automatiquement. 

1. **Renommez `schema.sql` et `data.sql` en `xxschemaCity.sql` et `xxdataCity.sql`** : Cela empêchera Spring Boot de les détecter et de réinitialiser la base de données à chaque démarrage. Cette étape est cruciale pour préserver les modifications de la base de données que vous effectuez directement via la console H2 ou des scripts SQL.

2. **Recompilez et exécutez l'application :**

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

### 3. 🛠️ Compilation et Exécution du Projet

Une fois les fichiers renommés et les modifications effectuées, vous pouvez compiler et exécuter le projet avec les commandes suivantes :

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

**Question : Comment arrêter l'exécution de l'application ?**

Pour arrêter l'application, vous pouvez utiliser `Ctrl+C` dans le terminal où l'application est en cours d'exécution.

**Question : Quand faut-il réexécuter la commande ?**

Si vous apportez des modifications aux fichiers source ou à la configuration, ou si vous avez besoin de redémarrer l'application pour refléter les nouvelles modifications, vous devrez réexécuter la commande suivante :

```bash
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

**Remarque :** Le paramètre `DB_CLOSE_ON_EXIT=FALSE` garantit que la base de données reste accessible même après la fermeture de l'application, tandis que `AUTO_RECONNECT=TRUE` permet de rétablir automatiquement la connexion si elle est perdue.

### 5. 🌐 Connexion à la Console H2

Accédez à la console H2 via l'URL suivante : [http://localhost:8080/h2/](http://localhost:8080/h2/).

**Question : Pourquoi l'URL ne fonctionne-t-elle pas ?**

Lorsque vous essayez d'accéder à la console H2 avec cette URL, il est possible que cela ne fonctionne pas immédiatement. Cela peut être dû à une absence ou une mauvaise configuration du chemin de la console H2 dans votre fichier `application.properties`.

### 🔧 Solution : Configurer le Chemin de la Console H2

Pour résoudre ce problème, vous devez ajouter ou vérifier la configuration suivante dans le fichier `application.properties` :

```properties
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

Ces paramètres permettent d'activer la console H2 et de définir le chemin correct pour y accéder.

**Question : Où se trouve le fichier `application.properties` ?**

Le fichier `application.properties` se trouve dans le répertoire `src/main/resources` de votre projet.

### **Recompilez et exécutez l'application :**

Après avoir configuré le chemin correct pour la console H2, vous devez recompiler et exécuter l'application pour que les changements prennent effet.

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

Une fois ces paramètres configurés, accédez à la console H2 via l'URL suivante : [http://localhost:8080/h2-console/](http://localhost:8080/h2-console/). Lors de la connexion, utilisez l'URL JDBC que vous avez configurée dans `application.properties` :

- **JDBC URL** : `jdbc:h2:C:/data/sampledata`

Cela vous permettra d'accéder à la console H2 et d'interagir avec votre base de données persistante.

### 6. 🔎 Exécution des Requêtes SQL

Une fois connecté, vous pouvez interagir avec votre base de données persistante en exécutant des requêtes SQL.

- **Vérifiez les données existantes dans la table `CITY` :**

  ```sql
  SELECT * FROM CITY;
  ```

- **Insérez de nouvelles données dans la table `TBL_EMPLOYEES` :**

  ```sql
  INSERT INTO TBL_EMPLOYEES (first_name, last_name, email) VALUES ('Emily', 'Clark', 'emily.clark@example.com');
  ```

- **Vérifiez que les nouvelles données ont bien été insérées :**

  ```sql
  SELECT * FROM TBL_EMPLOYEES;
  ```

### 7. 🛑 Arrêt et Redémarrage de l'Application

1. **Arrêt** : Pour arrêter l'application, utilisez `Ctrl+C` dans le terminal.

2. **Redémarrage** : Pour redémarrer l'application après avoir effectué des modifications ou pour relancer l'application, utilisez la commande suivante :

```bash
mvn spring-boot:run
```

**Question : Que se passe-t-il si vous ne renommez pas les fichiers SQL après avoir démarré l'application une première fois ?**

Si vous ne renommez pas les fichiers `schema.sql` et `data.sql`, Spring Boot les détectera et les exécutera à chaque démarrage, ce qui peut réinitialiser la base de données et perdre toutes les modifications apportées depuis la dernière exécution.

### 8. 💡 Initialisation avec des Données (SEED DATA)

Si vous souhaitez initialiser la base de données avec des données spécifiques à chaque démarrage, vous pouvez ajouter les requêtes d'insertion directement dans le fichier `xxdataCity.sql`.

Pour utiliser ces données à nouveau, renommez `xxdataCity.sql`

 en `data.sql` et recompilez l'application :

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

---

# Important:

- En renommant les fichiers `schema.sql` et `data.sql` en `xxschemaCity.sql` et `xxdataCity.sql`, vous prenez le contrôle manuel de l'initialisation de votre base de données. Cela vous permet de comprendre et de gérer l'impact des scripts SQL sur votre application.

- Spring Boot détecte par défaut les fichiers `schema.sql` et `data.sql` dans `src/main/resources` et les exécute automatiquement pour configurer la base de données. En les renommant, vous empêchez cette exécution automatique et évitez la réinitialisation non désirée de la base de données.
