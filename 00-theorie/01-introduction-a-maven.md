### Introduction à Maven

---

#### 1. Qu'est-ce que Maven ?

Maven est un outil d'automatisation de build principalement utilisé pour les projets Java, mais il peut également être utilisé avec d'autres langages. Il simplifie le processus de build, la gestion des dépendances, et la gestion du cycle de vie des projets en fournissant une méthode standard pour décrire un projet, ses dépendances, et les étapes de build. Pour quelqu'un qui connaît Java mais qui est nouveau avec Maven, pensez à Maven comme un outil qui automatise la compilation de votre code Java, son empaquetage dans un fichier JAR, la gestion des bibliothèques tierces, et bien plus encore—tout cela avec seulement quelques commandes.

---

#### 2. Pourquoi avons-nous besoin de Maven ?

Lorsque vous travaillez sur des projets Java, en particulier des projets de grande envergure, la gestion des dépendances, la garantie de builds cohérents entre différents environnements, et la gestion de structures de projets complexes peuvent devenir des défis importants. Maven répond à ces défis en offrant :

- **Structure de projet standardisée :** Tous les projets Maven suivent une structure de répertoires standardisée.
- **Gestion des dépendances :** Télécharge automatiquement et gère les bibliothèques et plugins dont votre projet dépend à partir d'un dépôt central comme Maven Central.
- **Cycle de vie du build :** Simplifie le processus de compilation, de test, d'empaquetage et de déploiement de votre application.
- **Reproductibilité :** Assure que les builds sont cohérents dans différents environnements, grâce à la gestion centralisée des dépendances.

---

### Comprendre le cycle de vie Maven

(FIGURE 1 : Cycle de vie d'un livrable Maven)

Le cycle de vie d'un projet Maven peut être compris à travers les phases clés suivantes :

1. **Compile :** Convertit le code source en bytecode, placé dans le répertoire `target`.
2. **Test :** Exécute les tests unitaires, assurant que votre code se comporte comme prévu.
3. **Package :** Regroupe le code compilé dans un format distribuable, tel qu'un fichier JAR ou WAR.
4. **Install :** Installe le package dans le dépôt local, le rendant disponible pour d'autres projets.
5. **Deploy :** Déploie le package dans un dépôt distant pour le partager entre plusieurs développeurs ou projets.

Les phases du cycle de vie de Maven vous permettent d'automatiser l'ensemble du processus de build, de la compilation au déploiement, assurant ainsi la cohérence et réduisant les erreurs manuelles.

---

### Structure d'un projet Maven

(FIGURE 2 : Structure d'un livrable Maven)

Chaque projet Maven possède une structure spécifique, qui inclut :

- **POM.xml (Project Object Model) :** Le cœur du projet Maven, ce fichier XML décrit le projet, ses dépendances, et ses plugins. Il définit également divers détails de configuration et les instructions de build.
- **Dépendances :** Les bibliothèques externes dont votre projet dépend, telles que les frameworks de logging ou les outils de test.
- **GroupID :** Identifie de manière unique votre projet au sein d'une organisation (par exemple, `com.example`).
- **ArtifactID :** Le nom de votre projet (par exemple, `calculator`).
- **VersionID :** La version de votre projet (par exemple, `1.0-SNAPSHOT`).

---

### 8. Structure du projet

Notre projet Maven devra suivre cette structure de répertoires :

```plaintext
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
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
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

- **Compiler le projet :** `mvn compile`
- **Exécuter les tests unitaires :** `mvn test`
- **Construire le projet (incluant les tests) :** `mvn package`
- **Nettoyer le projet :** `mvn clean`
- **Installer le projet dans le référentiel local Maven :** `mvn install`
- **Générer un site pour le projet :** `mvn site`

---

### Conclusion

En suivant le cycle de vie Maven, en comprenant la structure du projet, et en utilisant les commandes Maven courantes, vous pouvez gérer vos projets Java de manière plus efficace. Maven ne simplifie pas seulement le processus de build, mais impose également des bonnes pratiques et une standardisation, facilitant ainsi la collaboration au sein des équipes sur des projets complexes.

---

Cette version est maintenant complète et prête à être intégrée dans votre README, avec les sections de code ajoutées pour vous permettre de créer un projet Maven fonctionnel. Vous pouvez également insérer les figures (FIGURE 1 et FIGURE 2) dans les sections appropriées comme indiqué.
