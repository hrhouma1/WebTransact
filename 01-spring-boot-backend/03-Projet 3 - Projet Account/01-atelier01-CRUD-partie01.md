# 🏁 Partie 1 : Lancement de l'Application et Configuration de la Base de Données PostgreSQL sur Windows

Ce guide vous expliquera comment cloner le projet, l'ouvrir, configurer la base de données PostgreSQL sur Windows, et lancer l'application en utilisant Maven et Spring Boot.

## 🚀 Étapes à suivre :

### 1️⃣ Cloner le projet
```bash
git clone https://github.com/hrhouma1/accounts-v1.git
```

### 2️⃣ Accéder au répertoire du projet
```bash
cd accounts-v1
```

### 3️⃣ Ouvrir le projet dans votre éditeur de code (par exemple, Visual Studio Code)
```bash
code .
```

---

## 🛠️ Configuration de la Base de Données PostgreSQL sur Windows

Avant de lancer l'application, il est nécessaire de configurer la base de données PostgreSQL sur votre système Windows.

### 1️⃣ Créer l'utilisateur PostgreSQL `hrgres` et la base de données `microDemo`

#### 1.1 **Ouvrir pgAdmin ou l'invite de commande PostgreSQL**

- **Via pgAdmin** : Utilisez l'interface graphique pour créer un nouvel utilisateur et une base de données ( *VOIR : 01-spring-boot-backend/01-Projet 1 - Hello World/05-atelier05-hello-persistance-ORM.md* ➡️ **point 2.5 (E) 05-atelier05-hello-persistance-ORM.md**) 
- **Via l'invite de commande** : Ouvrez l'invite de commande PostgreSQL.

#### 1.2 **Créer l'utilisateur `hrgres` avec un mot de passe**

Si vous utilisez l'invite de commande PostgreSQL :
```sql
CREATE USER hrgres WITH PASSWORD 'hrgres';
```

Dans pgAdmin :
- Allez dans la section "Login/Group Roles".
- Faites un clic droit et sélectionnez "Create" > "Login/Group Role".
- Entrez `hrgres` comme nom d'utilisateur et définissez le mot de passe sur `hrgres`.

#### 1.3 **Créer la base de données `microDemo`**

Si vous utilisez l'invite de commande PostgreSQL :
```sql
CREATE DATABASE microDemo;
```

Dans pgAdmin :
- Allez dans la section "Databases".
- Faites un clic droit et sélectionnez "Create" > "Database".
- Entrez `microDemo` comme nom de la base de données.

#### 1.4 **Attribuer tous les privilèges à l'utilisateur `hrgres` sur la base de données `microDemo`**

Si vous utilisez l'invite de commande PostgreSQL :
```sql
GRANT ALL PRIVILEGES ON DATABASE microDemo TO hrgres;
```

Dans pgAdmin :
- Allez dans la section "Object", sélectionnez "Database", puis choisissez `microDemo`.
- Allez dans "Properties" et sous "Privileges", attribuez tous les privilèges à l'utilisateur `hrgres`.

### 2️⃣ Configurer les propriétés de connexion dans l'application

1. **Ouvrez le fichier `application.properties` (ou `application.yml`)** dans votre éditeur de code et ajoutez/modifiez les configurations suivantes :

```properties
spring.datasource.driverClassName=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/microDemo
spring.datasource.username=hrgres
spring.datasource.password=hrgres
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

server.port=8080
```

> **💡 Remarque :** Assurez-vous que les informations de connexion (`url`, `username`, `password`) correspondent à votre configuration locale.

---

## 🏃‍♂️ Lancer l'Application

### 1️⃣ Nettoyer le projet avec Maven
```bash
mvn clean
```

### 2️⃣ Compiler et installer les dépendances sans exécuter les tests
```bash
mvn install -DskipTests
```

### 3️⃣ Lancer l'application avec Spring Boot
```bash
mvn spring-boot:run
```

# Testez : 

- http://127.0.0.1:8080/accounts
 
 # Explications: 
 
 1. **Vous allez avoir une page vide étant donné que nous n'avons pas de données dans la table accounts**
 2. **Vous pouvez maintenant explorer la structure en couches ==> Allez au dossier 00-theorie**
 3. **Exercice 01: Explorez le code dans AccountsController.java dans le dossier controller**
 4. **Exercice 02: Donnez les différents points de terminaisons et les méthodes invoqués dans le controller, ainsi que les méthodes correpondantes dans le service et repository**



