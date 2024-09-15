# 🤖 **Méthode 4 : Automatisation via scripts Bash et Python**

Cette méthode consiste à automatiser le processus de comparaison des fichiers entre deux versions d'un projet en utilisant des scripts Bash ou Python. L'automatisation permet de gagner du temps lorsque vous devez comparer régulièrement de nombreux fichiers ou si vous voulez générer des rapports à partir des différences détectées.

# Objectif :
- Apprendre à écrire des scripts en **Bash** et **Python** pour automatiser la comparaison des fichiers entre deux versions d'un projet.
- Générer des **rapports automatiques** des différences, enregistrés dans des fichiers texte pour une analyse ultérieure.

---

# 📌 **Automatisation avec un script Bash**

Bash est une solution puissante pour automatiser des tâches sur les systèmes Unix/Linux. Dans cet exemple, nous allons comparer des fichiers entre les deux versions du projet **Accounts** en utilisant Bash et la commande `diff`, puis générer des rapports.

# Script Bash de base :

```bash
#!/bin/bash
dir_v2="./accounts-v2"
dir_v3="./accounts-v3"
files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java")

for file in "${files_to_compare[@]}"; do
    diff -u "$dir_v2/$file" "$dir_v3/$file" > "rapport_diff_${file}.txt"
    echo "Comparaison de $file terminée, différences enregistrées dans rapport_diff_${file}.txt"
done
```

# Explication détaillée du script :

1. **Variables définies pour les dossiers de comparaison** :
   - `dir_v2="./accounts-v2"` : Cette variable pointe vers le dossier contenant la version v2 du projet.
   - `dir_v3="./accounts-v3"` : Celle-ci pointe vers le dossier contenant la version v3.

2. **Liste des fichiers à comparer** :
   - `files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java")` : Cette variable contient une liste des fichiers spécifiques que vous voulez comparer. Ici, il s'agit d'un fichier Java (`AccountsController.java`). Vous pouvez ajouter plusieurs fichiers à cette liste.

3. **Boucle pour comparer les fichiers** :
   - `for file in "${files_to_compare[@]}"; do` : Cette boucle parcourt la liste des fichiers que vous avez définie dans `files_to_compare`. Pour chaque fichier, elle exécute la comparaison.

4. **Comparaison avec `diff`** :
   - `diff -u "$dir_v2/$file" "$dir_v3/$file"` : La commande `diff -u` compare le fichier dans `dir_v2` avec celui dans `dir_v3`. Le format `-u` est utilisé pour un affichage plus lisible, avec un contexte de ligne autour des différences.
   
5. **Génération d'un rapport** :
   - `> "rapport_diff_${file}.txt"` : Les résultats de la commande `diff` sont redirigés vers un fichier texte. Chaque rapport de différence est enregistré dans un fichier nommé en fonction du fichier comparé.

6. **Affichage d'un message de confirmation** :
   - `echo "Comparaison de $file terminée..."` : Cette ligne affiche un message dans le terminal pour chaque fichier, indiquant que la comparaison est terminée et que le rapport a été généré.

---

# ⚙️ **Script Bash avancé avec options supplémentaires**

Ce script Bash avancé ajoute des fonctionnalités telles que l'ignorance des différences d'espaces, la comparaison de plusieurs fichiers, et la création d'un répertoire pour stocker les rapports.

```bash
#!/bin/bash
dir_v2="./accounts-v2"
dir_v3="./accounts-v3"
output_dir="./comparaison_rapports"
files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java" "src/main/resources/application.properties")

# Créer un répertoire pour stocker les rapports
mkdir -p $output_dir

for file in "${files_to_compare[@]}"; do
    diff -u --ignore-all-space "$dir_v2/$file" "$dir_v3/$file" > "$output_dir/rapport_diff_$(basename $file).txt"
    echo "Différences enregistrées dans $output_dir/rapport_diff_$(basename $file).txt"
done

echo "Résumé des différences :"
diff -rq "$dir_v2" "$dir_v3"
```

