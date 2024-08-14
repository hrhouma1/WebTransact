# Installation de Maven 3.9.0 et Java 17 sur Windows

Ce guide explique comment installer Java 17 et Maven 3.9.0 sur un système Windows et configurer les variables d'environnement nécessaires.

----
# 1 - Étape 1: Installation de Java 17
----

1. **Télécharger Java 17 :**
   - Allez sur le site officiel de [Oracle](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html) ou utilisez l'OpenJDK [ici](https://jdk.java.net/17/).
   - Choisissez la version appropriée pour votre système (Windows x64 Installer) et téléchargez le fichier `.exe`.

2. **Installer Java 17 :**
   - Lancez le fichier `.exe` téléchargé et suivez les instructions pour installer Java.
   - Notez le chemin d'installation (par exemple, `C:\Program Files\Java\jdk-17`).

3. **Configurer `JAVA_HOME` :**
   - Ouvrez les Paramètres Système Avancés :
     - Faites un clic droit sur "Ce PC" ou "Ordinateur" sur votre bureau ou dans l'explorateur de fichiers.
     - Sélectionnez "Propriétés".
     - Cliquez sur "Paramètres système avancés" sur la gauche.
     - Cliquez sur "Variables d'environnement..." en bas de la fenêtre.
   - Dans la section "Variables système", cliquez sur "Nouvelle..." pour créer une nouvelle variable.
     - Nom de la variable : `JAVA_HOME`
     - Valeur de la variable : **le chemin vers votre installation de Java** (par exemple, `C:\Program Files\Java\jdk-17`)
   - Cliquez sur "OK" pour sauvegarder.

4. **Ajouter Java au PATH :**
   - Toujours dans la fenêtre "Variables d'environnement", trouvez la variable `Path` dans "Variables système" et sélectionnez-la, puis cliquez sur "Modifier...".
   - Cliquez sur "Nouveau" et ajoutez cette ligne :
     ```plaintext
     %JAVA_HOME%\bin
     ```
   - Cliquez sur "OK" pour sauvegarder.

5. **Vérifier l'installation de Java :**
   - Ouvrez une nouvelle fenêtre de commande (`cmd`) et tapez :
     ```bash
     java -version
     ```
   - Vous devriez voir une sortie indiquant la version Java installée.

---
# 2 - Étape 2: Installation de Maven 3.9.0
---

1. **Télécharger Maven 3.9.0 :**
   - Allez sur le site officiel d'[Apache Maven](https://maven.apache.org/download.cgi) et téléchargez le fichier `apache-maven-3.9.0-bin.zip`.

2. **Extraire l'archive :**
   - Extrayez le fichier `apache-maven-3.9.0-bin.zip` à l'emplacement de votre choix, par exemple `C:\Program Files\Apache\maven-3.9.0`.

3. **Configurer `MAVEN_HOME` :**
   - Dans la fenêtre "Variables d'environnement", créez une nouvelle variable système :
     - Nom de la variable : `MAVEN_HOME`
     - Valeur de la variable : **le chemin vers votre installation de Maven** (par exemple, `C:\Program Files\Apache\maven-3.9.0`)
   - Cliquez sur "OK" pour sauvegarder.

4. **Ajouter Maven au PATH :**
   - Toujours dans la fenêtre "Variables d'environnement", sélectionnez la variable `Path`, puis cliquez sur "Modifier...".
   - Cliquez sur "Nouveau" et ajoutez cette ligne :
     ```plaintext
     %MAVEN_HOME%\bin
     ```
   - Cliquez sur "OK" pour sauvegarder.

5. **Vérifier l'installation de Maven :**
   - Ouvrez une nouvelle fenêtre de commande (`cmd`) et tapez :
     ```bash
     mvn -version
     ```
   - Vous devriez voir une sortie indiquant la version de Maven installée, comme ceci :
     ```
     Apache Maven 3.9.0 (...)
     ```
---
# 3 - Conclusion
---

Vous avez maintenant installé Java 17 et Maven 3.9.0 sur votre machine Windows. Vous pouvez commencer à utiliser Maven pour gérer vos projets Java.