---

# Réponses : 
----


---
# **Exercice 01: Exploration du code dans AccountsController.java**
---

**Résumé de l'exploration :**

Le code `AccountsController.java` dans le dossier controller est un contrôleur RESTful qui gère les requêtes HTTP pour les comptes bancaires. Il contient des annotations pour chaque méthode afin de décrire les opérations réalisables, telles que la récupération, la création, la mise à jour et la suppression de comptes.


# ===> Table qui résume les points de terminaison (endpoints) et les méthodes correspondantes dans le contrôleur `AccountsController.java` :


| **Endpoint (URI)**           | **Méthode HTTP** | **Méthode dans AccountsController**                  |
|------------------------------|------------------|-----------------------------------------------------|
| `/myAccount/{id}`             | `GET`            | `getAccountDetails(Long id)`                         |
| `/accounts`                   | `GET`            | `getAllAccounts()`                                   |
| `/newAccount`                 | `POST`           | `newAccount(Accounts accounts)`                      |
| `/update/{id}`                | `PUT`            | `updateAccount(Long id, Accounts updateAccounts)`    |
| `/deleteAccount/{id}`         | `DELETE`         | `deleteAccount(Long id)`                             |

Cette table montre  l'association entre chaque point de terminaison, la méthode HTTP utilisée, et la méthode correspondante dans le contrôleur `AccountsController.java`.


---

# **Exercice 02: Tableau comparatif des points de terminaison et des méthodes correspondantes**

---

| **Point de terminaison (URI)** | **Méthode HTTP** | **Méthode dans AccountsController** | **Méthode dans AccountsService** | **Méthode dans AccountsRepository** |
|---------------------------------|------------------|-------------------------------------|-----------------------------------|--------------------------------------|
| `/myAccount/{id}`               | `GET`            | `getAccountDetails(Long id)`        | `getAccountsById(long id)`        | `findById(Long id)`                  |
| `/accounts`                     | `GET`            | `getAllAccounts()`                  | `getAllAccounts()`                | `findAll()`                          |
| `/newAccount`                   | `POST`           | `newAccount(Accounts accounts)`     | `save(Accounts accounts)`         | `save(Accounts accounts)`            |
| `/update/{id}`                  | `PUT`            | `updateAccount(Long id, Accounts updateAccounts)` | `updateAccount(long id, Accounts updateAccounts)` | `findById(Long id)` puis `save(Accounts accounts)` |
| `/deleteAccount/{id}`           | `DELETE`         | `deleteAccount(Long id)`            | `deleteAccount(Long id)`          | `deleteById(Long id)`                |

### **Détails des Méthodes**

#### **AccountsController.java**
- `getAccountDetails(Long id)`: Récupère les détails d'un compte spécifique à partir de l'identifiant fourni.
- `getAllAccounts()`: Récupère tous les comptes disponibles.
- `newAccount(Accounts accounts)`: Crée un nouveau compte avec les détails fournis.
- `updateAccount(Long id, Accounts updateAccounts)`: Met à jour un compte existant avec de nouvelles informations.
- `deleteAccount(Long id)`: Supprime un compte spécifique en utilisant son identifiant.

#### **AccountsService.java**
- `getAccountsById(long id)`: Cherche et renvoie un compte à partir de son identifiant.
- `getAllAccounts()`: Récupère une liste de tous les comptes disponibles.
- `save(Accounts accounts)`: Enregistre un nouveau compte après avoir vérifié que le client existe.
- `updateAccount(long id, Accounts updateAccounts)`: Met à jour les détails d'un compte existant si le compte est trouvé.
- `deleteAccount(Long id)`: Supprime un compte par son identifiant.

#### **AccountsRepository.java**
- `findById(Long id)`: Cherche un compte à partir de son identifiant (méthode héritée de `CrudRepository`).
- `findAll()`: Récupère tous les comptes (méthode héritée de `CrudRepository`).
- `save(Accounts accounts)`: Sauvegarde un compte dans la base de données (méthode héritée de `CrudRepository`).
- `deleteById(Long id)`: Supprime un compte par son identifiant (méthode héritée de `CrudRepository`).
- `findByCustomerId(int customerId)`: Cherche un compte à partir de l'identifiant du client.





