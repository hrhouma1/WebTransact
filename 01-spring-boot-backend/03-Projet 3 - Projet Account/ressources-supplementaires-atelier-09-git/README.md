# 🗂️ Table des matières
1. **Introduction** - [01_introduction.md](01_introduction.md)
2. **Clone des versions** - [02_clone_versions.md](02_clone_versions.md)
3. **Comparaison rapide avec `git diff`** - [03_comparaison_rapide.md](03_comparaison_rapide.md)
4. **Méthode 1 : Comparaison directe sans index** - [04_methode_1_sans_index.md](04_methode_1_sans_index.md)
5. **Méthode 2 : Comparaison avec dépôt Git local temporaire** - [05_methode_2_depot_local.md](05_methode_2_depot_local.md)
6. **Méthode 3 : Comparaison visuelle avec un IDE** - [06_methode_3_comparaison_visuelle.md](06_methode_3_comparaison_visuelle.md)
7. **Méthode 4 : Automatisation via scripts Bash et Python** - [07_methode_4_automatisation.md](07_methode_4_automatisation.md)
8. **Questions et réflexion** - [08_questions_reflexion.md](08_questions_reflexion.md)
9. **Conseils et recommandations** - [09_conseils.md](09_conseils.md)
10. **Références utiles** - [10_references.md](10_references.md)

---

## 📝 **01_introduction.md**
### Objectif de l’exercice :
- **Comparer deux versions** du projet **Accounts** (v2 et v3).
- **Identifier les modifications principales**, analyser les changements de code, la structure du projet, et les dépendances.

---

## 🛠️ **02_clone_versions.md**
### Commandes pour cloner les deux versions :
1. **Cloner la version v2** :
   ```bash
   git clone https://github.com/hrhouma1/accounts-v2
   ```

2. **Cloner la version v3** :
   ```bash
   git clone https://github.com/hrhouma1/accounts-v3
   ```

---

## 🔍 **03_comparaison_rapide.md**
### Comparaison rapide des fichiers avec Git Diff :
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

---

## 📝 **04_methode_1_sans_index.md**
### Comparaison directe sans index (en dehors d'un dépôt Git)
1. **Clonez les deux versions** dans des dossiers distincts :
   ```bash
   git clone https://github.com/hrhouma1/accounts-v2
   git clone https://github.com/hrhouma1/accounts-v3
   ```

2. **Examinez la structure des projets** et comparez les fichiers et dossiers.

3. **Comparer un fichier spécifique** :
   ```bash
   git diff --no-index ./accounts-v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java ./accounts-v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```

4. **Comparer les dossiers avec des exclusions** (par ex. exclure les répertoires de tests) :
   ```bash
   git diff --no-index --exclude=./accounts-v2/src/test/ ./accounts-v2 ./accounts-v3
   ```

---

## 📁 **05_methode_2_depot_local.md**
### Méthode 2 : Comparaison avec dépôt Git local temporaire
1. **Créez un dépôt Git local temporaire** :
   ```bash
   mkdir comparaison
   cd comparaison
   git init
   ```

2. **Copiez les fichiers des deux versions** dans des sous-dossiers (`v2` et `v3`), puis ajoutez-les à Git :
   ```bash
   cp -r ../accounts-v2 v2
   cp -r ../accounts-v3 v3
   git add v2 v3
   git commit -m "Ajout des versions v2 et v3"
   ```

3. **Comparer les différences entre les deux versions** :
   ```bash
   git diff v2 v3
   ```

4. **Utilisation de `diff` pour comparer deux fichiers** :
   ```bash
   diff v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```

---

## 👁️‍🗨️ **06_methode_3_comparaison_visuelle.md**
### Comparaison visuelle avec un IDE :
1. **Utilisation de Visual Studio Code** :
   - Ouvrez les deux fichiers à comparer.
   - Clic droit sur le premier fichier, sélectionnez **"Select for Compare"**.
   - Clic droit sur le deuxième fichier et sélectionnez **"Compare with Selected"**.

2. **Utilisation de IntelliJ IDEA** :
   - Ouvrez les deux fichiers dans l'IDE.
   - Faites un clic droit sur l'un des fichiers et sélectionnez **"Compare with..."**.

---

## 🤖 **07_methode_4_automatisation.md**
### Automatisation via scripts Bash et Python

#### 1. **Automatisation avec un script Bash** :
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

#### 2. **Automatisation avec un script Python** :
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

#### 3. **Script Bash avancé** :
```bash
#!/bin/bash
dir_v2="./accounts-v2"
dir_v3="./accounts-v3"
output_dir="./comparaison_rapports"
files_to_compare=("src/main/java/com/eazybytes/accounts/controller/AccountsController.java" "src/main/resources/application.properties")

mkdir -p $output_dir

for file in "${files_to_compare[@]}"; do
    diff -u --ignore-all-space "$dir_v2/$file" "$dir_v3/$file" > "$output_dir/rapport_diff_$(basename $file).txt"
    echo "Différences enregistrées dans $output_dir/rapport_diff_$(basename $file).txt"
done

echo "Résumé des différences :"
diff -rq "$dir_v2" "$dir_v3"
```

---

## ❓ **08_questions_reflexion.md**
### Questions de réflexion à poser aux étudiants :
1. Quels sont les nouveaux fichiers ou dossiers ajoutés dans la version **v3** ?
2. Y a-t-il des fichiers ou dossiers qui ont été supprimés ou renommés ?
3. Quelles sont les principales modifications de code que vous avez observées ?
4. Y a-t-il des changements dans la configuration du projet ou dans les dépendances ?
5. Selon vous, quel est l’objectif principal des modifications dans la version **v3** ?

---

## 💡 **09_conseils.md**
### Conseils supplémentaires pour les étudiants :
- **Focalisez-vous sur les modifications significatives** plutôt que sur les changements mineurs comme les espaces ou les commentaires.
- **Utilisez des outils graphiques** comme **Meld** ou **Beyond Compare** pour faciliter la comparaison visuelle des fichiers.
- **Lisez la documentation Git** pour mieux comprendre les commandes avancées de comparaison.

---

## 📚 **10_references.md**
### Références utiles :
- [GitHub v2 - Projet Version v2](https://github.com/hrhouma1/accounts-v2)
- [GitHub


