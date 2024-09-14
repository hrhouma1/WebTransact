---
# Exercice : Comparaison des versions v2 et v3 du projet Accounts
---

Dans cet exercice, vous allez comparer deux versions différentes du projet Accounts pour identifier les changements effectués entre la version v2 et la version v3.

# Étapes :

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

4. Pour une comparaison plus visuelle, vous pouvez utiliser un outil de diff graphique comme Meld, Beyond Compare, ou l'extension "Compare Folders" de Visual Studio Code[3].

5. Analysez les différences et notez les changements suivants :
   - Fichiers ajoutés ou supprimés
   - Modifications de code dans les fichiers existants
   - Changements dans la structure du projet
   - Mises à jour des dépendances (si applicable)

6. Résumez les principaux changements observés entre la version v2 et la version v3 du projet.

### Questions à répondre :

1. Quels sont les nouveaux fichiers ou dossiers ajoutés dans la version v3 ?
2. Y a-t-il des fichiers ou dossiers qui ont été supprimés ou renommés ?
3. Quelles sont les principales modifications de code que vous avez observées ?
4. Y a-t-il des changements dans la configuration du projet ou dans les dépendances ?
5. Selon vous, quel est l'objectif principal des modifications apportées dans la version v3 ?

### Conseils :

- Utilisez des outils de comparaison de fichiers pour faciliter l'identification des différences[3].
- Concentrez-vous sur les changements significatifs plutôt que sur les modifications mineures (comme les espaces ou les commentaires).
- N'hésitez pas à consulter la documentation de Git pour des commandes avancées de comparaison[2][4].

En réalisant cet exercice, les étudiants pourront développer leurs compétences en analyse de code, en compréhension des évolutions de projets, et en utilisation des outils de versionnage comme Git.

-----
# Références :
-----
- [1] https://github.com/hrhouma1/accounts-v2
- [2] https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits
- [3] https://stackoverflow.com/questions/1968512/getting-the-difference-between-two-repositories
- [4] https://refine.dev/blog/git-diff-command/
- [5] https://www.atlassian.com/git/tutorials/saving-changes/git-diff
- [6] https://docs.github.com/en/repositories/releasing-projects-on-github/comparing-releases
- [7] https://www.reddit.com/r/git/comments/108ivsp/what_is_the_best_way_to_diff_two_different_repos/