----
----

---

## 🚨 Résolution des Problèmes : Port 8080 Occupé

---
Si vous rencontrez une erreur indiquant que le port 8080 est déjà utilisé, suivez ces étapes :

### 1️⃣ Vérifier les processus utilisant le port 8080

Ouvrez l'invite de commande en tant qu'administrateur et exécutez :
```bash
netstat -ano | findstr :8080
```

### 2️⃣ Terminer le processus occupant le port 8080

Exécutez la commande suivante en remplaçant `numero_pid` par l'ID du processus récupéré :
```bash
taskkill /F /PID numero_pid
```

### 3️⃣ Relancer l'application
```bash
mvn spring-boot:run
```

---

# 🏁 Partie 2 : Gestion des Comptes sans Auto-Incrément et Ajout de Clients

Dans cette partie, nous allons gérer les comptes bancaires associés aux clients, en respectant certaines contraintes, notamment l'absence d'auto-incrémentation pour les comptes. **Assurez-vous de bien comprendre les relations entre les clients et les comptes avant de commencer.**

## ❗ Remarque Importante

Avant de commencer cette partie, il est essentiel de comprendre la relation entre les `accounts` et les `customers`. **Nous ne pouvons pas créer un compte sans avoir de clients.** C'est pourquoi il est impératif de commencer par la Partie 4 (ajout de 20 clients) avant de revenir ici pour tester les comptes. Vous devez ajouter les 20 clients avant de passer à la gestion des comptes.

## 🎯 Objectif

Créer 12 comptes via des requêtes POST selon la répartition suivante :
- **Client 1** : comptes 1, 11, 21
- **Client 2** : comptes 2, 12, 22
- **Client 3** : comptes 3, 13, 23
- **Client 4** : comptes 4, 14, 24



---

## 📝 Étapes

### 1️⃣ Insertion des Clients via SQL

Commencez par insérer les clients dans la base de données en suivant les étapes ci-dessous :

| **Customer ID** | **Date de Création** | **Email**                | **Numéro de Téléphone** | **Nom**           |
|-----------------|----------------------|--------------------------|-------------------------|-------------------|
| 1               | 2023-01-01           | email1@example.com        | 1000000001              | Name One          |
| 2               | 2023-01-02           | email2@example.com        | 1000000002              | Name Two          |
| 3               | 2023-01-03           | email3@example.com        | 1000000003              | Name Three        |
| 4               | 2023-01-04           | email4@example.com        | 1000000004              | Name Four         |
| 5               | 2023-01-05           | email5@example.com        | 1000000005              | Name Five         |
| 6               | 2023-01-06           | email6@example.com        | 1000000006              | Name Six          |
| 7               | 2023-01-07           | email7@example.com        | 1000000007              | Name Seven        |
| 8               | 2023-01-08           | email8@example.com        | 1000000008              | Name Eight        |
| 9               | 2023-01-09           | email9@example.com        | 1000000009              | Name Nine         |
| 10              | 2023-01-10           | email10@example.com       | 1000000010              | Name Ten          |
| 11              | 2023-01-11           | email11@example.com       | 1000000011              | Name Eleven       |
| 12              | 2023-01-12           | email12@example.com       | 1000000012              | Name Twelve       |
| 13              | 2023-01-13           | email13@example.com       | 1000000013              | Name Thirteen     |
| 14              | 2023-01-14           | email14@example.com       | 1000000014              | Name Fourteen     |
| 15              | 2023-01-15           | email15@example.com       | 1000000015              | Name Fifteen      |
| 16              | 2023-01-16           | email16@example.com       | 1000000016              | Name Sixteen      |
| 17              | 2023-01-17           | email17@example.com       | 1000000017              | Name Seventeen    |
| 18              | 2023-01-18           | email18@example.com       | 1000000018              | Name Eighteen     |
| 19              | 2023-01-19           | email19@example.com       | 1000000019              | Name Nineteen     |
| 20              | 2023-01-20           | email20@example.com       | 1000000020              | Name Twenty       |

#### 1.1 **Accéder à PostgreSQL**

- Allez dans pgAdmin ou ouvrez l'invite de commande PostgreSQL.

