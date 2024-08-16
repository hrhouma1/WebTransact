# 🏁 Partie 1 : Création en Lot des Comptes Bancaires

Dans cette partie, nous allons aborder l'insertion multiple de comptes pour différents clients via des requêtes POST en une seule opération. Cette approche vous permet de gérer efficacement les données tout en minimisant les risques d'erreurs.

## 🚀 Étapes à suivre :

### 1️⃣ Objectif : Insertion Multiple en Lots

Nous allons créer 12 comptes via une requête POST pour les clients existants, selon la répartition suivante :
- **Client 1** : comptes 1, 11, 21
- **Client 2** : comptes 2, 12, 22
- **Client 3** : comptes 3, 13, 23
- **Client 4** : comptes 4, 14, 24

### 2️⃣ Préparation de la Requête POST

#### 2.1 **URL de l'API**
```plaintext
POST http://localhost:8080/newAccounts
```

#### 2.2 **Corps de la Requête (Body)**
Préparez un corps JSON pour inclure les informations sur chaque compte à créer :

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

## 🛠️ Implémentation de l'Insertion Multiple

### 1️⃣ Modification du `AccountsController` pour gérer l'insertion en lot

Ajoutez une méthode dans `AccountsController` pour accepter une liste d'objets `Accounts` et les enregistrer via le service approprié.

```java
@PostMapping("/newAccounts")
public List<String> newAccounts(@RequestBody List<Accounts> accountsList) {
    return accountsService.saveAll(accountsList);
}
```

### 2️⃣ Implémentation du service dans `AccountsService`

Dans `AccountsService`, ajoutez une méthode pour enregistrer tous les comptes fournis. Cette méthode assure l'intégrité des données en utilisant une transaction.

```java
@Transactional
public List<String> saveAll(List<Accounts> accountsList) {
    List<String> responseList = new ArrayList<>();
    for (Accounts account : accountsList) {
        try {
            accountsRepository.save(account);
            responseList.add("Compte enregistré avec succès : " + account.getAccountNumber());
        } catch (Exception e) {
            responseList.add("Échec d'enregistrement pour le compte : " + account.getAccountNumber() + " - Erreur : " + e.getMessage());
        }
    }
    return responseList;
}
```

> **💡 Remarque :** L'utilisation de l'annotation `@Transactional` permet de garantir que toutes les opérations sont atomiques. En cas d'erreur, toutes les insertions sont annulées.

---

## 🏃‍♂️ Test et Vérification

### 1️⃣ Utiliser Postman pour tester l'insertion en lot

- **URL** : `http://localhost:8080/newAccounts`
- **Méthode** : POST
- **Body** : Copiez le JSON précédemment préparé.

### 2️⃣ Vérification dans la base de données

Après l'insertion, vérifiez que les comptes ont bien été créés en exécutant la commande suivante dans PostgreSQL :

```sql
SELECT * FROM public.accounts WHERE customer_id IN (1, 2, 3, 4);
```

---

# 🏁 Partie 2 : Suppression en Masse des Comptes

Dans cette partie, nous allons implémenter une fonctionnalité permettant de supprimer tous les comptes bancaires en une seule opération.

## 🚀 Étapes à suivre :

### 1️⃣ Objectif : Suppression en Masse

Ajouter une méthode dans `AccountsController` pour supprimer tous les comptes enregistrés.

### 2️⃣ Implémentation

#### 2.1 **Modification du `AccountsController`**

Ajoutez une méthode `DELETE` pour supprimer tous les comptes via le service approprié.

```java
@DeleteMapping("/deleteAllAccounts")
public String deleteAllAccounts() {
    return accountsService.deleteAllAccounts();
}
```

#### 2.2 **Modification du `AccountsService`**

Dans `AccountsService`, ajoutez une méthode pour supprimer tous les comptes et gérer les erreurs éventuelles.

```java
public String deleteAllAccounts() {
    try {
        accountsRepository.deleteAll();
        return "Tous les comptes ont été supprimés avec succès";
    } catch (Exception e) {
        return "Erreur lors de la suppression des comptes : " + e.getMessage();
    }
}
```

