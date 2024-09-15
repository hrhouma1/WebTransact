
# 🔍 Comparaison rapide avec git diff

## Comparaison rapide des fichiers avec Git Diff :
1. **Comparer tous les fichiers** entre les deux versions :
   ```bash
   git diff --no-index ./accounts-v2 ./accounts-v3
   ```

2. **Comparer uniquement certains types de fichiers** (par exemple les fichiers Java) :
   ```bash
   git diff --no-index ./accounts-v2/*.java ./accounts-v3/*.java
   ```

3. **Comparer des fichiers spécifiques** (ex. `AccountsController.java`) :
   ```bash
   git diff --no-index ./accounts-v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java ./accounts-v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```

4. **Ignorer les espaces et lignes blanches** lors de la comparaison :
   ```bash
   git diff --no-index --ignore-space-at-eol ./accounts-v2 ./accounts-v3
   ```