#### 1.2 **Insérer les 20 clients dans la table `customer`**
```sql
INSERT INTO public.customer (customer_id, create_dt, email, mobile_number, name)
VALUES
(1, '2023-01-01', 'email1@example.com', '1000000001', 'Name One'),
(2, '2023-01-02', 'email2@example.com', '1000000002', 'Name Two'),
(3, '2023-01-03', 'email3@example.com', '1000000003', 'Name Three'),
(4, '2023-01-04', 'email4@example.com', '1000000004', 'Name Four'),
(5, '2023-01-05', 'email5@example.com', '1000000005', 'Name Five'),
(6, '2023-01-06', 'email6@example.com', '1000000006', 'Name Six'),
(7, '2023-01-07', 'email7@example.com', '1000000007', 'Name Seven'),
(8, '2023-01-08', 'email8@example.com', '1000000008', 'Name Eight'),
(9, '2023-01-09', 'email9@example.com', '1000000009', 'Name Nine'),
(10, '2023-01-10', 'email10@example.com', '1000000010', 'Name Ten'),
(11, '2023-01-11', 'email11@example.com', '1000000011', 'Name Eleven'),
(12, '2023-01-12', 'email12@example.com', '1000000012', 'Name Twelve'),
(13, '2023-01-13', 'email13@example.com', '1000000013', 'Name Thirteen'),
(14, '2023-01-14', 'email14@example.com', '1000000014', 'Name Fourteen'),
(15, '2023-01-15', 'email15@example.com', '1000000015', 'Name Fifteen'),
(16, '2023-01-16', 'email16@example.com', '1000000016', 'Name Sixteen'),
(17, '2023-01-17', 'email17@example.com', '1000000017', 'Name Seventeen'),
(18, '2023-01-18', 'email18@example.com', '1000000018', 'Name Eighteen'),
(19, '2023-01-19', 'email19@example.com', '1000000019', 'Name Nineteen'),
(20, '2023-01-20', 'email20@example.com', '1000000020', 'Name Twenty');
```

#### 1.3 **Vérifier l'insertion des clients**
```sql
SELECT * FROM public.customer;
```

---

### 2️⃣ Insertion des Comptes via HTTP (POST) ➕

Une fois les 20 clients ajoutés, vous pouvez commencer à créer les comptes associés via des requêtes POST.

| **Client** | **Compte** | **Type de Compte** | **Adresse**  | **Date de Création** |
|------------|------------|--------------------|--------------|----------------------|
| Client 1   | Compte 1    | Checking           | 123 Main St  | 2023-01-02           |
| Client 1   | Compte 11   | Savings            | 123 Main St  | 2023-01-02           |
| Client 1   | Compte 21   | Checking           | 123 Main St  | 2023-01-02           |
| Client 2   | Compte 2    | Savings            | 456 Main St  | 2023-01-03           |
| Client 2   | Compte 12   | Checking           | 456 Main St  | 2023-01-03           |
| Client 2   | Compte 22   | Savings            | 456 Main St  | 2023-01-03           |
| Client 3   | Compte 3    | Checking           | 789 Elm St   | 2023-01-04           |
| Client 3   | Compte 13   | Savings            | 789 Elm St   | 2023-01-04           |
| Client 3   | Compte 23   | Checking           | 789 Elm St   | 2023-01-04           |
| Client 4   | Compte 4    | Savings            | 101 Pine St  | 2023-01-05           |
| Client 4   | Compte 14   | Checking           | 101 Pine St  | 2023-01-05           |
| Client 4   | Compte 24   | Savings            | 101 Pine St  | 2023-01-05           |

#### 2.1 **Créer un compte pour un client via Postman**

Exemple pour créer un compte pour le Client 1 :
- Ouvrez Postman.
- Choisissez `POST`.
- URL : `http://localhost:8080/newAccount`.
- Body -> raw -> JSON :
```json
{
  "accountNumber": 1,
  "customerId": 1,
  "accountType": "Checking",
  "branchAddress": "123 Main St",
  "createDt": "2023-01-02"
}
```

#### 2.2 **Vérifier l'insertion du compte**

- Ouvrir le navigateur et tester cette URL : `http://localhost:8080/accounts`.
- Ou utilisez Postman pour effectuer un GET sur `http://localhost:8080/accounts`.

#### 2.3 **Répéter l'opération pour les autres comptes**

Voici les JSON pour les autres comptes :