> **💡 Remarque :** Cette méthode supprime tous les comptes de la base de données. Assurez-vous d'avoir une copie de sauvegarde avant d'exécuter cette opération en environnement de production.

---

## 🏃‍♂️ Test et Vérification

### 1️⃣ Utiliser Postman pour tester la suppression en masse

- **URL** : `http://localhost:8080/deleteAllAccounts`
- **Méthode** : DELETE

### 2️⃣ Vérification dans la base de données

Après la suppression, vérifiez que les comptes ont bien été supprimés en exécutant la commande suivante dans PostgreSQL :

```sql
SELECT * FROM public.accounts;
```

---

# 🏁 Partie 3 : Exercice de Validation Avancée

## 🚀 Exercices à Compléter

### 1️⃣ Suppression en Lot des Comptes
- **Objectif** : Implémentez la suppression de plusieurs comptes à la fois en fournissant une liste d'identifiants.
- **URL** : `DELETE http://localhost:8080/deleteAccounts`
- **Body** : `[1, 2, 3, 4]` // Liste des identifiants de comptes à supprimer.

### 2️⃣ Mise à Jour Multiple
- **Objectif** : Mettre à jour plusieurs comptes en une seule opération.
- **URL** : `PUT http://localhost:8080/updateAccounts`
- **Body** : Liste d'objets JSON représentant les comptes à mettre à jour.

### 3️⃣ Ajout de Validation Personnalisée
- **Objectif** : Ajouter une validation pour s'assurer que tous les comptes créés en lot appartiennent au même client.

### 4️⃣ Recherche en Masse
- **Objectif** : Ajouter la fonctionnalité de recherche de comptes en passant une liste d'IDs.
- **URL** : `GET http://localhost:8080/findAccounts`
- **Body** : `[1, 2, 3, 4]` // Liste des identifiants de comptes à rechercher.

---

# Annexe : 


### 🏁 Partie 3 : Exercice de Validation Avancée

Dans cette partie, vous allez mettre en pratique plusieurs concepts avancés de manipulation de données en lot, en intégrant des opérations de suppression, de mise à jour, de validation personnalisée, et de recherche en masse dans une application Spring Boot. Ces exercices vous permettront de maîtriser la gestion des opérations complexes tout en garantissant l'intégrité des données.

---

## 🚀 Exercices à Compléter

### 1️⃣ Suppression en Lot des Comptes 🚮

**Objectif** : Implémentez la suppression de plusieurs comptes à la fois en fournissant une liste d'identifiants.

#### 1.1 **Modification du `AccountsController` pour la suppression en lot**

Ajoutez une méthode dans `AccountsController` pour accepter une liste d'identifiants de comptes à supprimer.

```java
@DeleteMapping("/deleteAccounts")
public String deleteAccounts(@RequestBody List<Long> accountIds) {
    return accountsService.deleteAllByIds(accountIds);
}
```

#### 1.2 **Implémentation de la méthode dans `AccountsService`**

Ajoutez une méthode dans `AccountsService` pour supprimer tous les comptes correspondant aux identifiants fournis.

```java
@Transactional
public String deleteAllByIds(List<Long> accountIds) {
    try {
        accountsRepository.deleteAllById(accountIds);
        return "Comptes supprimés avec succès";
    } catch (Exception e) {
        return "Erreur lors de la suppression des comptes : " + e.getMessage();
    }
}
```

> **💡 Remarque :** L'utilisation de l'annotation `@Transactional` permet d'assurer que toutes les suppressions se déroulent correctement. Si une suppression échoue, aucune des suppressions ne sera appliquée, maintenant ainsi l'intégrité des données.

#### 1.3 **Tester la suppression en lot**

- **URL** : `DELETE http://localhost:8080/deleteAccounts`
- **Méthode** : DELETE
- **Body** : `[1, 2, 3, 4]`  // Remplacez les identifiants par ceux des comptes que vous souhaitez supprimer.

Après l'envoi de la requête, vérifiez dans la base de données que les comptes spécifiés ont bien été supprimés.

---

### 2️⃣ Mise à Jour Multiple ✏️

**Objectif** : Mettre à jour plusieurs comptes en une seule opération, en fournissant une liste d'objets comptes avec les nouvelles informations.

