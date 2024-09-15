# 📁 **Méthode 2 : Comparaison avec un dépôt Git local temporaire**

Dans cette méthode, vous allez créer un dépôt Git local temporaire pour comparer deux versions d’un projet. Cela vous permettra de tirer parti des fonctionnalités de Git, comme le suivi des modifications et l’historique des commits, même si vous ne travaillez pas dans un véritable environnement Git multi-branches.

# Objectif :
- Apprendre à créer un dépôt Git local pour suivre les changements entre deux versions d’un projet.
- Comprendre comment utiliser `git diff` pour comparer des sous-dossiers ou des fichiers spécifiques en utilisant un dépôt Git temporaire.

---

# 📌 **Étapes détaillées :**

# 1. **Créez un dépôt Git local temporaire**

Un dépôt Git est un espace où vous pouvez suivre l’évolution de vos fichiers. Dans cet exercice, nous allons créer un dépôt temporaire pour comparer les deux versions du projet.

# Commandes :
1. **Créer un nouveau dossier pour la comparaison** :
   ```bash
   mkdir comparaison
   cd comparaison
   ```
   - **Explication** : Vous créez un nouveau dossier appelé `comparaison` qui servira de dépôt Git temporaire pour comparer les deux versions du projet *Accounts*.
   
2. **Initialiser un dépôt Git dans ce dossier** :
   ```bash
   git init
   ```
   - **Explication** : Cette commande initialise un nouveau dépôt Git dans le dossier `comparaison`. Ce dépôt vous permettra de suivre les modifications entre les deux versions du projet.

---

# 2. **Copiez les fichiers des deux versions dans des sous-dossiers (`v2` et `v3`)**

L’objectif ici est de copier les fichiers des deux versions (`v2` et `v3`) dans des sous-dossiers du dépôt Git que vous venez de créer. Cela vous permet de comparer ces deux versions comme si elles faisaient partie du même projet Git, même si elles ne le sont pas en réalité.

# Commandes :
1. **Copier les fichiers de la version v2** :
   ```bash
   cp -r ../accounts-v2 v2
   ```
   - **Explication** : Cette commande copie tous les fichiers du répertoire `accounts-v2` (préalablement cloné) dans un sous-dossier appelé `v2` dans votre dépôt temporaire.

2. **Copier les fichiers de la version v3** :
   ```bash
   cp -r ../accounts-v3 v3
   ```
   - **Explication** : De même, cette commande copie tous les fichiers du répertoire `accounts-v3` dans un sous-dossier appelé `v3` dans votre dépôt temporaire.

---

# 3. **Ajoutez les fichiers au dépôt Git**

Une fois les fichiers copiés, vous devez les ajouter au dépôt Git pour pouvoir utiliser les commandes de comparaison. Cette étape est essentielle pour suivre les modifications entre les deux versions.

# Commandes :
1. **Ajouter les fichiers copiés dans Git** :
   ```bash
   git add v2 v3
   ```
   - **Explication** : La commande `git add` indique à Git de suivre tous les fichiers dans les dossiers `v2` et `v3`. Vous dites à Git que vous voulez inclure ces fichiers dans le suivi du dépôt.

2. **Effectuer un commit** :
   ```bash
   git commit -m "Ajout des versions v2 et v3"
   ```
   - **Explication** : Le commit enregistre les fichiers dans le dépôt Git avec un message décrivant ce que vous avez fait. Ici, vous enregistrez les fichiers des deux versions avec un message indiquant que vous avez ajouté les versions v2 et v3 du projet *Accounts*.

---

# 4. **Comparer les différences entre les deux versions**

Maintenant que vous avez ajouté les deux versions dans Git, vous pouvez utiliser la commande `git diff` pour comparer les fichiers entre les deux sous-dossiers `v2` et `v3`. Cela vous permettra de visualiser les différences ligne par ligne entre les deux versions du projet.

# Commande :
   ```bash
   git diff v2 v3
   ```
   - **Explication** : Cette commande compare tous les fichiers des dossiers `v2` et `v3` et affiche les différences entre les deux versions. Les ajouts seront affichés en vert et les suppressions en rouge, ce qui vous permet de voir ce qui a changé entre les versions.

---

# 5. **Comparer des fichiers spécifiques**

Dans de nombreux cas, vous voudrez peut-être comparer un fichier spécifique au lieu de tous les fichiers. Par exemple, si vous savez que des modifications ont été apportées au fichier `AccountsController.java`, vous pouvez le comparer directement entre les deux versions.

# Commande :
   ```bash
   git diff v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```
   - **Explication** : 
     - `git diff` est utilisé pour comparer des fichiers spécifiques entre les deux versions.
     - Le chemin `v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java` fait référence à l'emplacement du fichier dans la version v2.
     - Le chemin `v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java` fait référence au même fichier dans la version v3.
   - **Résultat attendu** : Cette commande affichera les différences ligne par ligne entre le fichier `AccountsController.java` dans les deux versions du projet. Vous verrez quels changements ont été apportés à ce fichier particulier.

---

# 6. **Utilisation de `diff` pour comparer des fichiers sans Git**

Si vous ne voulez pas utiliser Git pour comparer les fichiers, vous pouvez utiliser la commande `diff`, qui est une alternative simple pour comparer deux fichiers ligne par ligne sans avoir besoin de Git. C’est une approche plus directe, utile si vous ne souhaitez pas gérer un dépôt Git.

# Commande :
   ```bash
   diff v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```
   - **Explication** : La commande `diff` compare deux fichiers directement, sans utiliser Git. Elle affiche les lignes qui diffèrent entre les deux fichiers, ce qui est utile pour une comparaison rapide et simple.

---

# ⚠️ **Conseils pour débutants** :
- **Astuce 1** : Utilisez `git status` à tout moment pour vérifier l’état actuel du dépôt Git et voir quels fichiers sont suivis ou non. Cela vous aidera à mieux comprendre où vous en êtes dans le processus.
  ```bash
  git status
  ```

- **Astuce 2** : N’oubliez pas de toujours vous placer dans le bon dossier avant de lancer une commande. Par exemple, avant d’utiliser `git diff`, assurez-vous d’être dans le dossier `comparaison`.
  
- **Astuce 3** : Si vous souhaitez voir un aperçu des différences sans trop de détails, utilisez `git diff --stat` pour afficher uniquement les noms des fichiers modifiés avec le nombre de lignes ajoutées ou supprimées.
  ```bash
  git diff --stat v2 v3
  ```

---

# Résumé :

Cette méthode vous permet de comparer deux versions d’un projet dans un dépôt Git local temporaire, même si elles ne font pas partie du même dépôt Git original. Vous pouvez ainsi utiliser toutes les commandes et fonctionnalités de Git pour analyser les différences entre les versions, tout en ayant la flexibilité de comparer des fichiers spécifiques.

Cette approche est plus puissante que la méthode 1, car elle vous permet de bénéficier des fonctionnalités de suivi et d’historique de Git, tout en restant relativement simple pour des débutants.