- **Client 2 :**
  ```json
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  }
  ```
  ```json
  {
    "accountNumber": 12,
    "customerId": 2,
    "accountType": "Checking",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  }
  ```
  ```json
  {
    "accountNumber": 22,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  }
  ```

- **Client 3 :**
  ```json
  {
    "accountNumber": 3,
    "customerId": 3,
    "accountType": "Checking",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  }
  ```
  ```json
  {
    "accountNumber": 13,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  }
  ```
  ```json
  {
    "accountNumber": 23,
    "customerId": 3,
    "accountType": "Checking",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  }
  ```

- **Client 4 :**
  ```json
  {
    "accountNumber": 4,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  }
  ```
  ```json
  {
    "accountNumber": 14,
    "customerId": 4,
    "accountType": "Checking",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  }
  ```
  ```json
  {
    "accountNumber": 24,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  }
  ```

---

### 3️⃣ Modifications des Comptes via HTTP (PUT) ✏️

Après avoir créé les comptes pour les clients, vous pouvez modifier les détails des comptes, tels que les adresses et le type de compte, en utilisant des requêtes PUT.

| **Client** | **Compte** | **Type de Compte** | **Ancienne Adresse** | **Nouvelle Adresse** | **Date de Création** |
|------------|------------|--------------------|----------------------|----------------------|----------------------|
| Client 1   | Compte 1    | Checking           | 123 Main St          | 321 Broadway          | 2023-02-01           |
| Client 1   | Compte 11   | Savings            | 123 Main St          | 321 Broadway          | 2023-02-01           |
| Client 1   | Compte 21   | Checking           | 123 Main St          | 321 Broadway          | 2023-02-01           |
| Client 2   | Compte 2    | Savings            | 456 Main St          | 789 Maple Ave         | 2023-02-02           |
| Client 2   | Compte 12   | Checking           | 456 Main St          | 789 Maple Ave         | 2023-02-02           |
| Client 2   | Compte 22   | Savings            | 456 Main St          | 789 Maple Ave         | 2023-02-02           |
| Client 3   | Compte 3    | Checking           | 789 Elm St           | 456 Oak St            | 2023-02-03           |
| Client 3   | Compte 13   | Savings            | 789 Elm St           | 456 Oak St            | 2023-02-03           |
| Client 3   | Compte 23   | Checking           | 789 Elm St           | 456 Oak St            | 2023-02-03           |
| Client 4   | Compte 4    | Savings            | 101 Pine St          | 987 Birch Rd          | 2023-02-04           |
| Client 4   | Compte 14   | Checking           | 101 Pine St          | 987 Birch Rd          | 2023-02-04           |
| Client 4   | Compte 24   | Savings            | 101 Pine St          | 987 Birch Rd          | 2023-02-04           |

#### 3.1 **Modifier un compte pour un client via Postman**

Exemple pour modifier le compte pour le **Client 1** :
- Ouvrez Postman.
- Choisissez `PUT`.
- URL : `http://localhost:8080/update/1`.
- Body -> raw -> JSON :
```json
{
  "accountNumber": 1,
  "customerId": 1,
  "accountType": "Savings",
  "branchAddress": "321 Broadway",
  "createDt": "2023-02-01"
}
```

#### 3.2 **Vérifier la modification du compte**

- Ouvrir le navigateur et tester cette URL : `http://localhost:8080/accounts`.
- Ou utilisez Postman pour effectuer un GET sur `http://localhost:8080/accounts`.

#### 3.3 **Répéter l'opération pour les autres comptes**

Voici les JSON pour les autres comptes :

- **Client 2 :**
  ```json
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Current",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```
  ```json
  {
    "accountNumber": 12,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```
  ```json
  {
    "accountNumber": 22,
    "customerId": 2,
    "accountType": "Current",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```

- **Client 3 :**
  ```json
  {
    "accountNumber": 3,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```
  ```json
  {
    "accountNumber": 13,
    "customerId": 3,
    "accountType": "Current",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```
  ```json
  {
    "accountNumber": 23,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```

- **Client 4 :**
  ```json
  {
    "accountNumber": 4,
    "customerId": 4,
    "accountType": "Current",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```
  ```json
  {
    "accountNumber": 14,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```
  ```json
  {
    "accountNumber": 24,
    "customerId": 4,
    "accountType": "Current",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```

---

### 4️⃣ Suppression des Comptes via HTTP (DELETE) 🚮

