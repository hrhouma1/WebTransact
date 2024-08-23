# Tutoriel MAVEN & LINUX : Création et Configuration Automatisée d’un Projet Maven sur Ubuntu 22.04

Ce tutoriel vous guidera à travers les étapes nécessaires pour configurer un projet Java avec Maven sur Ubuntu 22.04, incluant l'installation de Java 17 et Maven 3.9.0, ainsi que la création automatique d'un projet Maven avec un script shell.

## Pré-requis

Assurez-vous que vous avez les permissions suffisantes sur votre système pour installer des logiciels et exécuter des scripts.

## 1. Installation de Java 17

Pour commencer, vous devez installer Java 17, qui est requis pour exécuter Maven et compiler votre projet Java.

### Étape 1 : Mise à jour du système

Ouvrez un terminal et exécutez la commande suivante pour mettre à jour les paquets de votre système :

```bash
sudo apt update && sudo apt upgrade -y
```

### Étape 2 : Installation de Java 17

Installez Java 17 avec la commande suivante :

```bash
sudo apt install openjdk-17-jdk -y
```

### Étape 3 : Vérification de l'installation

Vérifiez que Java 17 est bien installé en exécutant :

```bash
java -version
```

La sortie devrait ressembler à ceci :

```
openjdk version "17.0.x" 202x-xx-xx
OpenJDK Runtime Environment (build 17.0.x+x-xx)
OpenJDK 64-Bit Server VM (build 17.0.x+x-xx, mixed mode, sharing)
```

## 2. Installation de Maven 3.9.0

Ensuite, vous devez installer Maven 3.9.0.

### Étape 1 : Téléchargement de Maven

Téléchargez l'archive binaire de Maven 3.9.0 depuis le site officiel :

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
```

### Étape 2 : Extraction de l'archive

Extrayez l'archive téléchargée :

```bash
tar xzf apache-maven-3.9.9-bin.tar.gz
```

### Étape 3 : Déplacement de Maven

Déplacez le répertoire Maven dans `/opt/maven` :

```bash
sudo mv apache-maven-3.9.9 /opt/maven
```

### Étape 4 : Configuration des variables d'environnement

Configurez les variables d'environnement pour Maven en créant un fichier de configuration :

```bash
sudo nano /etc/profile.d/maven.sh
```

Ajoutez les lignes suivantes au fichier :

```bash
export MAVEN_HOME=/opt/maven
export PATH=$MAVEN_HOME/bin:$PATH
```

Enregistrez et fermez le fichier (`Ctrl+O`, `Enter`, puis `Ctrl+X`).

### Étape 5 : Rechargement des variables d'environnement

Rechargez la configuration pour appliquer les changements :

```bash
source /etc/profile.d/maven.sh
```

### Étape 6 : Vérification de l'installation de Maven

Vérifiez que Maven est correctement installé en exécutant :

```bash
mvn -version
```

Vous devriez voir une sortie similaire à ceci :

```
Apache Maven 3.9.0 (xxxxxxx; 202x-xx-xxTxx:xx:xxZ)
Maven home: /opt/maven
Java version: 17.0.x, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-17-openjdk-amd64
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.xx.xx-xx-generic", arch: "amd64", family: "unix"
```

## 3. Automatisation de la création et configuration du projet Maven

Nous allons maintenant créer un script shell pour automatiser la création d’un projet Maven, le renommage des fichiers, et l’exécution des commandes Maven.

### Étape 1 : Création du script shell

Créez un fichier nommé `setup_maven_project.sh` :

```bash
nano setup_maven_project.sh
```

### Étape 2 : Ajout du script

Collez le contenu suivant dans le fichier `setup_maven_project.sh` :

```bash
#!/bin/bash

# Nom du projet et des fichiers
GROUP_ID="com.example"
ARTIFACT_ID="calculator"
ARCHETYPE_ID="maven-archetype-quickstart"
MAIN_CLASS="Calculator"
TEST_CLASS="CalculatorTest"

