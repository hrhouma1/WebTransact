

### Annexe : Pratique 4 – JENKINS + Maven (2/3)
### Création de la structure du projet - Projet de calculatrice

---

#### Contenu

1. Commandes MAVEN couramment utilisées  
2. Création manuelle du projet  
3. Création automatique du projet - Utilisation de Maven Archetype  

---

### 1. Commandes MAVEN couramment utilisées

Voici un ensemble de commandes Maven couramment utilisées. Ces commandes sont exécutées dans le terminal ou l'invite de commande (cmd) à la racine du projet, où se trouve le fichier `pom.xml`.

- `mvn archetype:generate`
- `mvn compile`
- `mvn test`
- `mvn package`
- `mvn verify`
- `mvn install`
- `mvn deploy`
- `mvn clean`
- `mvn site`
- `mvn dependency:analyze`
- `mvn dependency:update-snapshots`

Créer cette structure de projet pour un projet Maven peut être effectué de deux manières : (1) manuellement ou (2) en utilisant un outil de ligne de commande comme Maven lui-même. Voici comment vous pouvez procéder dans les deux cas :

---

### 2. Création manuelle du projet

Pour créer manuellement la structure de dossiers, vous suivez les étapes dans l'explorateur de fichiers de votre système d'exploitation ou via le terminal/invite de commandes :

1. **Créer la structure de dossiers :**  
   Utilisez des commandes `mkdir` dans le terminal (Linux/macOS) ou l'invite de commandes (Windows) pour créer tous les dossiers nécessaires. Voici comment vous pourriez le faire sur un système Unix-like (Linux/macOS) :
   ```bash
   mkdir -p CalculatorProject/src/main/java/com/example
   mkdir -p CalculatorProject/src/test/java/com/example
   ```

   Sur Windows, vous devez créer chaque dossier un par un via l'explorateur de fichiers ou l'invite de commandes avec `mkdir`.

2. **Créer les fichiers :**  
   Utilisez un éditeur de texte pour créer `Calculator.java` et `CalculatorTest.java` dans leurs dossiers respectifs, puis copiez-collez le code fourni. Créez également le fichier `pom.xml` à la racine du projet (`CalculatorProject/`).

---

### 3. Création automatique du projet - Utilisation de Maven Archetype

Maven propose un moyen plus rapide de générer une structure de projet de base grâce à la commande `archetype:generate`. Cela crée un projet avec une structure de dossier standard, y compris `pom.xml`, et peut même inclure un exemple de classe et de test. Voici comment utiliser cette commande :

