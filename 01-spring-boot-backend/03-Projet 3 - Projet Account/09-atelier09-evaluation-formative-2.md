---
# 01 - Exercice : Comparaison des versions v2 et v3 du projet Accounts
---

Dans cet exercice, vous allez comparer deux versions différentes du projet Accounts pour identifier les changements effectués entre la version v2 et la version v3.

- Clonez les deux versions du projet dans des dossiers séparés :

```bash
git clone https://github.com/hrhouma1/accounts-v2
git clone https://github.com/hrhouma1/accounts-v3
```

- Pour une comparaison rapide , utilisez la commande *git diff*.
- Pour une comparaison plus visuelle, vous pouvez utiliser un outil de diff graphique de comparaison de fichiers comme *Meld*, *Beyond Compare*, ou l'extension "**Compare Folders**" de Visual Studio Code[3].
- Concentrez-vous sur les changements significatifs plutôt que sur les modifications mineures (comme les espaces ou les commentaires).
- N'hésitez pas à consulter la documentation de Git pour des commandes avancées de comparaison[2][4].

5. Analysez les différences et notez les changements suivants :
   - Fichiers ajoutés ou supprimés
   - Modifications de code dans les fichiers existants
   - Changements dans la structure du projet
   - Mises à jour des dépendances (si applicable)

---
# 02 - Questions à répondre 
---

1. Quels sont les nouveaux fichiers ou dossiers ajoutés dans la version v3 ?
2. Y a-t-il des fichiers ou dossiers qui ont été supprimés ou renommés ?
3. Quelles sont les principales modifications de code que vous avez observées ?
4. Y a-t-il des changements dans la configuration du projet ou dans les dépendances ?
5. Selon vous, quel est l'objectif principal des modifications apportées dans la version v3 ?

---
# 03 - Conseils 
---

**Utiliser des outils spécialisés pour comparer des fichiers :**
   - **Meld** (Linux/Windows) ou **Beyond Compare** (Windows/Linux/macOS) sont des outils graphiques de comparaison de fichiers très puissants. Ils permettent de visualiser facilement les différences ligne par ligne et sont plus ergonomiques pour des comparaisons fréquentes.
   - **DiffMerge** ou **KDiff3** sont aussi des options populaires pour comparer des fichiers ou des dossiers entiers.



-----
# 04 - Références pour vous aider !
-----
- [1] https://github.com/hrhouma1/accounts-v2
- [2] https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits
- [3] https://stackoverflow.com/questions/1968512/getting-the-difference-between-two-repositories
- [4] https://refine.dev/blog/git-diff-command/
- [5] https://www.atlassian.com/git/tutorials/saving-changes/git-diff
- [6] https://docs.github.com/en/repositories/releasing-projects-on-github/comparing-releases
- [7] https://www.reddit.com/r/git/comments/108ivsp/what_is_the_best_way_to_diff_two_different_repos/



---
# 05 -  Solutions :
---

---
# Méthode 1: comparaison directe sans index (en dehors d’un dépôt Git)
---

1. Clonez les deux versions du projet dans des dossiers séparés :

```bash
git clone https://github.com/hrhouma1/accounts-v2
git clone https://github.com/hrhouma1/accounts-v3
```

2. Examinez la structure des deux projets et comparez les fichiers et dossiers présents dans chaque version.

3. Utilisez la commande `git diff` pour comparer les fichiers spécifiques entre les deux versions. Par exemple :

```bash
mkdir accounts-compare
cd accounts-compare/
git clone https://github.com/hrhouma1/accounts-v2
git clone https://github.com/hrhouma1/accounts-v3
git diff --no-index ./accounts-v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java  ./accounts-v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java

```

Bien que la commande `git diff --no-index` fonctionne bien pour comparer des fichiers individuels en dehors d’un dépôt Git, voici quelques méthodes plus efficaces ou adaptées selon le contexte :

---
# Méthode 2: comparaison plus rapide ( dépôt Git local temporaire) mais *non visuelle*
---


- Si vous désirez effectuer la comparaison rapide de deux version, il faut **utiliser un dépôt Git local temporaire :**. Pour ce faire, créez un dossier indépendant danslequel vous copierez les deux fichiers à comparer par exemple les deux controlleurs *AccountsController.java* des versions **v2** et **v3** respectivement.
- Renommez les à  *AccountsControllerv1.java* et  *AccountsControllerv2.java*

