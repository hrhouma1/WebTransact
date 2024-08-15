# Introduction à Maven

---

# 1. Qu'est-ce que Maven ?

---


Maven est un outil d'automatisation de build principalement utilisé pour les projets Java, mais il peut également être utilisé avec d'autres langages. Il simplifie le processus de build, la gestion des dépendances, et la gestion du cycle de vie des projets en fournissant une méthode standard pour décrire un projet, ses dépendances, et les étapes de build. Pour quelqu'un qui connaît Java mais qui est nouveau avec Maven, pensez à Maven comme un outil qui automatise la compilation de votre code Java, son empaquetage dans un fichier JAR, la gestion des bibliothèques tierces, et bien plus encore—tout cela avec seulement quelques commandes.

---

# 2. Pourquoi avons-nous besoin de Maven ?

---


Lorsque vous travaillez sur des projets Java, en particulier des projets de grande envergure, la gestion des dépendances, la garantie de builds cohérents entre différents environnements, et la gestion de structures de projets complexes peuvent devenir des défis importants. Maven répond à ces défis en offrant :

- **Structure de projet standardisée :** Tous les projets Maven suivent une structure de répertoires standardisée.
- **Gestion des dépendances :** Télécharge automatiquement et gère les bibliothèques et plugins dont votre projet dépend à partir d'un dépôt central comme Maven Central.
- **Cycle de vie du build :** Simplifie le processus de compilation, de test, d'empaquetage et de déploiement de votre application.
- **Reproductibilité :** Assure que les builds sont cohérents dans différents environnements, grâce à la gestion centralisée des dépendances.

---

# 3. Comprendre le cycle de vie Maven

---


