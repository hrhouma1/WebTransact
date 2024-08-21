# pratique 01 - Guide de démarrage rapide avec Git

# Objectif

- Ce guide fournit une série de commandes Git de base pour initialiser un dépôt, ajouter des fichiers, configurer les informations d'utilisateur, et pousser les changements vers un dépôt distant.

# Étapes

# 1. Initialiser un dépôt Git

Commencez par initialiser un nouveau dépôt Git dans votre répertoire de projet :

```bash
git init
```

# 2. Vérifier l'état du dépôt

Vous pouvez vérifier l'état de votre dépôt à tout moment avec :

```bash
git status
```

# 3. Créer des fichiers

Créez trois fichiers nommés `page1.txt`, `page2.txt`, et `page3.txt` :

```bash
touch page1.txt page2.txt page3.txt
```

# 4. Vérifier à nouveau l'état

Après avoir créé les fichiers, vérifiez l'état du dépôt :

```bash
git status
```

# 5. Ajouter les fichiers à l'index

Ajoutez tous les fichiers créés à l'index (staging area) :

```bash
git add .
```

# 6. Vérifier l'état après ajout

Vérifiez l'état du dépôt après avoir ajouté les fichiers :

```bash
git status
```

# 7. Configurer les informations utilisateur globales

Configurez votre nom et email utilisateur globalement :

```bash
git config --global user.name "hrhouma"
git config --global user.email "rehoumahaythem@gmail.com"
```

## Remarque :
- Vous pouvez remplacer "hrhouma" et "rehoumahaythem@gmail.com" par votre utilisateur global à vous

# 8. Configurer les informations utilisateur locales

Configurez des informations utilisateur spécifiques à ce dépôt :

```bash
git config --local user.name "dev"
git config --local user.email "dev_alex@gmail.com"
```
- Vous pouvez remplacer "dev" et "dev_alex@gmail.com" par votre utilisateur local à vous

# 9. Commit des fichiers

Enregistrez les modifications avec un message de commit :

```bash
git commit -m "Ajout des pages page1.txt page2.txt page3.txt"
```

# 10. Vérifier l'état après le commit

Vérifiez l'état de votre dépôt après avoir effectué le commit :

```bash
git status
```

# 11. Ajouter un dépôt distant

Ajoutez un dépôt distant nommé `origin` :

```bash
git remote add origin https://github.com/hrhouma/deploiement1.git
```

# 12. Renommer la branche principale

Renommez la branche principale en `master` :

```bash
git branch -M master
```

# 13. Pousser les changements vers le dépôt distant

Poussez vos changements vers la branche `master` sur le dépôt distant :

```bash
git push -u origin master
```

# 14. Vérifier la configuration Git

Pour voir la configuration actuelle de votre dépôt, utilisez :

```bash
cat .git/config
```



| **Commande Git** | **Action Git**                         | **Analogie de la valise**                                           | **Description en vrai vie**                                   |
|------------------|----------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------|
| `git add`        | Ajouter les fichiers à l'index         | Mettre des objets dans la valise                                    | Préparer les fichiers à être inclus dans le prochain commit    |
| `git commit`     | Enregistrer les changements            | Fermer la valise et la préparer pour le voyage                      | Enregistrer définitivement les changements dans le dépôt local |
| `git push`       | Envoyer les changements vers un dépôt distant | Envoyer la valise à la maison de vacances (destination finale) | Partager les changements avec d'autres en les envoyant sur un dépôt distant (comme GitHub) |

### Explication détaillée :

- **Git add** : Imagine que tu choisis des vêtements et des objets pour un voyage. En les mettant dans la valise, tu te prépares à emporter ces articles. Avec `git add`, tu fais la même chose pour tes fichiers : tu les "prépares" à être inclus dans le commit.

- **Git commit** : Une fois ta valise bien remplie, tu la fermes et la prépares à être envoyée. Cela signifie que tout ce que tu as mis dans la valise est prêt et ne peut plus être changé. En faisant `git commit`, tu enregistres tous les fichiers ajoutés pour qu'ils soient une partie permanente de l'historique de ton projet.

- **Git push** : Enfin, tu envoies ta valise à ta destination de vacances. Tes amis ou ta famille peuvent ouvrir la valise et utiliser ce que tu y as mis. Avec `git push`, tu envoies tes commits vers un dépôt distant, comme GitHub, où d'autres peuvent accéder à ton travail.
