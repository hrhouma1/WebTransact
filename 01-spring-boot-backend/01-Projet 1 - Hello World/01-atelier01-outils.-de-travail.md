---
# 1 -  Instructions d'utilisation
---

1. **Téléchargement et extraction** :
   - Téléchargez le dossier depuis ce lien : [OUTILSSPRING.zip](https://drive.google.com/drive/folders/1ZzIFS9Zx9uOWDmlngGrG3CBrXJojY4-c?usp=sharing).
   - Utilisez WinRAR (téléchargeable depuis [WinRAR](https://winrar.fr.softonic.com/?ex=RAMP-2125.0)) pour extraire le contenu du fichier `OUTILSSPRING.zip`.
   - **Ne pas utiliser WinZip**, car certains fichiers pourraient ne pas être extraits correctement.

2. **Installation de Java 17** :
   - Bien que Java 8 soit inclus, vous devez installer Java 17. Téléchargez-le depuis le site officiel de Java et suivez les instructions d'installation (**voir 02-atelier02**).

3. **Installation de Maven 3.9.0** :
   - Après avoir extrait le dossier `apache-maven-3.9.0`, ajoutez le chemin du dossier `bin` de Maven à votre variable d'environnement `PATH` (**voir 02-atelier02**).

4. **Configuration de Spring Tool Suite** :
   - Lancez l'IDE Spring Tool Suite en utilisant le dossier extrait ou en installant via le fichier `.zip`. Configurez l'IDE avec votre JDK (Java 17) et commencez à travailler sur vos projets Spring Boot.

- Ces outils sont essentiels pour commencer à développer des applications Spring Boot et suivre les exercices pratiques que vous allez réaliser. 
- Assurez-vous que toutes les configurations sont correctes avant de démarrer vos projets.

---
# Annexe 1 : Description du dossier `OUTILSSPRING.zip`
---

Le dossier `OUTILSSPRING.zip` contient tous les outils nécessaires pour commencer à travailler avec Maven et Spring Boot. Voici les éléments inclus dans le dossier et leur utilisation :

1. **`apache-maven-3.9.0`** :
   - Dossier contenant les fichiers nécessaires pour Maven version 3.9.0. Vous pouvez l'extraire et l'utiliser directement sans installation supplémentaire.

3. **`jdk-8u202-windows-x64.exe`** :
   - Installateur pour Java Development Kit (JDK) version 8. Par contre, nous allons utiliser Java 17.
   - Ce fichier est inclus pour des besoins spécifiques ou pour les environnements où Java 8 est requis.
   - Une démonstration aura lieu en classe pour vous montrer comment changer de version JAVA en modifiant le contenent de JAVA_HOME (le pointer vers java 8 ou jaba 17) et placer %JAVA_HOME%\bin dans la *première position du path*.

4. **`lombok.jar`** :
   - Une bibliothèque Java qui est fréquemment utilisée avec Spring Boot pour réduire la quantité de code boilerplate dans vos projets. Il suffit de l'ajouter à votre projet ou à votre IDE (*démoen classe*).

5. **`postgresql-12.14-1-windows-x64.exe`** :
   - Installateur pour PostgreSQL, une base de données relationnelle utilisée pour vos projets Spring Boot. Utilisez-le pour installer et configurer PostgreSQL sur votre machine.

6. **`spring-tool-suite-4-4.17.2.RELEASE-e4.26.0-win32.win32.x86_64`** :

7. **`spring-tool-suite-4-4.17.2.RELEASE-e4.26.0-win32.win32.x86_64.zip`** :
      - Dossier contenant Spring Tool Suite (STS), un IDE basé sur Eclipse, conçu spécialement pour les développeurs Spring. Il est livré avec des outils et des plugins pour vous aider à développer des applications Spring Boot facilement.
      - Version compressée de Spring Tool Suite 4. Si vous préférez réinstaller ou distribuer l'IDE, vous pouvez utiliser ce fichier.
