# 📝 **Introduction**

# Objectif de l’exercice :

Cet exercice a pour objectif de vous initier à différentes techniques de comparaison de versions d’un projet logiciel, tant avec des outils en ligne de commande qu'avec des environnements de développement intégrés (IDE). Vous allez comparer deux versions du projet **Accounts** (v2 et v3), en utilisant des commandes Git, des outils graphiques, ainsi que des scripts d'automatisation pour effectuer des comparaisons approfondies.

# Ce que vous apprendrez :

1. **Comparer des versions avec et sans IDE** : Vous découvrirez comment utiliser à la fois des outils en ligne de commande pour effectuer des comparaisons de code et des environnements de développement intégrés (comme Visual Studio Code ou IntelliJ IDEA) pour faciliter la visualisation et la navigation dans les différences entre les versions.

2. **Explorer la comparaison entre deux fichiers spécifiques** : Vous allez apprendre à identifier et analyser des changements précis dans des fichiers clés du projet en les comparant entre deux branches ou versions différentes.

3. **Comparer des fichiers entre branches Git** : Vous allez également explorer comment comparer des fichiers spécifiques entre deux branches de développement, ce qui vous permettra de suivre les changements dans des environnements de collaboration où plusieurs branches sont en cours de développement.

4. **Ignorer les différences mineures** : Grâce à des commandes avancées, vous apprendrez à ignorer les changements mineurs tels que les espaces ou les commentaires lors de la comparaison, vous concentrant ainsi sur les modifications significatives du code.

5. **Automatiser les comparaisons** : En plus de comparer manuellement des fichiers, vous verrez comment automatiser ce processus via des scripts en Bash ou Python, pour des projets comportant de nombreux fichiers.

# Pourquoi c’est important :

- **Travailler efficacement sans IDE** : Bien que les IDE facilitent les comparaisons de code, savoir utiliser des outils en ligne de commande comme `git diff` est essentiel lorsque vous travaillez dans des environnements dépourvus d’interface graphique ou dans des environnements de production.
  
- **Utiliser des IDE pour accélérer l'analyse** : En parallèle, vous verrez comment utiliser les fonctionnalités de comparaison intégrées des IDE pour une navigation plus fluide et rapide entre les différences de code, ce qui est particulièrement utile dans des projets de grande envergure.

- **Analyser des modifications dans un projet collaboratif** : En travaillant sur des branches différentes, il est important de savoir identifier les changements apportés à des fichiers critiques entre deux branches. Cela vous aide à comprendre comment les modifications dans une branche affecteront les autres branches du projet, avant de les fusionner.

# Contexte du projet *Accounts* :

Le projet **Accounts** est un système de gestion de comptes utilisé dans des environnements professionnels pour gérer les informations relatives aux utilisateurs et à leurs comptes. Dans cet exercice, vous allez comparer deux versions de ce projet, **v2** et **v3**, qui comportent des modifications importantes. Cela inclut des ajustements dans les fonctionnalités, des corrections de bugs, ou des révisions de la structure du code.

# Méthodes que vous allez explorer :

- **Comparaison sans IDE** : Vous allez apprendre à utiliser les commandes **Git** comme `git diff`, `git log` et `git checkout` pour comparer les versions de fichiers, examiner l’historique des modifications, et naviguer entre les branches directement en ligne de commande.
  
- **Comparaison avec IDE** : Vous allez découvrir comment utiliser des environnements de développement comme **Visual Studio Code** ou **IntelliJ IDEA** pour comparer facilement deux versions de fichiers, effectuer des diff visuels ligne par ligne, et comparer des branches entières.

- **Comparaison entre deux fichiers spécifiques** : Vous identifierez les différences entre des fichiers spécifiques, comme par exemple `AccountsController.java`, dans les versions **v2** et **v3**, et comprendrez comment ces modifications affectent le projet global.

- **Comparaison entre branches Git** : Vous allez comparer des fichiers entre deux branches différentes du projet pour suivre les modifications introduites dans une branche de développement avant de les fusionner avec la branche principale (par exemple, comparer les fichiers entre une branche `feature` et `main`).

# Résultat attendu :

À la fin de cet exercice, vous devrez être en mesure de :
- **Comparer des versions de projet avec et sans IDE(*outils en ligne de commande*)**, en utilisant des outils adaptés à chaque environnement.
- **Identifier les changements entre deux versions ou branches spécifiques** du projet.
- **Analyser et décrire les impacts des modifications** sur le code, la structure et les dépendances du projet.
- **Proposer des améliorations** ou des ajustements en fonction des différences observées.
