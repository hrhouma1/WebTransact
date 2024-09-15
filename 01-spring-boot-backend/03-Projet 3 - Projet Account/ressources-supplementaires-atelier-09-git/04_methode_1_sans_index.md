
# 📝 Méthode 1 : Comparaison directe sans index (en dehors d'un dépôt Git)

## Étapes :
1. **Clonez les deux versions** dans des dossiers distincts :
   ```bash
   git clone https://github.com/hrhouma1/accounts-v2
   git clone https://github.com/hrhouma1/accounts-v3
   ```

2. **Examinez la structure des projets** et comparez les fichiers et dossiers.

3. **Comparer un fichier spécifique** :
   ```bash
   git diff --no-index ./accounts-v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java ./accounts-v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```

4. **Comparer les dossiers avec des exclusions** (par ex. exclure les répertoires de tests) :
   ```bash
   git diff --no-index --exclude=./accounts-v2/src/test/ ./accounts-v2 ./accounts-v3
   ```
