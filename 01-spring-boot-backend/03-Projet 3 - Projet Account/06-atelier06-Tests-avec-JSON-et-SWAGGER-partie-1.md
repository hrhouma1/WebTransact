# 🏁 Partie 06 : Tests avec JSON et SWAGGER - partie 1

Dans cette section, vous allez tester l'application Spring Boot en utilisant des requêtes HTTP pour gérer les comptes associés aux clients. Vous utiliserez Swagger pour envoyer des requêtes POST, GET, PUT, et DELETE.

### Étapes avec Swagger :

1. **Accédez à l'interface Swagger** :
   - Ouvrez votre navigateur et accédez à l'URL de votre application : `http://localhost:8080/swagger-ui.html`.

2. **Suppression de tous les comptes** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `DELETE /deleteAllAccounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez ensuite sur le bouton **`Try it out`** et enfin sur **`Execute`** pour envoyer la requête de suppression de tous les comptes.

3. **Vérification de la suppression de tous les comptes** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`**. La réponse devrait être vide si tous les comptes ont bien été supprimés.

4. **Vérification de tous les clients** :
   - **Section** : `customers-controller`
   - **Endpoint** : `GET /customers`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour voir la liste des clients existants.

---

# 1️⃣ Insertion des Comptes via HTTP (POST) ➕

Après avoir supprimé tous les comptes, vous pouvez commencer à créer de nouveaux comptes associés via des requêtes POST.

- **Section** : `accounts-controller`
- **Endpoint** : `POST /newAccount`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`**. Dans la section **Body**, choisissez `application/json` et collez le JSON correspondant pour créer un compte. Cliquez sur **`Execute`** pour envoyer la requête.

Voici les JSON à copier-coller pour créer les comptes :

- **Client 1 :**
  ```json
  {
    "accountNumber": 1,
    "customerId": 1,
    "accountType": "Checking",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  }
  ```
  ```json
  {
    "accountNumber": 11,
    "customerId": 1,
    "accountType": "Savings",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  }
  ```
  ```json
  {
    "accountNumber": 21,
    "customerId": 1,
    "accountType": "Checking",
    "branchAddress": "123 Main St",
    "createDt": "2023-01-02"
  }
  ```

---
# Vérification: 
---

 **Vérification de l'ajout de tous les comptes du client #1** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`**. La réponse devrait être vide si tous les comptes ont bien été supprimés.


---
- **Client 2 :**
---

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

---
# Vérification: 
---

 **Vérification de l'ajout de tous les comptes du client #2** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`**. La réponse devrait être vide si tous les comptes ont bien été supprimés.




---
- **Client 3 :**
---


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


---
# Vérification: 
---

 **Vérification de l'ajout de tous les comptes du client #3** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`**. La réponse devrait être vide si tous les comptes ont bien été supprimés.


  

---
- **Client 4 :**
---

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
# Vérification: 
---

 **Vérification de l'ajout de tous les comptes du client #4 et tous les clients** :
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`**. La réponse devrait être vide si tous les comptes ont bien été supprimés.



---


# 2️⃣ Modifications des Comptes via HTTP (PUT) ✏️

---

Après avoir créé les comptes, vous pouvez modifier les détails de ces comptes en utilisant des requêtes PUT.

- **Section** : `accounts-controller`
- **Endpoint** : `PUT /update/{id}`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`**. Dans la section **Body**, choisissez `application/json` et collez le JSON correspondant pour modifier un compte. Cliquez sur **`Execute`** pour envoyer la requête.

---

#### **Client 1 :**

2.1. Allez à : **Endpoint** : `GET /myAccount/1`  
2.2. Vérifiez le paramètre ==> `"accountType": "Checking"`  
2.3. Modifiez le compte avec : **Endpoint** : `PUT /update/1`

Voici le JSON à copier-coller pour modifier le compte 1 :

  ```json
  {
    "accountNumber": 1,
    "customerId": 1,
    "accountType": "Savings",
    "branchAddress": "321 Broadway",
    "createDt": "2023-02-01"
  }
  ```

2.4. Allez à : **Endpoint** : `GET /myAccount/1`  
2.5. Vérifiez le paramètre ==> `"accountType": "Savings"`

---

2.6. Allez à : **Endpoint** : `GET /myAccount/11`  
2.7. Vérifiez le paramètre ==> `"accountType": ".........."`  
2.8. Modifiez le compte avec : **Endpoint** : `PUT /update/11`

Voici le JSON à copier-coller pour modifier le compte 11 :

  ```json
  {
    "accountNumber": 11,
    "customerId": 1,
    "accountType": "Current",
    "branchAddress": "321 Broadway",
    "createDt": "2023-02-01"
  }
  ```

