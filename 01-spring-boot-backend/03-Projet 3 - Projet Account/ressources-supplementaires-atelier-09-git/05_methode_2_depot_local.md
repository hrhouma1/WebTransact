
# 📁 Méthode 2 : Comparaison avec un dépôt Git local temporaire

## Étapes :
1. **Créez un dépôt Git local temporaire** :
   ```bash
   mkdir comparaison
   cd comparaison
   git init
   ```

2. **Copiez les fichiers des deux versions** dans des sous-dossiers (`v2` et `v3`), puis ajoutez-les à Git :
   ```bash
   cp -r ../accounts-v2 v2
   cp -r ../accounts-v3 v3
   git add v2 v3
   git commit -m "Ajout des versions v2 et v3"
   ```

3. **Comparer les différences entre les deux versions** :
   ```bash
   git diff v2 v3
   ```

4. **Utilisation de `diff` pour comparer deux fichiers** :
   ```bash
   diff v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```