#### 2.1 **Modification du `AccountsController` pour la mise à jour multiple**

Ajoutez une méthode dans `AccountsController` pour accepter une liste d'objets comptes à mettre à jour.

```java
@PutMapping("/updateAccounts")
public String updateAccounts(@RequestBody List<Accounts> accountsList) {
    return accountsService.updateAccounts(accountsList);
}
```

#### 2.2 **Implémentation de la méthode dans `AccountsService`**

Ajoutez une méthode dans `AccountsService` pour mettre à jour les comptes dans la base de données.

```java
@Transactional
public String updateAccounts(List<Accounts> accountsList) {
    try {
        accountsList.forEach(account -> accountsRepository.save(account));
        return "Comptes mis à jour avec succès";
    } catch (Exception e) {
        return "Erreur lors de la mise à jour des comptes : " + e.getMessage();
    }
}
```

> **💡 Remarque :** Chaque compte est mis à jour indépendamment, mais toutes les mises à jour sont regroupées dans une seule transaction pour assurer la cohérence des données.

#### 2.3 **Tester la mise à jour multiple**

- **URL** : `PUT http://localhost:8080/updateAccounts`
- **Méthode** : PUT
- **Body** : Voici un exemple de corps JSON pour mettre à jour plusieurs comptes :

```json
[
  {
    "accountNumber": 1,
    "customerId": 1,
    "accountType": "Savings",
    "branchAddress": "456 Oak St",
    "createDt": "2023-02-01"
  },
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Checking",
    "branchAddress": "789 Elm St",
    "createDt": "2023-03-01"
  }
]
```

Après l'envoi de la requête, vérifiez que les comptes ont bien été mis à jour dans la base de données.

---

### 3️⃣ Ajout de Validation Personnalisée ✔️

**Objectif** : Ajouter une validation pour s'assurer que tous les comptes créés en lot appartiennent au même client.

#### 3.1 **Modification du `AccountsService` pour ajouter la validation**

Ajoutez une validation dans la méthode `saveAll` pour vérifier que tous les comptes appartiennent au même client avant de les enregistrer.

```java
public String saveAll(List<Accounts> accountsList) {
    if (!accountsList.stream().allMatch(a -> a.getCustomerId().equals(accountsList.get(0).getCustomerId()))) {
        return "Tous les comptes doivent appartenir au même client";
    }
    // Reste de la méthode d'enregistrement...
}
```

> **💡 Remarque :** Cette validation garantit l'intégrité logique des données en s'assurant que tous les comptes d'une opération en lot sont liés au même client.

#### 3.2 **Tester la validation**

Tentez d'insérer des comptes avec des `customerId` différents dans la même requête POST. Vous devriez recevoir un message d'erreur indiquant que tous les comptes doivent appartenir au même client.

---

### 4️⃣ Recherche en Masse 🔍

**Objectif** : Ajouter la fonctionnalité de recherche de comptes en passant une liste d'IDs.

#### 4.1 **Modification du `AccountsController` pour la recherche en masse**

Ajoutez une méthode dans `AccountsController` pour accepter une liste d'identifiants de comptes et renvoyer les comptes correspondants.

```java
@GetMapping("/findAccounts")
public List<Accounts> findAccounts(@RequestBody List<Long> accountIds) {
    return accountsService.findAllByIds(accountIds);
}
```

#### 4.2 **Implémentation de la méthode dans `AccountsService`**

Ajoutez une méthode dans `AccountsService` pour rechercher tous les comptes correspondant aux identifiants fournis.

```java
public List<Accounts> findAllByIds(List<Long> accountIds) {
    return accountsRepository.findAllById(accountIds);
}
```

#### 4.3 **Tester la recherche en masse**

- **URL** : `GET http://localhost:8080/findAccounts`
- **Méthode** : POST
- **Body** : `[1, 2, 3, 4]`  // Remplacez les identifiants par ceux des comptes que vous souhaitez rechercher.

Vérifiez que les comptes correspondants aux identifiants fournis sont bien retournés.

---

## 🏃‍♂️ Test et Vérification

Pour chaque exercice, il est essentiel de tester soigneusement vos implémentations en utilisant un outil comme Postman et en vérifiant les résultats directement dans la base de données.

