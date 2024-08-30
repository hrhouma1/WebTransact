

----

# 🏁 Partie 4 : Manipulations CRUD des Comptes via Swagger

----


Dans cette partie, nous allons effectuer les opérations CRUD (Create, Read, Update, Delete) sur les comptes bancaires en utilisant l'interface Swagger que vous avez intégrée précédemment. Swagger simplifie les interactions avec votre API en vous permettant de tester chaque endpoint via une interface web.

---

## 🚀 Étapes à Suivre

# 1️⃣ Accéder à Swagger UI

Une fois votre application démarrée, ouvrez votre navigateur et accédez à Swagger UI pour interagir avec votre API :

- **URL Swagger UI** : [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
- **Alternative** : [http://localhost:8080/swagger-ui/](http://localhost:8080/swagger-ui/)

---

# 2️⃣ Effectuer les Opérations CRUD

#### 2.1 **Créer un Compte (Create - POST)**

1. **Accédez à l'endpoint** `/newAccount` dans Swagger UI.
2. **Cliquez sur 'Try it out'** pour activer l'édition du corps de la requête.
3. **Saisissez le JSON suivant** pour créer un nouveau compte :

   ```json
   {
     "accountNumber": 1,
     "customerId": 1,
     "accountType": "Checking",
     "branchAddress": "123 Main St",
     "createDt": "2023-01-02"
   }
   ```

4. **Cliquez sur 'Execute'** pour envoyer la requête et créer le compte.

#### 2.2 **Lire les Comptes (Read - GET)**

1. **Accédez à l'endpoint** `/accounts` dans Swagger UI.
2. **Cliquez sur 'Try it out'** et ensuite sur 'Execute' pour récupérer la liste de tous les comptes.

   - **Pour un compte spécifique** : Accédez à l'endpoint `/myAccount/{id}` et entrez l'identifiant du compte pour récupérer ses détails.

#### 2.3 **Mettre à Jour un Compte (Update - PUT)**

1. **Accédez à l'endpoint** `/update/{id}` dans Swagger UI.
2. **Entrez l'ID du compte** que vous souhaitez mettre à jour.
3. **Cliquez sur 'Try it out'** et entrez le JSON mis à jour, par exemple :

   ```json
   {
     "accountNumber": 1,
     "customerId": 1,
     "accountType": "Savings",
     "branchAddress": "321 Broadway",
     "createDt": "2023-02-01"
   }
   ```

4. **Cliquez sur 'Execute'** pour envoyer la requête de mise à jour.

#### 2.4 **Supprimer un Compte (Delete - DELETE)**

1. **Accédez à l'endpoint** `/deleteAccount/{id}` dans Swagger UI.
2. **Entrez l'ID du compte** que vous souhaitez supprimer.
3. **Cliquez sur 'Try it out'** puis sur 'Execute' pour supprimer le compte.

---

# 3️⃣ Exemples de JSON pour les Opérations

- **Créer un Compte** :
  ```json
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Savings",
    "branchAddress": "456 Main St",
    "createDt": "2023-01-03"
  }
  ```

- **Mettre à Jour un Compte** :
  ```json
  {
    "accountNumber": 2,
    "customerId": 2,
    "accountType": "Current",
    "branchAddress": "789 Maple Ave",
    "createDt": "2023-02-02"
  }
  ```

- **Supprimer un Compte** : Il suffit d'aller à l'interface *SWAGGER* et de spécifier l'ID du compte dans l'interface *SWAGGER*. Il faut aller dans `/deleteAccount/{id}`, choisir *try it out* et mettre 2 dans le champ *id*. 
- Alternative : utilisation de postman et spécifier par exemple `/deleteAccount/2`.

---

### 🛠️ Test et Vérification

Après avoir exécuté les opérations via Swagger UI, vous pouvez utiliser les endpoints GET pour vérifier les résultats. Par exemple, utilisez `/accounts` (*http://localhost:8080/accounts*) pour voir la liste des comptes après avoir effectué des insertions, mises à jour ou suppressions.

---

### 🎓 Prochains Défis

1. **Mise en Place de la Documentation via Swagger** : Vous avez déjà commencé à utiliser Swagger pour documenter et tester votre API. Continuez à explorer ses fonctionnalités pour améliorer la documentation.
2. **Opérations Avancées** : Testez des opérations plus complexes, telles que l'insertion en lot de plusieurs comptes ou la suppression de tous les comptes à la fois.
3. **Validation Personnalisée** : Implémentez des validations pour s'assurer que les données soumises répondent à certaines contraintes, comme l'exigence que tous les comptes d'un client soient du même type.

---

Avec Swagger, vous avez désormais un outil puissant pour interagir avec votre API de manière intuitive, tester vos endpoints et documenter automatiquement votre code. Cela rend votre développement plus rapide, plus sûr et plus transparent pour d'autres développeurs ou équipes.

--------
----------
--------
----
# Évaluation Formative - Aller plus loin
----

----

# Suppression de Tous les Comptes

----

1. **Accédez à l'interface Swagger** :
   - Ouvrez votre navigateur et allez sur [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html).

2. **Sélectionnez l'endpoint pour supprimer tous les comptes** :
   - Vous pouvez utiliser un endpoint personnalisé si vous l'avez implémenté, tel que `/deleteAllAccounts`, ou supprimer les comptes un par un si vous n'avez pas encore mis en place cette fonctionnalité.

3. **Suppression en Masse via Swagger (si disponible)** :
   - Accédez à l'endpoint `/deleteAllAccounts`.
   - Cliquez sur 'Try it out' puis sur 'Execute' pour supprimer tous les comptes en une seule fois.

4. **Vérification** :
   - Utilisez l'endpoint `/accounts` pour vérifier qu'il ne reste aucun compte dans la base de données.

# Suppression Individuelle de Comptes (Si suppression en masse non disponible)

1. **Listez tous les comptes** :
   - Accédez à l'endpoint `/accounts` dans Swagger UI.
   - Cliquez sur 'Try it out' puis 'Execute' pour voir tous les comptes existants.

2. **Supprimez chaque compte individuellement** :
   - Utilisez l'endpoint `/deleteAccount/{id}` en remplaçant `{id}` par l'identifiant de chaque compte.
   - Cliquez sur 'Try it out' puis 'Execute' pour supprimer chaque compte un par un.

3. **Vérification** :
   - Après avoir supprimé tous les comptes, vérifiez de nouveau via l'endpoint `/accounts` pour vous assurer qu'aucun compte n'est présent.

----
# Insertion des Nouveaux Comptes
----

Une fois que vous avez confirmé que tous les comptes ont été supprimés :

1. **Accédez à l'endpoint `/newAccount` dans Swagger**.
2. **Insérez un nouveau compte** en utilisant les exemples JSON fournis précédemment.
3. **Vérifiez les Insertion** en utilisant l'endpoint `/accounts` pour confirmer que les comptes ont bien été ajoutés.

----
# Conclusion
----

En commençant par supprimer tous les comptes existants, vous vous assurez que votre environnement est propre avant de procéder à de nouvelles insertions. Utilisez Swagger pour tester chaque opération de manière séquentielle et vérifier que chaque étape réussit avant de passer à la suivante.