2.9. Allez à : **Endpoint** : `GET /myAccount/11`  
2.10. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.11. Allez à : **Endpoint** : `GET /myAccount/21`  
2.12. Vérifiez le paramètre ==> `"accountType": ".........."`    
2.13. Modifiez le compte avec : **Endpoint** : `PUT /update/21`

Voici le JSON à copier-coller pour modifier le compte 21 :

  ```json
  {
    "accountNumber": 21,
    "customerId": 1,
    "accountType": "Savings",
    "branchAddress": "321 Broadway",
    "createDt": "2023-02-01"
  }
  ```

2.14. Allez à : **Endpoint** : `GET /myAccount/21`  
2.15. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

#### **Client 2 :**

2.16. Allez à : **Endpoint** : `GET /myAccount/2`  
2.17. Vérifiez le paramètre ==> `"accountType": "........."`  
2.18. Modifiez le compte avec : **Endpoint** : `PUT /update/2`

Voici le JSON à copier-coller pour modifier le compte 2 :

  ```json
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Current",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```

2.19. Allez à : **Endpoint** : `GET /myAccount/2`  
2.20. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.21. Allez à : **Endpoint** : `GET /myAccount/12`  
2.22. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.23. Modifiez le compte avec : **Endpoint** : `PUT /update/12`

Voici le JSON à copier-coller pour modifier le compte 12 :

  ```json
  {
    "accountNumber": 12,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```

2.24. Allez à : **Endpoint** : `GET /myAccount/12`  
2.25. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.26. Allez à : **Endpoint** : `GET /myAccount/22`  
2.27. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.28. Modifiez le compte avec : **Endpoint** : `PUT /update/22`

Voici le JSON à copier-coller pour modifier le compte 22 :

  ```json
  {
    "accountNumber": 22,
    "customerId": 2,
    "accountType": "Current",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```

2.29. Allez à : **Endpoint** : `GET /myAccount/22`  
2.30. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

#### **Client 3 :**

2.31. Allez à : **Endpoint** : `GET /myAccount/3`  
2.32. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.33. Modifiez le compte avec : **Endpoint** : `PUT /update/3`

Voici le JSON à copier-coller pour modifier le compte 3 :

  ```json
  {
    "accountNumber": 3,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```

2.34. Allez à : **Endpoint** : `GET /myAccount/3`  
2.35. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.36. Allez à : **Endpoint** : `GET /myAccount/13`  
2.37. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.38. Modifiez le compte avec : **Endpoint** : `PUT /update/13`

Voici le JSON à copier-coller pour modifier le compte 13 :

  ```json
  {
    "accountNumber": 13,
    "customerId": 3,
    "accountType": "Current",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```

2.39. Allez à : **Endpoint** : `GET /myAccount/13`  
2.40. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.41. Allez à : **Endpoint** : `GET /myAccount/23`  
2.42. Vérifiez le paramètre ==> `"accountType": ".........."`  
2.43. Modifiez le compte avec : **Endpoint** : `PUT /update/23`

Voici le JSON à copier-coller pour modifier le compte 23 :

  ```json
  {
    "accountNumber": 23,
    "customerId": 3,
    "accountType": "Savings",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-03"
  }
  ```

2.44. Allez à : **Endpoint** : `GET /myAccount/23`  
2.45. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

#### **Client 4 :**

2.46. Allez à : **Endpoint** : `GET /myAccount/4`  
2.47. Vérifiez le paramètre ==> `"accountType": ".........."`  
2.48. Modifiez le compte avec : **Endpoint** : `PUT /update/4`

Voici le JSON à copier-coller pour modifier le compte 4 :

  ```json
  {
    "accountNumber": 4,
    "customerId": 4,
    "accountType": "Current",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```

2.49. Allez à : **Endpoint** : `GET /myAccount/4`  
2.50. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.51. Allez à : **Endpoint** : `GET /myAccount/14`  
2.52. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.53. Modifiez le compte avec : **Endpoint** : `PUT /update/14`

Voici le JSON à copier-coller pour modifier le compte 14 :

  ```json
  {
    "accountNumber": 14,
    "customerId": 4,
    "accountType": "Savings",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```

2.54. Allez à : **Endpoint** : `GET /myAccount/14`  
2.55. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

2.56. Allez à : **Endpoint** : `GET /myAccount/24`

  
2.57. Vérifiez le paramètre ==> `"accountType": ".........."`   
2.58. Modifiez le compte avec : **Endpoint** : `PUT /update/24`

Voici le JSON à copier-coller pour modifier le compte 24 :

  ```json
  {
    "accountNumber": 24,
    "customerId": 4,
    "accountType": "Current",
    "branchAddress": "987 Birch Rd",
    "createDt": "2023-02-04"
  }
  ```

2.59. Allez à : **Endpoint** : `GET /myAccount/24`  
2.60. Vérifiez le paramètre ==> `"accountType": ".........."`  

---

# 3️⃣ Suppression des Comptes via HTTP (DELETE) 🚮