![image](https://github.com/user-attachments/assets/59a966be-07e8-4cc8-9946-e3702cfe2072)

(FIGURE 1 : Cycle de vie d'un livrable Maven)

Le cycle de vie d'un projet Maven peut être compris à travers les phases clés suivantes :

1. **Compile :** Convertit le code source en bytecode, placé dans le répertoire `target`.
2. **Test :** Exécute les tests unitaires, assurant que votre code se comporte comme prévu.
3. **Package :** Regroupe le code compilé dans un format distribuable, tel qu'un fichier JAR ou WAR.
4. **Install :** Installe le package dans le dépôt local, le rendant disponible pour d'autres projets.
5. **Deploy :** Déploie le package dans un dépôt distant pour le partager entre plusieurs développeurs ou projets.

Les phases du cycle de vie de Maven vous permettent d'automatiser l'ensemble du processus de build, de la compilation au déploiement, assurant ainsi la cohérence et réduisant les erreurs manuelles.

---

# 4. Structure d'un projet Maven

---


![image](https://github.com/user-attachments/assets/db695659-6a0b-4533-b126-e04214ddb0f4)

(FIGURE 2 : Structure d'un livrable Maven)

Chaque projet Maven possède une structure spécifique, qui inclut :

- **POM.xml (Project Object Model) :** Le cœur du projet Maven, ce fichier XML décrit le projet, ses dépendances, et ses plugins. Il définit également divers détails de configuration et les instructions de build.
- **Dépendances :** Les bibliothèques externes dont votre projet dépend, telles que les frameworks de logging ou les outils de test.
- **GroupID :** Identifie de manière unique votre projet au sein d'une organisation (par exemple, `com.example`).
- **ArtifactID :** Le nom de votre projet (par exemple, `calculator`).
- **VersionID :** La version de votre projet (par exemple, `1.0-SNAPSHOT`).

---

# 5. Structure du projet

---

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

### 5.1. Commandes Maven couramment utilisées

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
- **`mkdir`** (Pour créer la structure de répertoires)

Créer cette structure de projet pour un projet Maven peut être effectué de deux manières : (1) manuellement ou (2) en utilisant un outil de ligne de commande comme Maven lui-même. Voici comment vous pouvez procéder dans les deux cas :

---

### 5.2. Création manuelle du projet

Pour créer manuellement la structure de dossiers, vous suivez les étapes dans l'explorateur de fichiers de votre système d'exploitation ou via le terminal/invite de commandes :

1. **Créer la structure de dossiers :**  
   Utilisez des commandes `mkdir` dans le terminal (Linux/macOS) ou l'invite de commandes (Windows) pour créer tous les dossiers nécessaires. Voici comment vous pourriez le faire sur un système Unix-like (Linux/macOS) :

   ```bash
   mkdir -p CalculatorProject/src/main/java/com/example
   mkdir -p CalculatorProject/src/test/java/com/example
   ```

   Sur Windows, vous devriez créer chaque dossier un par un via l'explorateur de fichiers ou l'invite de commandes avec `mkdir`.

2. **Créer les fichiers :**  
   Utilisez un éditeur de texte pour créer `Calculator.java` et `CalculatorTest.java` dans leurs dossiers respectifs, puis copiez-collez le code fourni. Créez également le fichier `pom.xml` à la racine du projet (`CalculatorProject/`).


------

### 5.3. Création automatique du projet

---

**Générez un projet Maven** en utilisant la commande suivante :

   ```bash
   mvn archetype:generate -DgroupId=com.example -DartifactId=calculator -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   cd calculator
   ```

**Ouvrez le projet dans VS Code** :

   ```bash
   code .
   ```

**Renommer les fichiers App.java et AppTest.java**
**Renommez les fichiers** suivants :
   - `App.java` → `Calculator.java`
   - `AppTest.java` → `CalculatorTest.java`


------

# 6. Calculator.java

Assurez vous d'avoir crée le fichier `Calculator.java` dans le répertoire `src/main/java/com/example/` :

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

# 7. CalculatorTest.java

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

# 8. pom.xml

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

# 9. Exécution des commandes Maven

Vous pouvez exécuter les commandes Maven mentionnées précédemment dans le terminal ou CMD à la racine du projet (`CalculatorProject`), là où se trouve le fichier `pom.xml`.

- **Compiler le projet :** `mvn compile`
- **Exécuter les tests unitaires :** `mvn test`
- **Construire le projet (incluant les tests) :** `mvn package`
- **Nettoyer le projet :** `mvn clean`
- **Installer le projet dans le référentiel local Maven :** `mvn install`
- **Générer un site pour le projet :** `mvn site`



---

# 10. Combinaison de commandes Maven

Dans les projets réels, il est courant de combiner plusieurs commandes Maven pour automatiser plusieurs étapes du cycle de vie du build en une seule commande. Par exemple, vous pouvez vouloir nettoyer le projet, compiler le code, exécuter les tests, et installer le package dans le dépôt local, le tout en une seule commande. Voici comment vous pouvez le faire :

#### Combinaison de commandes Maven

```bash
mvn clean install
```

Cette commande exécute les actions suivantes :

1. **`mvn clean`** : Supprime le répertoire `target`, nettoyant ainsi tous les fichiers générés lors des builds précédents.
2. **`mvn install`** : Compile le projet, exécute les tests unitaires, package le projet, puis l'installe dans le dépôt local Maven.

L'avantage de combiner les commandes est de pouvoir effectuer plusieurs tâches consécutives sans avoir à exécuter chaque commande individuellement, ce qui est non seulement un gain de temps, mais assure également que toutes les étapes nécessaires sont exécutées de manière cohérente.

Vous pouvez également combiner d'autres commandes selon vos besoins. Par exemple :

```bash
mvn clean compile package
```

Cela nettoie le projet, compile le code, et package le code compilé en un fichier JAR ou WAR.

Cette flexibilité de Maven vous permet d'adapter le processus de build à vos besoins spécifiques, tout en maintenant la simplicité et l'efficacité dans le développement de projets Java.

---

# Conclusion

En suivant le cycle de vie Maven, en comprenant la structure du projet, et en utilisant les commandes Maven courantes, vous pouvez gérer vos projets Java de manière plus efficace. Maven ne simplifie pas seulement le processus de build, mais impose également des bonnes pratiques et une standardisation, facilitant ainsi la collaboration au sein des équipes sur des projets complexes.


