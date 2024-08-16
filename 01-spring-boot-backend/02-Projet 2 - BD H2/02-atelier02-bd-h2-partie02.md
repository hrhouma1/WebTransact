# 📚 Base de Données Persistante avec H2 - Version 2

Cette version du projet vous guide pour utiliser H2 avec une base de données persistante sur le disque.

## 🚀 Étapes pour Exécuter cette Version du Projet

### 1.1 🔍 Vérification des Fichiers Nécessaires

```bash
git clone https://github.com/hrhouma1/h2-persistance-EX2.git
cd h2-persistance-EX2
```

Assurez-vous d'avoir les deux fichiers suivants dans votre projet :

- **schema.sql** : Ce fichier est utilisé pour créer la structure de la base de données.
- **data.sql** : Ce fichier initialise la base de données avec des données (seed data).

### 1.2 🛠️ Compilation et Exécution du Projet

- Utilisez les commandes Maven suivantes pour nettoyer, installer, et exécuter l'application :

```bash
mvn clean
mvn install -DskipTests
mvn spring-boot:run
```

### 2. 🗂️ Emplacement de la Base de Données

- La base de données sera créée à cet emplacement : `C:\temp\test.mv.db`. Assurez-vous que ce chemin est accessible et que vous disposez des permissions nécessaires pour y écrire.

- 💀 **Si vous n'avez pas les permissions nécessaires (par exemple, si vous utilisez une machine qui n'est pas la vôtre), créez manuellement le fichier `test.mv.db` dans `C:\temp`.**

### 3. 🌐 Connexion à la Console H2

Accédez à la console H2 via l'URL suivante : [http://localhost:8080/h2/](http://localhost:8080/h2/). Une fois sur la page de connexion, modifiez l'URL JDBC :

- **Ancienne URL JDBC** : `jdbc:h2:mem:testdb`
- **Nouvelle URL JDBC** : `jdbc:h2:file:C:/temp/test`

Cela permet de passer la base de données en mode persistant.

### 4. 🔎 Exécution des Requêtes SQL

Une fois connecté, exécutez la commande SQL suivante pour visualiser les données dans la table **TBL_EMPLOYEES** :

```sql
SELECT * FROM TBL_EMPLOYEES;
```

### 5. 📝 Insertion de Données

Insérez de nouvelles données dans la table **TBL_EMPLOYEES** en exécutant les commandes SQL suivantes :

```sql
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Emily', 'Clark', 'emily.clark@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('David', 'Taylor', 'david.taylor@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Sophia', 'Brown', 'sophia.brown@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('James', 'Davis', 'james.davis@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Isabella', 'Miller', 'isabella.miller@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Michael', 'Wilson', 'michael.wilson@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Charlotte', 'Moore', 'charlotte.moore@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Benjamin', 'Taylor', 'benjamin.taylor@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Amelia', 'Anderson', 'amelia.anderson@example.com');
INSERT INTO TBL_EMPLOYEES (FIRST_NAME, LAST_NAME, EMAIL) VALUES ('Ethan', 'Thomas', 'ethan.thomas@example.com');
```

### 6. 🔎 Vérification des Données

Après avoir inséré les nouvelles données, vérifiez qu'elles ont bien été ajoutées en exécutant :

```sql
SELECT * FROM TBL_EMPLOYEES;
```

### 🎯 Création d'une Nouvelle Table

1. **Création de la Table `HAYTHEM`** : Une fois connecté, vous pouvez exécuter la commande SQL suivante pour créer la table `HAYTHEM` :

   ```sql
   CREATE TABLE HAYTHEM (
       ID INT PRIMARY KEY,
       NAME VARCHAR(255)
   );
   ```

2. **Insertion de Données dans la Table `HAYTHEM`** : Ajoutez des données dans la table `HAYTHEM` en utilisant les commandes suivantes :

   ```sql
   INSERT INTO HAYTHEM (ID, NAME) VALUES (1, 'Alice');
   INSERT INTO HAYTHEM (ID, NAME) VALUES (2, 'Bob');
   INSERT INTO HAYTHEM (ID, NAME) VALUES (3, 'Charlie');
   ```

3. **Consultation des Données** : Vérifiez que les données ont été insérées correctement en exécutant la requête suivante :

   ```sql
   SELECT * FROM HAYTHEM;
   ```

### 🔄 Déconnexion et Reconnexion

1. **Déconnexion** : Déconnectez-vous de la console H2, mais **n'arrêtez pas l'exécution de l'application**. Si vous arrêtez l'application, elle recréera la base de données à partir de `schema.sql`.

2. **Reconnexion** : Reconnectez-vous et vérifiez si les données et la table `HAYTHEM` sont toujours présentes.

   ➡️ **Observation** : Tant que l'application est en cours d'exécution, vous ne pouvez pas vérifier si les données sont persistantes, mais vous pouvez voir que les données sont présentes en mémoire.

### 🛑 Arrêt et Redémarrage de l'Application

1. **Arrêt** : Arrêtez l'exécution de l'application.

2. **Redémarrage** :

Avant de redémarrer l'application, supprimez les fichiers `schema.sql` et `data.sql` pour vérifier la persistance. Sinon, si vous les conservez, tout sera recréé à partir de `schema.sql`, et vous ne verrez pas le concept de persistance.

### 💡 Autre Solution pour Initialisation avec des Données (Seed Data)

Une alternative consiste à ajouter les requêtes d'insertion directement dans le fichier `data.sql`. Cela garantit que les données sont initialisées à chaque démarrage de l'application, tout en conservant la possibilité de persister les modifications.

