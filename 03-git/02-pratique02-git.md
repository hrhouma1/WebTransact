```bash
# Créer un nouveau répertoire appelé ProjetJava
mkdir ProjetJava

# Naviguer dans le répertoire ProjetJava
cd ProjetJava

# Initialiser un dépôt Git local dans le répertoire ProjetJava
git init

# Vérifier l'état actuel du dépôt Git (affiche les fichiers suivis et non suivis)
git status

# Configurer votre nom d'utilisateur global pour Git
git config --global user.name "votreUserGithub"

# Configurer votre adresse email globale pour Git
git config --global user.email "votreVraiEmailGithub"

# Créer un nouveau fichier texte appelé votrenom.txt pour commencer à rédiger votre CV
touch votrenom.txt

# Vérifier à nouveau l'état du dépôt Git (le fichier votrenom.txt apparaîtra comme non suivi)
git status

# Ajouter le fichier votrenom.txt au suivi dans Git pour que votre travail soit sauvegardé et prêt à être partagé
git add votrenom.txt

# Vérifier l'état du dépôt Git pour confirmer que votrenom.txt est maintenant suivi
git status

# Configurer votre nom d'utilisateur local pour ce dépôt Git
git config --local user.name "votreUserGithub"

# Configurer votre adresse email locale pour ce dépôt Git
git config --local user.email "votreVraiEmailGithub"

# Effectuer un commit pour immortaliser la première version de votre CV, comme si vous graviez votre premier chapitre dans l'histoire de votre carrière
git commit -m "The journey begins: First draft of my CV added"

# Supprimer l'origine distante actuelle si elle existe
git remote remove origin

# Ajouter une nouvelle origine distante pointant vers votre dépôt GitHub, où votre histoire numérique sera partagée avec le monde
git remote add origin VOTRE_URL

# Renommer la branche actuelle en 'main' pour symboliser le début officiel de votre voyage
git branch -M main

# Pousser le contenu de la branche 'main' vers l'origine distante, lançant ainsi votre CV dans l'univers numérique
git push -u origin main

# Modification 1 : Vous commencez à écrire votre introduction, un premier aperçu de qui vous êtes et de vos aspirations
echo "Bonjour, je m'appelle Eric, et je suis un développeur passionné par la technologie. Voici une brève introduction sur moi." >> votrenom.txt

# Configurer le nom d'utilisateur de votre ami à votre gauche pour ce dépôt Git
git config --local user.name "usernameamiacotedevousa-gauche"

# Configurer l'adresse email de votre ami à votre gauche pour ce dépôt Git
git config --local user.email "EmailGithubdevotreamiacotedevousa-gauche"

# Effectuer un commit pour capturer ce moment où votre ami vous aide à raconter votre histoire
git commit -m "A friend's touch: Introduction added by l'ami à gauche"

# Supprimer l'origine distante actuelle si elle existe
git remote remove origin

# Ajouter une nouvelle origine distante pointant vers votre dépôt GitHub
git remote add origin VOTRE_URL

# Renommer la branche actuelle en 'main'
git branch -M main

# Pousser le contenu de la branche 'main' vers l'origine distante avec le nom de votre ami à gauche
git push -u origin main

# Modification 2 : Vous ajoutez vos réalisations, les fruits de votre travail, pour montrer au monde ce que vous avez accompli
echo "Ajout des certifications : AWS Certified Solutions Architect, Google Cloud Professional Data Engineer. Mise à jour des diplômes : Master en Informatique." >> votrenom.txt

# Configurer le nom d'utilisateur de votre ami à votre droite pour ce dépôt Git
git config --local user.name "usernameamiacotedevousa-DROITE"

# Configurer l'adresse email de votre ami à votre droite pour ce dépôt Git
git config --local user.email "EmailGithubdevotreamiacotedevousa-DROITE"

# Effectuer un commit pour immortaliser ces ajouts, comme si vous posiez une pierre angulaire dans l'édifice de votre carrière
git commit -m "Milestones achieved: Certifications and diplomas added by l'ami à droite"

# Supprimer l'origine distante actuelle si elle existe
git remote remove origin

# Ajouter une nouvelle origine distante pointant vers votre dépôt GitHub
git remote add origin VOTRE_URL

# Renommer la branche actuelle en 'main'
git branch -M main

# Pousser le contenu de la branche 'main' vers l'origine distante avec le nom de votre ami à droite
git push -u origin main
```
