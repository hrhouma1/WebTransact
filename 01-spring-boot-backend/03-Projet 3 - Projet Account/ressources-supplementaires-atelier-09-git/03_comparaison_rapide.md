# 🔍 **Comparaison rapide et avancée avec git diff**

# Comparaison rapide des fichiers avec Git Diff :

1. **Comparer tous les fichiers** entre les deux versions :
   ```bash
   git diff --no-index ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Cette commande compare tous les fichiers des répertoires `accounts-v2` et `accounts-v3`. Elle affiche toutes les lignes qui ont été modifiées, ajoutées ou supprimées entre les deux versions.

2. **Comparer uniquement certains types de fichiers** (par exemple les fichiers Java) :
   ```bash
   git diff --no-index ./accounts-v2/*.java ./accounts-v3/*.java
   ```
   - **Explication** : Cette commande se concentre uniquement sur les fichiers Java. Cela permet de limiter la comparaison aux fichiers d'intérêt sans inclure d'autres types de fichiers comme les fichiers de configuration ou les assets.

3. **Comparer des fichiers spécifiques** (ex. `AccountsController.java`) :
   ```bash
   git diff --no-index ./accounts-v2/src/main/java/com/eazybytes/accounts/controller/AccountsController.java ./accounts-v3/src/main/java/com/eazybytes/accounts/controller/AccountsController.java
   ```
   - **Explication** : Si vous souhaitez comparer uniquement un fichier spécifique entre les deux versions, cette commande vous permet de zoomer sur les changements dans un seul fichier sans vous encombrer des modifications dans le reste du projet.

4. **Ignorer les espaces et lignes blanches** lors de la comparaison :
   ```bash
   git diff --no-index --ignore-space-at-eol ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Parfois, les espaces ou les retours à la ligne ne sont pas significatifs pour votre comparaison. Cette option permet d’ignorer ces différences mineures.

---

# Commandes supplémentaires pour une comparaison plus détaillée :

5. **Comparer en ignorant toutes les différences d'espaces** (y compris les espaces au début ou en fin de ligne) :
   ```bash
   git diff --no-index --ignore-all-space ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Cela permet d’ignorer toutes les différences d’espacement entre les fichiers, y compris les tabulations ou les espaces multiples. Très utile si votre équipe n'a pas de règle stricte sur l'espacement.

6. **Comparer en affichant les différences ligne par ligne avec des couleurs** pour une meilleure lisibilité :
   ```bash
   git diff --color ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Cette option affiche les changements avec des couleurs, ce qui est particulièrement utile lorsque vous visualisez de nombreuses différences. Les ajouts, suppressions et modifications sont ainsi plus visibles.

7. **Comparer mot par mot** pour voir les changements spécifiques dans les mots (utile dans les chaînes de texte) :
   ```bash
   git diff --color-words ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Si vous travaillez avec du texte ou des chaînes, cette option permet d’afficher les différences mot par mot plutôt que ligne par ligne. C’est utile pour identifier des modifications précises dans des chaînes ou des commentaires.

8. **Afficher uniquement les noms des fichiers modifiés** entre les deux versions sans afficher les détails :
   ```bash
   git diff --name-only ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Parfois, vous souhaitez simplement connaître les fichiers qui ont été modifiés sans avoir à voir les détails des changements. Cette commande est idéale pour cela.

9. **Afficher les statistiques des modifications** (nombre de lignes ajoutées et supprimées) :
   ```bash
   git diff --stat ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Cette commande génère un résumé statistique des changements, incluant le nombre de lignes ajoutées et supprimées pour chaque fichier. Utile pour avoir une vue d’ensemble rapide des modifications.

10. **Afficher les différences avec du contexte supplémentaire** autour des lignes modifiées :
   ```bash
   git diff -U10 --no-index ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Par défaut, Git affiche 3 lignes de contexte autour des différences. Vous pouvez utiliser cette option pour afficher 10 lignes de contexte, ce qui est utile pour voir le code environnant les modifications sans avoir à ouvrir le fichier complet.

11. **Comparer uniquement les fichiers modifiés ou ajoutés** :
   - Si vous souhaitez ne voir que les fichiers modifiés ou ajoutés entre les deux versions (en ignorant les fichiers supprimés) :
     ```bash
     git diff --diff-filter=AM ./accounts-v2 ./accounts-v3
     ```
   - **Explication** : Cette commande filtre les résultats pour n’afficher que les fichiers qui ont été modifiés (M) ou ajoutés (A). Les fichiers supprimés ou non modifiés ne sont pas affichés.

12. **Comparer uniquement les fichiers supprimés** :
   - Si vous souhaitez voir uniquement les fichiers supprimés entre les deux versions :
     ```bash
     git diff --diff-filter=D ./accounts-v2 ./accounts-v3
     ```
   - **Explication** : Cette option affiche uniquement les fichiers supprimés, ce qui est utile si vous souhaitez vérifier quels fichiers ont été retirés du projet.

13. **Comparer les fichiers en ignorant les permissions ou les modes d'exécution** :
   ```bash
   git diff --ignore-permissions --no-index ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Si les permissions de fichiers (comme les droits d'exécution) ont changé mais pas leur contenu, vous pouvez utiliser cette commande pour ignorer ces différences.

14. **Comparer en ignorant les différences de fin de ligne (EOL)** :
   ```bash
   git diff --ignore-space-at-eol ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Cela permet d'ignorer les changements dans les retours à la ligne (fin de ligne), par exemple si un fichier utilise CRLF sur Windows et LF sur Linux.

15. **Afficher uniquement les lignes modifiées sans le contexte** :
   ```bash
   git diff --no-index --unified=0 ./accounts-v2 ./accounts-v3
   ```
   - **Explication** : Par défaut, Git montre plusieurs lignes de contexte autour des modifications. Cette commande affiche uniquement les lignes modifiées sans les lignes environnantes, utile pour des comparaisons rapides.

