### L'histoire de Paula et ses coéquipiers : Collaborer avec Git pour créer un projet ensemble

Paula, une étudiante en programmation, est très motivée par la gestion de projets en groupe. Elle décide de créer un projet avec l'aide de ses amis Eric, Ludovik, et Benjamin. Le projet consiste à développer une application web qui permet aux étudiants de partager leurs idées et ressources pour améliorer leur apprentissage.

Paula, en tant que chef de projet, initie la première version du projet, et chaque membre de l'équipe travaille sur une fonctionnalité distincte à travers différentes branches Git. Voici comment Paula et son équipe collaborent pour mener à bien ce projet.

---

## Projet : Application de partage pour les étudiants

### 1. Créer un nouveau répertoire pour le projet

Paula commence par créer un répertoire pour l'application web :

```bash
mkdir partageEtudiants
cd partageEtudiants
```

### 2. Initialiser un dépôt Git

Elle initialise ensuite un dépôt Git pour suivre l'évolution du projet :

```bash
git init
```

### 3. Créer la branche principale

Paula crée une branche `main` pour représenter la version stable du projet :

```bash
git branch -M main
```

### 4. Ajouter le premier fichier README

Elle crée un fichier README pour décrire le projet :

```bash
echo "# Application de partage pour les étudiants" > README.md
git add README.md
git commit -m "Initial commit: Added README file"
```

### 5. Création d'une branche pour une nouvelle fonctionnalité par Paula

Paula crée une nouvelle branche `interface` pour développer l'interface utilisateur de l'application :

```bash
git checkout -b interface
```

### 6. Paula commence à travailler sur l'interface utilisateur

Dans la branche `interface`, Paula crée les fichiers nécessaires pour l'interface utilisateur :

```bash
mkdir ui
echo "<html><body><h1>Bienvenue sur notre application de partage</h1></body></html>" > ui/index.html
git add ui/index.html
git commit -m "Created the initial UI for the homepage"
```

### 7. Paula pousse ses changements sur la branche distante

Paula pousse la branche `interface` vers le dépôt distant pour que les autres membres de l'équipe puissent y accéder :

```bash
git push -u origin interface
```

### 8. Eric commence à travailler sur la gestion des utilisateurs

Eric, qui est responsable de la gestion des utilisateurs, crée une nouvelle branche `gestion-utilisateurs` à partir de `main` :

```bash
git checkout main
git checkout -b gestion-utilisateurs
```

### 9. Eric ajoute la gestion des utilisateurs

Dans la branche `gestion-utilisateurs`, Eric ajoute un fichier pour la gestion des utilisateurs :

```bash
mkdir users
echo "module.exports = function registerUser() { console.log('User registered'); };" > users/user.js
git add users/user.js
git commit -m "Added user registration functionality"
```

### 10. Ludovik travaille sur la base de données

Ludovik, en charge de la base de données, crée une branche `database` :

```bash
git checkout main
git checkout -b database
```

Il configure la base de données :

```bash
mkdir db
echo "CREATE TABLE users (id INT, name VARCHAR(100));" > db/schema.sql
git add db/schema.sql
git commit -m "Database schema for users created"
```

### 11. Benjamin intègre une fonctionnalité de messagerie

Benjamin crée une branche `messaging` pour ajouter une fonctionnalité de messagerie entre étudiants :

```bash
git checkout main
git checkout -b messaging
```

Il commence à travailler sur le backend de la messagerie :

```bash
mkdir messaging
echo "module.exports = function sendMessage() { console.log('Message sent'); };" > messaging/message.js
git add messaging/message.js
git commit -m "Added messaging functionality"
```

### 12. Fusion des branches dans `main`

Une fois que toutes les fonctionnalités sont prêtes, Paula décide de fusionner les branches dans `main`. Elle commence par fusionner `interface` :

```bash
git checkout main
git merge interface
```

Ensuite, elle fusionne les autres branches :

```bash
git merge gestion-utilisateurs
git merge database
git merge messaging
```

### 13. Résolution des conflits (si nécessaire)

Paula pourrait rencontrer des conflits lors de la fusion. Elle résout les conflits et finalise la fusion.

### 14. Pousser la version finale du projet

Paula pousse la version finale sur la branche `main` :

```bash
git push origin main
```

---

### Conclusion

Grâce à cette approche collaborative utilisant des branches, Paula et son équipe ont réussi à créer une application de partage pour les étudiants. Chaque membre a pu travailler de manière indépendante sur sa fonctionnalité, puis les intégrer harmonieusement dans une version stable du projet.
