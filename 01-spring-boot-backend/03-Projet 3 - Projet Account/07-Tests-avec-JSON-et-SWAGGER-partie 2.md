# 🏁 Tests avec JSON et SWAGGER- partie 2

Dans cette section, vous allez tester l'application Spring Boot en utilisant des requêtes HTTP pour gérer les comptes associés aux clients. Vous utiliserez Swagger pour envoyer des requêtes POST, GET, PUT, et DELETE.

### Étapes avec Swagger :

1. **Accédez à l'interface Swagger** :
   - Ouvrez votre navigateur et accédez à l'URL de votre application : `http://localhost:8080/swagger-ui.html`.

---

# 1️⃣ Insertion des Comptes via HTTP (POST) ➕

Après avoir accédé à l'interface Swagger, vous pouvez commencer par créer de nouveaux comptes associés via des requêtes POST.

- **Section** : `accounts-controller`
- **Endpoint** : `POST /newAccounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`**. Dans la section **Body**, choisissez `application/json` et collez le JSON correspondant pour créer les comptes par lots. Cliquez sur **`Execute`** pour envoyer la requête.

### JSON pour l'insertion par lots :

```json
[
  {
    "accountNumber": 1,
    "customerId": 1,
    "accountType": "Checking",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  },
  {
    "accountNumber": 11,
    "customerId": 1,
    "accountType": "Savings",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  },
  {
    "accountNumber": 21,
    "customerId": 1,
    "accountType": "Checking",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  },
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  },
  {
    "accountNumber": 12,
    "customerId": 2,
    "accountType": "Checking",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  },
  {
    "accountNumber": 22,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  },
  {
    "accountNumber": 3,
    "customerId": 3,
    "accountType": "Checking",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  },
  {
    "accountNumber": 13,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  },
  {
    "accountNumber": 23,
    "customerId": 3,
    "accountType": "Checking",
    "branchAddress": "789 Elm St",
    "createDt": "2023-01-04"
  },
  {
    "accountNumber": 4,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  },
  {
    "accountNumber": 14,
    "customerId": 4,
    "accountType": "Checking",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  },
  {
    "accountNumber": 24,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "101 Pine St",
    "createDt": "2023-01-05"
  }
]
```

---

# Vérification:

---

**Vérification de l'ajout des comptes par lots** :
- **Section** : `accounts-controller`
- **Endpoint** : `GET /accounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour vérifier si les comptes ont bien été ajoutés.

---

# 2️⃣ Test des Nouvelles Méthodes 🧪

Avant de procéder à la suppression, vous pouvez tester les nouvelles méthodes introduites pour la gestion des comptes.

1. **Endpoint** : `POST /findAccounts`
   - **Action** : Envoyez une requête POST avec un body JSON contenant les `accountNumbers` à rechercher.

   Exemple de body JSON :
   ```json
   {
     "accountNumbers": [1, 2, 3]
   }
   ```

2. **Vérification** : 
   - **Section** : `accounts-controller`
   - **Endpoint** : `POST /findAccounts`
   - **Action** : Vérifiez que les comptes correspondants sont bien retournés dans la réponse.

---

# 3️⃣ Suppression des Comptes via HTTP (DELETE) 🚮

Enfin, vous pouvez supprimer les comptes en utilisant des requêtes DELETE.

- **Section** : `accounts-controller`
- **Endpoint** : `DELETE /deleteAccounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`**. Dans la section **Body**, choisissez `application/json` et collez le JSON correspondant pour supprimer les comptes par lots. Cliquez sur **`Execute`** pour envoyer la requête.

### JSON pour la suppression par lots :

```json
{
  "accountNumbers": [1, 11, 21, 2, 12, 22, 3, 13, 23, 4, 14, 24]
}
```

---

# Vérification:

---

**Vérification de la suppression des comptes par lots** :
- **Section** : `accounts-controller`
- **Endpoint** : `GET /accounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour vérifier si les comptes ont bien été supprimés.

---

# 4️⃣ Suppression Finale 🚨

Pour être sûr que tous les comptes sont supprimés, vous pouvez exécuter une suppression finale de tous les comptes.

- **Section** : `accounts-controller`
- **Endpoint** : `DELETE /deleteAllAccounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour supprimer tous les comptes restants, s'il y en a.

---

# Vérification Finale:

---

**Vérification après la suppression finale** :
- **Section** : `accounts-controller`
- **Endpoint** : `GET /accounts`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour vérifier que la liste des comptes est bien vide.

