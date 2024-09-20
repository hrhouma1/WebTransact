## Scénario

Imaginons que vous travaillez sur le projet de recherche d'utilisateurs GitHub avec un collègue. Vous avez chacun votre propre branche de fonctionnalité :

- Votre branche : `feature-search-improvements`
- La branche de votre collègue : `feature-ui-enhancements`

# Étape 1 : Configuration initiale

```bash
# Cloner le dépôt
git clone https://github.com/votre-repo/github-user-search.git
cd github-user-search

# Créer et basculer sur votre branche de fonctionnalité
git checkout -b feature-search-improvements
```

# Étape 2 : Faire des modifications

Modifiez le fichier HTML pour améliorer la fonction de recherche :

```html
<!-- Modification dans la fonction searchUsers -->
async function searchUsers() {
    const searchTerm = searchInput.value.trim();
    if (searchTerm.length === 0) {
        resultsContainer.innerHTML = '';
        return;
    }

    try {
        const response = await fetch(`https://api.github.com/search/users?q=${searchTerm}&per_page=10`);
        const data = await response.json();
        displayUsers(data.items);
    } catch (error) {
        console.error('Erreur lors de la recherche:', error);
    }
}
```

# Étape 3 : Commiter vos changements

```bash
git add index.html
git commit -m "Amélioration de la fonction de recherche pour afficher 10 résultats"
```

# Étape 4 : Fetch des changements distants

```bash
git fetch origin
```

Cette commande récupère les dernières modifications du dépôt distant sans les fusionner dans votre branche locale.

# Étape 5 : Rebase sur la branche principale

```bash
git rebase origin/main
```

Cette commande réapplique vos commits sur le dessus des derniers changements de la branche principale.

# Étape 6 : Résoudre les conflits (si nécessaire)

Si des conflits surviennent pendant le rebase, vous devrez les résoudre manuellement :

1. Ouvrez les fichiers en conflit et résolvez les différences.
2. Ajoutez les fichiers résolus avec `git add`.
3. Continuez le rebase avec `git rebase --continue`.

# Étape 7 : Push de vos changements

```bash
git push origin feature-search-improvements --force-with-lease
```

L'option `--force-with-lease` est plus sûre que `--force` car elle vérifie que vous n'écrasez pas les commits d'autres personnes.

# Différences entre rebase, pull et fetch

1. `git fetch` :
   - Récupère les changements du dépôt distant sans les fusionner.
   - Utile pour voir les modifications avant de les intégrer.

2. `git pull` :
   - Équivalent à `git fetch` suivi de `git merge`.
   - Fusionne automatiquement les changements distants dans votre branche locale.

3. `git rebase` :
   - Réapplique vos commits locaux sur le dessus des commits distants.
   - Crée un historique linéaire plus propre.

# Exemple de workflow avec pull vs rebase

# Utilisation de pull :

```bash
git checkout feature-search-improvements
git pull origin main
# Résoudre les conflits si nécessaire
git push origin feature-search-improvements
```

# Utilisation de rebase :

```bash
git checkout feature-search-improvements
git fetch origin
git rebase origin/main
# Résoudre les conflits si nécessaire
git push origin feature-search-improvements --force-with-lease
```

La principale différence est que le rebase crée un historique plus linéaire en réappliquant vos commits sur le dessus des changements distants, tandis que le pull crée un commit de fusion.

En utilisant ces commandes et techniques, vous pouvez gérer efficacement les modifications de votre projet de recherche d'utilisateurs GitHub tout en maintenant un historique de commits propre et linéaire.