1. **Ouvrez votre terminal ou invite de commande.**
2. **Naviguez vers le dossier où vous souhaitez créer votre projet.**
3. **Exécutez la commande Maven Archetype :**

   ```bash
   mvn archetype:generate -DgroupId=com.example -DartifactId=calculator -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

   - `-DgroupId` définit l'identifiant de groupe de votre projet, généralement l'organisation ou l'espace de nommage.
   - `-DartifactId` est le nom de votre projet, qui deviendra aussi le nom du dossier de base.
   - `-DarchetypeArtifactId` spécifie l'archétype Maven à utiliser, `maven-archetype-quickstart` est un archétype de base pour les applications Java.
   - `-DinteractiveMode=false` exécute la commande sans mode interactif pour éviter les invites de confirmation supplémentaires.

Après l'exécution, Maven créera un projet dans un dossier appelé `calculator` avec la structure souhaitée. Vous devrez peut-être ajuster les noms des packages et les contenus des fichiers `Calculator.java` et `CalculatorTest.java` pour correspondre à ceux fournis précédemment.

L'utilisation de l'archétype Maven est la manière la plus rapide et la plus conforme aux standards pour générer la structure d'un projet Java. Cela vous permet non seulement de gagner du temps mais aussi d'assurer que la structure du projet suit les conventions Maven, facilitant la maintenance et la compréhension pour les nouveaux développeurs.

---

### Pratique 3 – JENKINS + Maven (1/3)
### Introduction à MAVEN - Projet de calculatrice

---

#### Contenu

1. Compiler le projet  
2. Exécuter les tests unitaires  
3. Construire le projet  
4. Nettoyer le projet  
5. Installer le projet dans le référentiel local Maven  
6. Générer un site pour le projet  
7. Explication de MAVEN  
8. Structure du projet  
9. Calculator.java  
10. CalculatorTest.java

  
11. pom.xml  
12. Exécution des commandes Maven  

---

### 1. Compiler le projet

```bash
mvn compile
```
Cette commande compile le code source du projet (`src/main/java`) et place les fichiers `.class` générés dans le dossier `target/classes`.

---

### 2. Exécuter les tests unitaires

```bash
mvn test
```
Lance les tests unitaires définis dans `src/test/java` en utilisant le framework de test spécifié dans le `pom.xml` (par exemple, JUnit). Les résultats des tests sont affichés dans la console.

---

### 3. Construire le projet

```bash
mvn package
```
Compile le code source, exécute les tests unitaires, et si les tests réussissent, package le code compilé dans un format distribuable, comme un fichier JAR, dans le dossier `target`.

---

### 4. Nettoyer le projet

```bash
mvn clean
```
Supprime le dossier `target`, nettoyant ainsi le projet de tous les fichiers générés lors des précédentes commandes Maven.

---

### 5. Installer le projet dans le référentiel local Maven

```bash
mvn install
```
Compile le projet, exécute les tests, package le projet (comme avec `mvn package`), et copie le package dans le référentiel local Maven. Cela permet de réutiliser le projet comme dépendance dans d'autres projets Maven localement.

---

### 6. Générer un site pour le projet

```bash
mvn site
```
Génère un site web pour votre projet contenant des informations utiles comme la documentation de l'API JavaDoc, les rapports de couverture des tests, l'analyse de la qualité du code, etc.

---

### 7. Explication de MAVEN

Maven est un outil d'automatisation de build pour les projets Java (et autres langages JVM) qui gère les dépendances, la compilation, les tests, le packaging, et le déploiement d'une manière standardisée. Le fichier `pom.xml` (Project Object Model) au cœur de chaque projet Maven décrit tout ce qui concerne le projet (configuration, dépendances, plugins, objectifs, etc.), permettant à Maven de gérer le cycle de vie du build du projet. Maven aide à standardiser et à simplifier le processus de build en fournissant une structure de projet et un modèle de configuration communs, facilitant ainsi le développement et la collaboration entre équipes.

---

### 8. Structure du projet

Notre projet Maven devra suivre cette structure de répertoires :

```
CalculatorProject/
|-- pom.xml
-- src/
    |-- main/
    |   -- java/
    |       -- com/
    |           -- example/
    |               -- Calculator.java
    -- test/
        -- java/
            -- com/
                -- example/
                    -- CalculatorTest.java
```

---

### 9. Calculator.java

Créez le fichier `Calculator.java` dans le répertoire `src/main/java/com/example/` :

```java
package com.example;

public class Calculator {
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
```

---

### 10. CalculatorTest.java

Créez le fichier `CalculatorTest.java` dans le répertoire `src/test/java/com/example/` :

```java
package com.example;
import org.junit.Assert;
import org.junit.Test;

public class CalculatorTest {
    private Calculator calculator = new Calculator();

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
```

---

### 11. pom.xml

Fichier `pom.xml` qui configure notre projet pour utiliser JUnit 4.12 pour les tests :

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://www.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>calculator</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- JUnit dependency -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

---

### 12. Exécution des commandes Maven

Vous pouvez exécuter les commandes Maven mentionnées précédemment dans le terminal ou CMD à la racine du projet (`CalculatorProject`), là où se trouve le fichier `pom.xml`.

- Compiler le projet : `mvn compile`
- Exécuter les tests unitaires : `mvn test`
- Construire le projet (incluant les tests) : `mvn package`
- Nettoyer le projet : `mvn clean`
- Installer le projet dans le référentiel local Maven : `mvn install`
- Générer un site pour le projet : `mvn site`

---

Cela conclut le document avec l'annexe incluse pour couvrir les aspects importants du projet Maven ainsi que l'intégration avec Jenkins.