Après avoir créé et modifié les comptes pour les clients, il peut être nécessaire de les supprimer individuellement. Cette section vous guide à travers le processus de suppression de chaque compte un par un en utilisant des requêtes HTTP DELETE.

| **Client** | **Compte** | **Type de Compte** | **Adresse**  | **Date de Création** |
|------------|------------|--------------------|--------------|----------------------|
| Client 1   | Compte 1    | Savings            | 321 Broadway | 2023-02-01           |
| Client 1   | Compte 11   | Current            | 321 Broadway | 2023-02-01           |
| Client 1   | Compte 21   | Savings            | 321 Broadway | 2023-02-01           |
| Client 2   | Compte 2    | Current            | 789 Maple Ave | 2023-02-02          |
| Client 2   | Compte 12   | Savings            | 789 Maple Ave | 2023-02-02          |
| Client 2   | Compte 22   | Current            | 789 Maple Ave | 2023-02-02          |
| Client 3   | Compte 3    | Savings            | 456 Oak St    | 2023-02-03           |
| Client 3   | Compte 13   | Current            | 456 Oak St    | 2023-02-03           |
| Client 3   | Compte 23   | Savings            | 456 Oak St    | 2023-02-03           |
| Client 4   | Compte 4    | Current            | 987 Birch Rd  | 2023-02-04           |
| Client 4   | Compte 14   | Savings            | 987 Birch Rd  | 2023-02-04           |
| Client 4   | Compte 24   | Current            | 987 Birch Rd  | 2023-02-04           |

#### 4.1 **Suppression d'un compte pour un client via Postman**

Exemple pour supprimer le compte pour le **Client 1** :
- Ouvrez Postman.
- Choisissez `DELETE`.
- URL : `http://localhost:8080/deleteAccount/1`.

#### 4.2 **Vérifier la suppression du compte**

- Ouvrir le navigateur et tester cette URL : `http://localhost:8080/accounts`.
- Ou utilisez Postman pour effectuer un GET sur `http://localhost:8080/accounts`.

#### 4.3 **Répéter l'opération pour les autres comptes**

Voici les URLs correspondantes pour chaque compte à supprimer :

- **Client 1 :**
  - Supprimer Compte 1 : `http://localhost:8080/deleteAccount/1`
  - Supprimer Compte 11 : `http://localhost:8080/deleteAccount/11`
  - Supprimer Compte 21 : `http://localhost:8080/deleteAccount/21`

- **Client 2 :**
  - Supprimer Compte 2 : `http://localhost:8080/deleteAccount/2`
  - Supprimer Compte 12 : `http://localhost:8080/deleteAccount/12`
  - Supprimer Compte 22 : `http://localhost:8080/deleteAccount/22`

- **Client 3 :**
  - Supprimer Compte 3 : `http://localhost:8080/deleteAccount/3`
  - Supprimer Compte 13 : `http://localhost:8080/deleteAccount/13`
  - Supprimer Compte 23 : `http://localhost:8080/deleteAccount/23`

- **Client 4 :**
  - Supprimer Compte 4 : `http://localhost:8080/deleteAccount/4`
  - Supprimer Compte 14 : `http://localhost:8080/deleteAccount/14`
  - Supprimer Compte 24 : `http://localhost:8080/deleteAccount/24`

---

## 🛠️ Test et Vérification

### 1️⃣ Vérification via GET
- **Vérifiez la suppression via l'URL `http://localhost:8080/accounts` ou via POSTMAN GET `http://localhost:8080/accounts`**.

### 2️⃣ Continuer à supprimer et tester
- **Répétez les opérations DELETE pour chaque compte jusqu'à ce que tous soient supprimés**.

---

## 🎓 Prochains Défis

### 1️⃣ Documentation via Swagger
- Implémentez et testez la documentation de votre API avec Swagger.

### 2️⃣ Compréhension de la Structure MVC
- Approfondissez la compréhension de la structure `controller -> services -> repository -> BD`.

### 3️⃣ Gestion de l'Auto-Incrémentation de AccountID
- Explorez l'implémentation de l'auto-incrémentation pour les `accountId`.

### 4️⃣ Insertion en Lots (Batch Processing)
- Implémentez l'insertion de comptes en masse via des opérations batch.

---

## ✍️ Évaluation Formative

