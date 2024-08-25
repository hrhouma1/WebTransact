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