# Générez le projet Maven
mvn archetype:generate -DgroupId=$GROUP_ID -DartifactId=$ARTIFACT_ID -DarchetypeArtifactId=$ARCHETYPE_ID -DinteractiveMode=false

# Se déplacer dans le répertoire du projet
cd $ARTIFACT_ID

# Renommer les fichiers générés
mv src/main/java/com/example/App.java src/main/java/com/example/$MAIN_CLASS.java
mv src/test/java/com/example/AppTest.java src/test/java/com/example/$TEST_CLASS.java

# Remplacement du contenu dans les fichiers Java
sed -i "s/App/$MAIN_CLASS/g" src/main/java/com/example/$MAIN_CLASS.java
sed -i "s/App/$MAIN_CLASS/g" src/test/java/com/example/$TEST_CLASS.java

# Ajout du code pour Calculator.java
cat > src/main/java/com/example/$MAIN_CLASS.java <<EOL
package com.example;

public class $MAIN_CLASS {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public double divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Division by zero.");
        }
        return (double) a / b;
    }
}
EOL

# Ajout du code pour CalculatorTest.java
cat > src/test/java/com/example/$TEST_CLASS.java <<EOL
package com.example;
import org.junit.Assert;
import org.junit.Test;

public class $TEST_CLASS {
    private $MAIN_CLASS calculator = new $MAIN_CLASS();

    @Test
    public void testAdd() {
        Assert.assertEquals(5, calculator.add(2, 3));
    }

    @Test
    public void testSubtract() {
        Assert.assertEquals(1, calculator.subtract(3, 2));
    }

    @Test
    public void testMultiply() {
        Assert.assertEquals(6, calculator.multiply(2, 3));
    }

    @Test
    public void testDivide() {
        Assert.assertEquals(2.0, calculator.divide(4, 2), 0);
    }

    @Test(expected = IllegalArgumentException.class)
    public void testDivideByZero() {
        calculator.divide(1, 0);
    }
}
EOL

# Mise à jour du fichier pom.xml pour inclure JUnit
sed -i '/<dependencies>/a \
    <dependency>\n\
      <groupId>junit</groupId>\n\
      <artifactId>junit</artifactId>\n\
      <version>4.12</version>\n\
      <scope>test</scope>\n\
    </dependency>' pom.xml

# Exécution des commandes Maven
mvn clean install
mvn site

echo "Le projet Maven $ARTIFACT_ID a été créé et configuré avec succès !"
```

### Étape 3 : Rendre le script exécutable

Rendez le script exécutable en utilisant la commande suivante :

```bash
chmod +x setup_maven_project.sh
```

### Étape 4 : Exécution du script

Exécutez le script pour créer et configurer automatiquement le projet Maven :

```bash
./setup_maven_project.sh
```

### Ce que fait le script :
- **Génère un projet Maven** avec les paramètres spécifiés (`groupId`, `artifactId`, `archetypeId`).
- **Renomme les fichiers générés** (`App.java` et `AppTest.java`) en `Calculator.java` et `CalculatorTest.java`.
- **Remplace les occurrences** de `App` par `Calculator` dans les fichiers Java.
- **Ajoute le code** pour les fichiers `Calculator.java` et `CalculatorTest.java`.
- **Met à jour le fichier `pom.xml`** pour inclure la dépendance JUnit 4.12.
- **Exécute les commandes Maven** pour nettoyer, compiler, tester, installer le projet et générer un site Maven.

### Étape 5 : Vérification des résultats

Après l'exécution du script, vous pouvez vérifier que tout s'est bien passé en inspectant le répertoire du projet et en exécutant les commandes Maven suivantes si nécessaire :

```bash
mvn compile
mvn test
mvn package
```

---

## Conclusion

En suivant ce tutoriel, vous avez non seulement installé Java 17 et Maven 3.9.0 sur Ubuntu 22.04, mais vous avez également automatisé la création et la configuration d'un projet Maven à l'aide d'un script shell. Cela simplifie le processus de mise en place d'un projet Java, vous permettant de vous concentrer davantage sur le développement de votre code.