### 1️⃣ Insertion Multiple en Lots
- **Objectif** : Créer 12 comptes via POST.
- **URL** : `http://localhost:8080/newAccounts`
- **Body** : Passez une liste d'objets JSON représentant les comptes à créer.

### 2️⃣ Suppression en Masse
- **Objectif** : Implémenter la suppression de tous les comptes d'un seul coup.
- **URL** : `http://localhost:8080/deleteAllAccounts`
- **Méthode** : DELETE (pas de body requis).

### 3️⃣ Mise à Jour Multiple
- **Objectif** : Mettre à jour plusieurs comptes en une seule opération.
- **URL** : `http://localhost:8080/updateAccounts`
- **Body** : Liste d'objets JSON représentant les comptes à mettre à jour.

### 4️⃣ Ajout de Validation Personnalisée
- **Objectif** : Ajouter une validation pour s'assurer que tous les comptes créés en lot appartiennent au même client.

### 5️⃣ Recherche en Masse
- **Objectif** : Ajouter la fonctionnalité de recherche de comptes en passant une liste d'IDs.

---



# 📄 Annexe : Explication des Annotations de Mapping dans le Contrôleur Spring Boot

| **Annotation**                  | **Méthode HTTP** | **URL**                    | **Description**                                                                                                                                         | **Exemple d'Utilisation**                                              |
|---------------------------------|------------------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| `@DeleteMapping("/deleteAccount/{id}")` | DELETE           | `/deleteAccount/{id}`        | Cette annotation est utilisée pour supprimer un compte spécifique en utilisant son identifiant (`id`). Le `id` est passé en tant que paramètre de l'URL. | Supprimer un compte : `DELETE /deleteAccount/1`                        |
| `@PutMapping("/update/{id}")`      | PUT              | `/update/{id}`               | Cette annotation permet de mettre à jour les détails d'un compte spécifique. Le `id` du compte à mettre à jour est passé en paramètre dans l'URL.        | Mettre à jour un compte : `PUT /update/1`                              |
| `@PostMapping("/newAccount")`      | POST             | `/newAccount`                | Cette annotation est utilisée pour créer un nouveau compte. Les détails du compte sont passés dans le corps de la requête en format JSON.                | Créer un nouveau compte : `POST /newAccount`                           |
| `@GetMapping("/accounts")`         | GET              | `/accounts`                  | Cette annotation permet de récupérer la liste de tous les comptes disponibles.                                                                            | Récupérer tous les comptes : `GET /accounts`                           |
| `@GetMapping("/myAccount/{id}")`   | GET              | `/myAccount/{id}`            | Cette annotation permet de récupérer les détails d'un compte spécifique en utilisant son identifiant (`id`). Le `id` est passé en tant que paramètre de l'URL. | Récupérer un compte spécifique : `GET /myAccount/1`                    |

---

### 🔍 Détails des Annotations :

1. **@DeleteMapping** : Utilisée pour la suppression des ressources.
   - **Exemple** : `@DeleteMapping("/deleteAccount/{id}")`
   - **Description** : Supprime un compte en fonction de l'ID fourni dans l'URL.

2. **@PutMapping** : Utilisée pour mettre à jour une ressource existante.
   - **Exemple** : `@PutMapping("/update/{id}")`
   - **Description** : Met à jour les informations d'un compte existant en fonction de l'ID.

3. **@PostMapping** : Utilisée pour la création d'une nouvelle ressource.
   - **Exemple** : `@PostMapping("/newAccount")`
   - **Description** : Crée un nouveau compte avec les détails fournis dans le corps de la requête.

4. **@GetMapping** : Utilisée pour récupérer des ressources.
   - **Exemple** : `@GetMapping("/accounts")`
   - **Description** : Récupère la liste de tous les comptes disponibles.

   - **Exemple** : `@GetMapping("/myAccount/{id}")`
   - **Description** : Récupère les détails d'un compte spécifique en fonction de l'ID fourni dans l'URL.

---

### 💡 Remarque :
- Les annotations `@DeleteMapping`, `@PutMapping`, `@PostMapping`, et `@GetMapping` sont des raccourcis fournis par Spring Boot pour gérer les requêtes HTTP.
- Chaque annotation correspond à une méthode HTTP spécifique (DELETE, PUT, POST, GET), utilisée pour interagir avec les ressources (ici, les comptes) sur le serveur.


