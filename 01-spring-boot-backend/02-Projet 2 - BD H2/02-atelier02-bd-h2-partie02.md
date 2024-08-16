# 📚 Base de Données Persistante avec H2 -version 2

Cette version du projet vous guide pour utiliser H2 avec une base de données persistante sur le disque.


## 🚀 Étapes pour Exécuter cette Version du Projet

### 1. 🔍 Vérification des Fichiers Nécessaires

```bash
git clone https://github.com/hrhouma1/h2-persistance-EX2.git
cd h2-persistance-EX2
```


Assurez-vous d'avoir les deux fichiers suivants dans votre projet :

- **schema.sql** : Ce fichier est utilisé pour la création de la base de données.
- **data.sql** : Ce fichier ajoute des données initiales (seed data) à la base de données.

### 2. 🗂️ Emplacement de la Base de Données

La base de données sera créée ici : `C:\temp\test.mv.db`. Assurez-vous que ce chemin est accessible et que vous avez les permissions nécessaires pour y écrire.

### 3. 🌐 Connexion à la Console H2

Accédez à la console H2 via l'URL suivante : [http://localhost:8080/h2/](http://localhost:8080/h2/). Une fois sur la page de connexion, changez l'URL JDBC :

- **Ancienne URL JDBC** : `jdbc:h2:mem:testdb`
- **Nouvelle URL JDBC** : `jdbc:h2:file:C:/temp/test`

Cela permet de basculer la base de données en mode persistant.

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

### 🎯 Création d'une Nouvelle Base de Données

Vous pouvez tester la création d'une nouvelle base de données en exécutant la commande SQL suivante :

```sql
CREATE DATABASE HAYTHEM;
```

### 🔄 Déconnexion et Reconnexion

1. **Déconnexion** : Déconnectez-vous de la console H2, mais **n'arrêtez pas l'exécution de l'application**. Si vous arrêtez l'application, elle recréera la base de données à partir de `schema.sql`.

2. **Reconnexion** : Reconnectez-vous et vérifiez si les données et la base de données `HAYTHEM` sont toujours présentes.

   ➡️ **Observation** : Si la base de données `HAYTHEM` est encore là, cela signifie que les données sont persistantes. Sinon, cela indique que la base de données est réinitialisée à partir de `schema.sql`.

### 🛑 Arrêt et Redémarrage de l'Application

1. **Arrêt** : Arrêtez l'exécution de l'application.

2. **Redémarrage** : Redémarrez l'application. Vous remarquerez que tout est recréé à partir de `schema.sql`. Pour éviter cela, il peut être nécessaire de supprimer les fichiers `schema.sql` et `data.sql`.

### 💡 Autre Solution pour Initialisation avec des Données (SEED DATA)

Une alternative consiste à ajouter les requêtes d'insertion directement dans le fichier `data.sql`. Cela permet d'assurer que les données sont initialisées à chaque démarrage de l'application, tout en conservant la possibilité de persister les modifications.