![image](https://github.com/user-attachments/assets/037d9afd-a466-4e17-9a2e-503630925047)

   1. Créez un dépôt Git dans le répertoire temporaire :
      ```bash
      mkdir comparaison
      cd comparaison
      # copier et coller *AccountsControllerv1.java* et  *AccountsControllerv2.java*
      git init
      ```
   2. Utilisez `git diff` pour comparer les différentes versions de fichiers.
   
   Cela permet d'utiliser pleinement les fonctionnalités de Git comme le suivi des modifications, les comparaisons inter-commits, etc.

   3. **Utiliser `diff` ou `cmp` (en ligne de commande) :**
   Si vous recherchez une solution légère et rapide pour des comparaisons simples :
   - **`diff`** : Compare deux fichiers et affiche les différences :
     ```bash
     diff AccountsControllerv1.java AccountsControllerv2.java
     ```
     Il existe plusieurs options pour personnaliser l’affichage, comme ignorer les espaces avec `-w` :
     ```bash
     diff -w AccountsControllerv1.java AccountsControllerv2.java
     ```
   - **`cmp`** : Compare deux fichiers octet par octet et renvoie la première différence trouvée :
     ```bash
     cmp AccountsControllerv1.java AccountsControllerv2.java
     ```

---
# Méthode 3: **IDE avec fonction de comparaison intégrée (VISUELLE) :**
---

   Si vous travaillez dans un IDE comme **IntelliJ IDEA**, **VSCode**, ou **Eclipse**, ils ont souvent des fonctions intégrées pour comparer deux fichiers ou répertoires, directement dans l'interface graphique.

   - Sur **VSCode**, par exemple, vous pouvez ouvrir deux fichiers, faire un clic droit sur l'onglet du premier fichier et choisir **"Select for Compare"**, puis faire un clic droit sur le second fichier et sélectionner **"Compare with Selected"**.


![image](https://github.com/user-attachments/assets/d1d6aa2a-81de-421d-a774-d5043a6a7a15)
![image](https://github.com/user-attachments/assets/eab02667-51c6-42c4-8c07-b4b23f700a47)
![image](https://github.com/user-attachments/assets/34b29e07-1ecd-4986-8795-4b8419c8adbd)
![image](https://github.com/user-attachments/assets/78088416-165a-4a0a-83d2-086475cfdf3e)
![image](https://github.com/user-attachments/assets/388b5aed-5a7f-4838-999a-15be109e8314)
![image](https://github.com/user-attachments/assets/91564ecf-c33c-43ed-a861-6088b2c53366)
![image](https://github.com/user-attachments/assets/1f29f022-3f25-4e81-9758-9b59b8c5570a)





















---
# Annexe 1 : Guide détaillé pour la visualisation des modifications côte à côte de versions commitées dans Visual Studio Code
---

Cet annexe 1 fournit une explication détaillée sur comment utiliser Visual Studio Code pour comparer visuellement des modifications entre différentes versions d'un fichier dans un projet versionné avec Git. Cela peut être particulièrement utile pour des débutants qui apprennent à gérer des versions de code source.

## Utiliser les Fonctionnalités Git Intégrées de Visual Studio Code

**1. Ouvrir la Vue de Contrôle de Source :**
   - Dans Visual Studio Code, repérez l'icône de contrôle de source qui se trouve généralement sur le côté gauche de la fenêtre. Cette icône ressemble à une fourche ou à des branches qui se séparent, symbolisant le contrôle de version.

**2. Section des Modifications :**
   - Lorsque vous cliquez sur cette icône, la barre latérale affiche tous les fichiers qui ont été modifiés depuis le dernier commit. Vous verrez une liste de fichiers, chacun accompagné d'icônes indiquant s'ils ont été ajoutés, modifiés ou supprimés.
   - Trouvez et cliquez sur `AccountsController.java` ou le fichier qui vous intéresse. Cela ouvrira une vue qui montre les différences entre votre version actuelle du fichier et la dernière version enregistrée (commitée).

**3. Comparaison Côte à Côte :**
   - La fenêtre qui s'ouvre montre deux versions du fichier côte à côte. Le côté gauche représente l'ancienne version du fichier (avant vos modifications), et le côté droit montre ce que vous avez changé.
   - Les modifications sont colorées pour faciliter la compréhension : les suppressions sont indiquées en rouge et les ajouts en vert. Cette coloration aide à visualiser rapidement ce qui a été ajouté, modifié ou supprimé.

## Utiliser l'Extension GitLens pour des Comparaisons Avancées

**1. Installer GitLens :**
   - GitLens est une extension qui améliore les capacités de Visual Studio Code pour le contrôle de version Git. Pour l'installer, allez dans la vue Extensions (l'icône ressemble à des blocs empilés sur le côté gauche), tapez "GitLens" dans la barre de recherche, puis cliquez sur "Installer".

**2. Comparer des Branches ou des Commits :**
   - Une fois GitLens installé, ouvrez la palette de commandes en utilisant `Ctrl+Shift+P` (ou `Cmd+Shift+P` sur macOS), tapez "GitLens: Compare with..." et sélectionnez cette commande.
   - Vous serez invité à choisir entre différentes branches ou commits que vous souhaitez comparer. Sélectionnez les options qui correspondent aux versions que vous voulez voir côte à côte.
   - GitLens ouvrira une vue de comparaison similaire à celle des fonctionnalités intégrées, mais avec plus d'options et de détails sur les modifications entre les commits ou les branches.



---
# Annexe 2 : Comparaison de branches dans Visual Studio Code avec GitLens
---

- Références : https://stackoverflow.com/questions/42112526/how-to-compare-different-branches-in-visual-studio-code

Cet annexe 2 explique comment utiliser GitLens dans Visual Studio Code pour comparer efficacement des branches, permettant aux développeurs, de visualiser les modifications entre différentes versions de leur code.

### Installation de GitLens

**1. Installer GitLens :**
   - **Ouvrez Visual Studio Code.**
   - **Accédez à l'onglet "Extensions"** en cliquant sur l'icône qui ressemble à des carrés sur le côté gauche de la fenêtre.
   - **Recherchez "GitLens"** dans la barre de recherche en haut de l'onglet Extensions.
   - **Cliquez sur "Installer"** pour ajouter GitLens à votre environnement de développement.

### Configuration Initiale

**2. Configurer GitLens :**
   - Une fois GitLens installé, **redémarrez Visual Studio Code** pour vous assurer que l'extension est correctement chargée.
   - **Ouvrez la palette de commandes** avec `Ctrl+Shift+P` (ou `Cmd+Shift+P` sur macOS) et tapez `GitLens: Welcome`. Suivez les instructions pour configurer les paramètres de base selon vos préférences.

### Comparaison de Branches

**3. Lancer une Comparaison :**
   - Cliquez sur l'**icône GitLens** dans la barre latérale, qui apparaît avec le logo de GitLens après l'installation.
   - Sélectionnez **"Search & Compare"** pour accéder aux outils de comparaison.
   - Cliquez sur **"Compare References"**. Cette option vous permet de sélectionner les deux branches à comparer.

**4. Sélectionner les Branches à Comparer :**
   - Dans la fenêtre de comparaison, vous verrez deux listes déroulantes ou des champs pour entrer les noms des branches.
   - **Choisissez la première branche (branche A)** dans le premier menu déroulant.
   - **Choisissez la deuxième branche (branche B)** dans le deuxième menu déroulant.
   - GitLens affichera automatiquement les différences entre les branches sélectionnées.

**5. Examiner les Modifications :**
   - **Vue des fichiers modifiés :** La comparaison révèlera une liste de tous les fichiers qui ont des différences entre les branches sélectionnées.
   - **Détails des changements :** En cliquant sur un fichier spécifique, vous pouvez voir les modifications ligne par ligne, avec des différences clairement mises en évidence.

### Fonctionnalités Avancées

**6. Naviguer dans les Commits :**
   - GitLens permet aussi de **visualiser les commits** qui ont été faits dans chaque branche. Cela peut aider à comprendre le contexte des changements.
   - **Utilisez les flèches** pour naviguer entre les commits dans la vue détaillée.

**7. Editer Directement depuis la Comparaison :**
   - Si vous avez besoin de faire des ajustements, **vous pouvez éditer les fichiers directement** dans la vue de comparaison.
   - Ceci est particulièrement utile pour faire des corrections rapides sans quitter l'interface de comparaison.

### Conseils 

- **Prenez le temps de vous familiariser** avec l'interface de GitLens. Explorez les différentes options dans la barre latérale pour voir ce que chaque fonction peut faire.
- **Consultez la documentation de GitLens** pour des guides détaillés sur les caractéristiques spécifiques.
- **Pratiquez la comparaison** entre des branches peu complexes pour commencer, afin de comprendre le flux de travail sans se sentir submergé par des différences trop nombreuses ou complexes.