# Explication du script avancé :

1. **Création d'un répertoire pour stocker les rapports** :
   - `mkdir -p $output_dir` : Cette commande crée un répertoire appelé `comparaison_rapports` (si celui-ci n'existe pas déjà) où les rapports de comparaison seront stockés.

2. **Option pour ignorer les différences d'espaces** :
   - `diff -u --ignore-all-space "$dir_v2/$file" "$dir_v3/$file"` : L'option `--ignore-all-space` permet d'ignorer les différences liées aux espaces dans les fichiers. Cela est particulièrement utile si les modifications de formatage (comme les espaces) ne sont pas pertinentes pour votre analyse.

3. **Génération d'un résumé des différences** :
   - `diff -rq "$dir_v2" "$dir_v3"` : Cette commande génère un résumé rapide des différences entre les deux répertoires, en listant simplement les fichiers modifiés, ajoutés ou supprimés, sans afficher les détails ligne par ligne.

---

# 🐍 **Automatisation avec un script Python**

Python est une alternative puissante à Bash, surtout pour des tâches d'automatisation plus complexes. Dans cet exemple, nous allons utiliser le module `difflib` de Python pour comparer des fichiers entre deux versions d'un projet.

# Script Python de base :

```python
import os
import difflib

dir_v2 = './accounts-v2'
dir_v3 = './accounts-v3'

files_to_compare = ['src/main/java/com/eazybytes/accounts/controller/AccountsController.java']

def compare_files(file_v2, file_v3):
    with open(file_v2) as f1, open(file_v3) as f2:
        diff = difflib.unified_diff(f1.readlines(), f2.readlines(), fromfile=file_v2, tofile=file_v3)
        return ''.join(diff)

for file in files_to_compare:
    file_v2 = os.path.join(dir_v2, file)
    file_v3 = os.path.join(dir_v3, file)

    report = compare_files(file_v2, file_v3)
    report_file = f'rapport_diff_{file.replace("/", "_")}.txt'
    with open(report_file, 'w') as f:
        f.write(report)

    print(f'Comparaison de {file} terminée, rapport généré dans {report_file}.')
```

# Explication du script Python :

1. **Définition des répertoires** :
   - `dir_v2 = './accounts-v2'` et `dir_v3 = './accounts-v3'` : Ces variables définissent les chemins vers les répertoires contenant les versions v2 et v3 du projet.

2. **Liste des fichiers à comparer** :
   - `files_to_compare = ['src/main/java/com/eazybytes/accounts/controller/AccountsController.java']` : Une liste des fichiers à comparer. Vous pouvez ajouter d'autres fichiers en les séparant par des virgules dans cette liste.

3. **Fonction de comparaison de fichiers** :
   - `def compare_files(file_v2, file_v3)` : Cette fonction utilise le module `difflib.unified_diff` pour comparer deux fichiers et renvoyer les différences sous forme de chaîne de caractères.

4. **Boucle pour parcourir les fichiers à comparer** :
   - `for file in files_to_compare` : Cette boucle parcourt la liste des fichiers à comparer, exécute la fonction `compare_files` pour chaque fichier, et génère un rapport des différences.

5. **Génération et enregistrement des rapports** :
   - `report_file = f'rapport_diff_{file.replace("/", "_")}.txt'` : Chaque rapport est enregistré dans un fichier texte, avec un nom basé sur le fichier comparé.
   - `with open(report_file, 'w') as f` : Les résultats de la comparaison sont écrits dans ce fichier pour une consultation ultérieure.

---

# ⚠️ **Conseils** :

- **Astuce 1** : Si vous travaillez sur des systèmes Windows, vous pouvez utiliser **Git Bash** ou **WSL** (Windows Subsystem for Linux) pour exécuter des scripts Bash.
  
- **Astuce 2** : Pour exécuter un script Python, assurez-vous d'avoir Python installé sur votre machine. Vous pouvez vérifier la version avec :
  ```bash
  python --version
  ```

- **Astuce 3** : Si vous comparez un grand nombre de fichiers, utilisez des **listes** dans vos scripts pour gérer plusieurs comparaisons en une seule exécution.

---

# Résumé :

Avec ces scripts automatisés, vous pouvez comparer rapidement et efficacement plusieurs fichiers entre deux versions d’un projet. Que vous utilisiez **Bash** ou **Python**, ces scripts génèrent des rapports de comparaison détaillés, vous permettant de documenter les différences et de les analyser ultérieurement. Cela permet de gagner du temps lors de la comparaison répétée de fichiers ou de projets entiers.

Cette méthode est particulièrement utile pour des projets de grande envergure où vous avez de nombreux fichiers à comparer régulièrement. Elle est également idéale pour les équipes de développement qui souhaitent automatiser le processus de comparaison afin de garantir que les modifications entre les versions sont bien documentées et compréhensibles.

---

# 📝 **Pourquoi utiliser des scripts d'automatisation ?**

L’utilisation de scripts Bash ou Python pour automatiser les comparaisons est une méthode très efficace, car :

1. **Gain de temps** : Si vous devez comparer de nombreux fichiers ou si vous effectuez cette tâche de manière récurrente, l'automatisation permet d'éviter de répéter manuellement les mêmes commandes.

2. **Rapports structurés** : Les résultats de la comparaison sont automatiquement enregistrés dans des fichiers texte. Vous pouvez ensuite les consulter, les partager avec vos collègues ou les archiver pour référence future.

3. **Personnalisation facile** : Vous pouvez modifier ces scripts pour inclure des options supplémentaires, comme ignorer certaines différences mineures (espaces, commentaires, etc.) ou limiter la comparaison à certains types de fichiers (fichiers source, fichiers de configuration, etc.).

4. **Adaptabilité** : Les scripts peuvent être adaptés à différents environnements. Que vous travailliez sous Linux, macOS ou Windows (avec Git Bash), ces scripts sont flexibles et portables.

---

# ⚙️ **Exemples d'extension des scripts** :

- **Ajouter la prise en charge de plusieurs types de fichiers** :
   - Vous pouvez modifier la variable `files_to_compare` pour inclure plusieurs types de fichiers (Java, XML, JSON, etc.). Cela vous permet de comparer tous les fichiers d'un projet en une seule fois.

- **Ignorer les fichiers spécifiques** :
   - Ajoutez des options dans le script Bash ou Python pour ignorer certains fichiers qui ne sont pas pertinents (comme les fichiers temporaires ou les fichiers générés automatiquement).

- **Générer des rapports au format HTML** :
   - Si vous souhaitez rendre les rapports plus lisibles, vous pouvez modifier les scripts Python pour générer des rapports au format HTML au lieu de fichiers texte. Cela vous permet de les visualiser dans un navigateur.

---

# Conclusion :

L’automatisation des comparaisons avec des scripts Bash ou Python est une compétence essentielle pour les développeurs qui gèrent des projets complexes avec de nombreuses versions. Cette méthode vous permet de :

- **Gagner du temps et d’éviter les erreurs humaines** dans les comparaisons manuelles.
- **Standardiser les processus** de comparaison et de documentation des différences entre les versions.
- **Accroître la productivité** en vous concentrant sur les analyses des changements plutôt que sur la répétition des tâches de comparaison.

Que vous travailliez sur de petits projets ou de grandes applications, cette méthode est particulièrement utile pour maintenir un suivi clair et efficace des modifications entre différentes versions d'un projet.

---

# 💡 **Récapitulatif des scripts :**

- **Script Bash de base** : Comparaison simple de fichiers avec génération de rapports texte.
- **Script Bash avancé** : Comparaison multiple de fichiers, prise en charge des exclusions d’espaces, et génération de rapports dans un dossier dédié.
- **Script Python** : Utilisation de `difflib` pour une comparaison détaillée des fichiers, avec possibilité de générer des rapports texte pour chaque comparaison.