Enfin, vous pouvez supprimer les comptes en utilisant des requêtes DELETE.

- **Section** : `accounts-controller`
- **Endpoint** : `DELETE /deleteAccount/{id}`
- **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`**. Dans la section **Parameters**, entrez l'ID du compte à supprimer (par exemple, `1` pour le compte avec accountNumber 1). Cliquez sur **`Execute`** pour envoyer la requête.

Je vous propose les étapes pour chaque compte à supprimer, incluant les vérifications avant et après la suppression :

---

### **Client 1 :**

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/1`
  - Vérifiez que le compte avec l'`accountNumber` 1 est disponible.

- **Suppression** :
  - Supprimer Compte 1 : `http://localhost:8080/deleteAccount/1`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/1`
  - Vérifiez que le compte avec l'`accountNumber` 1 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/11`
  - Vérifiez que le compte avec l'`accountNumber` 11 est disponible.

- **Suppression** :
  - Supprimer Compte 11 : `http://localhost:8080/deleteAccount/11`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/11`
  - Vérifiez que le compte avec l'`accountNumber` 11 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/21`
  - Vérifiez que le compte avec l'`accountNumber` 21 est disponible.

- **Suppression** :
  - Supprimer Compte 21 : `http://localhost:8080/deleteAccount/21`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/21`
  - Vérifiez que le compte avec l'`accountNumber` 21 n'est plus disponible.

---

### **Client 2 :**

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/2`
  - Vérifiez que le compte avec l'`accountNumber` 2 est disponible.

- **Suppression** :
  - Supprimer Compte 2 : `http://localhost:8080/deleteAccount/2`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/2`
  - Vérifiez que le compte avec l'`accountNumber` 2 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/12`
  - Vérifiez que le compte avec l'`accountNumber` 12 est disponible.

- **Suppression** :
  - Supprimer Compte 12 : `http://localhost:8080/deleteAccount/12`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/12`
  - Vérifiez que le compte avec l'`accountNumber` 12 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/22`
  - Vérifiez que le compte avec l'`accountNumber` 22 est disponible.

- **Suppression** :
  - Supprimer Compte 22 : `http://localhost:8080/deleteAccount/22`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/22`
  - Vérifiez que le compte avec l'`accountNumber` 22 n'est plus disponible.

---

### **Client 3 :**

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/3`
  - Vérifiez que le compte avec l'`accountNumber` 3 est disponible.

- **Suppression** :
  - Supprimer Compte 3 : `http://localhost:8080/deleteAccount/3`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/3`
  - Vérifiez que le compte avec l'`accountNumber` 3 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/13`
  - Vérifiez que le compte avec l'`accountNumber` 13 est disponible.

- **Suppression** :
  - Supprimer Compte 13 : `http://localhost:8080/deleteAccount/13`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/13`
  - Vérifiez que le compte avec l'`accountNumber` 13 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/23`
  - Vérifiez que le compte avec l'`accountNumber` 23 est disponible.

- **Suppression** :
  - Supprimer Compte 23 : `http://localhost:8080/deleteAccount/23`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/23`
  - Vérifiez que le compte avec l'`accountNumber` 23 n'est plus disponible.

---

### **Client 4 :**

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/4`
  - Vérifiez que le compte avec l'`accountNumber` 4 est disponible.

- **Suppression** :
  - Supprimer Compte 4 : `http://localhost:8080/deleteAccount/4`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/4`
  - Vérifiez que le compte avec l'`accountNumber` 4 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/14`
  - Vérifiez que le compte avec l'`accountNumber` 14 est disponible.

- **Suppression** :
  - Supprimer Compte 14 : `http://localhost:8080/deleteAccount/14`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/14`
  - Vérifiez que le compte avec l'`accountNumber` 14 n'est plus disponible.

---

- **Vérification avant suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/24`
  - Vérifiez que le compte avec l'`accountNumber` 24 est disponible.

- **Suppression** :
  - Supprimer Compte 24 : `http://localhost:8080/deleteAccount/24`

- **Vérification après suppression** :
  - Allez à : **Endpoint** : `GET /myAccount/24`
  - Vérifiez que le compte avec l'`accountNumber` 24 n'est plus disponible.



---
# Résumé de la suppression :
---

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

### 🛠️ Test et Vérification

1. **Vérification via GET**
   - **Section** : `accounts-controller`
   - **Endpoint** : `GET /accounts`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour vérifier si les comptes ont été ajoutés ou supprimés correctement.

2. **Vérification de tous les clients**
   - **Section** : `customers-controller`
   - **Endpoint** : `GET /customers`
   - **Action** : Cliquez sur cette opération pour l'ouvrir. Cliquez sur **`Try it out`** puis sur **`Execute`** pour voir la liste des clients et vérifier les associations avec les comptes.

3. **Continuez à tester les différentes fonctionnalités en fonction des opérations précédentes.**
