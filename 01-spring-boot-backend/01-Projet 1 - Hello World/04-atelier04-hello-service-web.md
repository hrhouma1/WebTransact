# 🛠️ **Méthode 01 - Suivre les étapes dans le document suivant :**  
📄 **01-projet01-partie01.docx** dans le dossier **Documents**

- 📂 **01-spring-boot-backend/01-Projet 1 - Hello World/Documents**
- 🌐 [Lien GitHub vers le document](https://github.com/hrhouma1/WebTransact/blob/main/01-spring-boot-backend/01-Projet%201%20-%20Hello%20World/Documents/01-projet01-partie01.docx)

---

# 📑 **Méthode 02 - Notes de support** 
Veuillez trouver les notes de support ci-dessous. 👇

---

# 🌟 **Projet 01 - « Greeting »** 🌟

## 🗂️ **TABLE DES MATIÈRES**

1. [Créer et importer le projet](#1---créer-et-importer-le-projet)
   1. [Starter ou Spring Initializr](#11--starter-ou-spring-initializr)
   2. [Ajout des dépendances](#12--ajout-des-dépendances)
   3. [Ouvrir dans VSCode, effectuer un import de type « Maven Projects », et sélection de pom.xml](#13--ouvrir-dans-vscode-effectuer-un-import-de-type-maven-projects-et-sélection-de-pomxml)
   4. [Créez la classe Greeting.java](#14--créez-la-classe-greetingjava)
   5. [Créez la classe GreetingController.java](#15--créez-la-classe-greetingcontrollerjava)
   6. [Observez et testez](#16--observez-et-testez)
      - [Résolution de problèmes #1](#171--résolution-de-problèmes-1)
      - [Résolution de problèmes #2](#172--résolution-de-problèmes-2)

---

## 1️⃣ **Créer et importer le projet**

### 1.1️⃣ - Starter ou Spring Initializr

Pour démarrer le projet, utilisez [Spring Initializr](https://start.spring.io/). Choisissez les dépendances nécessaires et configurez votre projet comme illustré ci-dessous.

### 1.2️⃣ - Ajout des dépendances

Ajoutez les dépendances essentielles pour votre projet dans le fichier `pom.xml`. Voici les dépendances recommandées :

- **Spring Web** 🌐 : Pour créer des applications web RESTful.
- **Lombok** ✂️ : Pour réduire le code boilerplate.
- **Spring Data JPA** 📦 : Pour la persistance des données avec JPA.
- **PostgreSQL Driver** 🛢️ : Pour connecter l'application à une base de données PostgreSQL.

### 1.3️⃣ - Ouvrir dans VSCode, effectuer un import de type « Maven Projects », et sélection de pom.xml

Une fois le projet généré, déplacez-le dans votre espace de travail et ouvrez-le dans Visual Studio Code (VSCode) :

1. Ouvrez VSCode et accédez à **File > Open Folder** pour ouvrir votre projet.
2. Assurez-vous d'avoir l'extension **Maven for Java** installée dans VSCode pour gérer les projets Maven.
3. Dans l'explorateur de projets, cliquez avec le bouton droit sur le fichier `pom.xml` et sélectionnez **Maven > Update Project** pour télécharger les dépendances.

### 1.4️⃣ - Créez la classe **Greeting.java**

Créez une classe `Greeting.java` pour gérer les données de salutation. Voici un exemple de code pour cette classe :

```java
package com.example.demo;

public class Greeting {

    private Long id;
    private String content;

    public Greeting(Long id, String content) {
        this.id = id;
        this.content = content;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

### 1.5️⃣ - Créez la classe **GreetingController.java**

Ensuite, créez un contrôleur pour gérer les requêtes HTTP. Voici un exemple pour `GreetingController.java` :

```java
package com.example.demo;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @GetMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
}
```

### 1.6️⃣ - **Observez et testez** 🧪

Après avoir configuré les classes, il est temps de tester votre projet. Utilisez les commandes Maven suivantes dans le terminal intégré de VSCode pour nettoyer, compiler et lancer l'application :

1. **Maven clean** 🧹 : Nettoie le projet.
2. **Maven install** 📦 : Compile et installe les dépendances nécessaires.
3. **Spring Boot app** 🚀 : Lance l'application.

```java
mvn clean
mvn install ==> erreur à cause des tests unitaires
mvn install -DskipTests
mvn spring-boot:run  ==> erreur à cause des dépendances non utilisés
```



### 1.7️⃣ - **Résolution d’erreurs** 🛠️

#### 1.7.1️⃣ - Résolution de problèmes #1

Si vous rencontrez une erreur de configuration, vérifiez si vous avez ajouté des dépendances inutilisées. Supprimez-les comme illustré :

# Dépendances à supprimer
```xml
<!-- Dépendances à supprimer -->
<dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <optional>true</optional>
</dependency>

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
   <groupId>org.postgresql</groupId>
   <artifactId>postgresql</artifactId>
   <scope>runtime</scope>
</dependency>
```



# Dépendances à garder


```xml
<!-- Dépendances à supprimer -->
<dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <optional>true</optional>
</dependency>

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
   <groupId>org.postgresql</groupId>
   <artifactId>postgresql</artifactId>
   <scope>runtime</scope>
</dependency>
```

```java
mvn clean
mvn install -DskipTests
mvn spring-boot:run 
```

Ensuite, saisissez l'URL suivante dans votre navigateur pour tester l'application : [http://localhost:8080/greeting?name=armestrong](http://localhost:8080/greeting?name=armestrong).


#### 1.7.2️⃣ - Résolution de problèmes #2

Si le port 8080 est déjà utilisé, vous pouvez soit changer de port dans `application.properties`, soit tuer le processus en cours.

- **Solution 1** 🔄 : Changer de port dans `application.properties` ou `application.yml`.
  ```properties
  server.port=8081
  ```

  ```yaml
  server:
    port: 8081
  ```

- **Solution 2** 💻 : Tuer le processus utilisant le port 8080.
  ```bash
  netstat -noa | findstr :8080
  taskkill /F /PID pid_number
  ```

---

🎯 Ce tutoriel vous guide étape par étape pour créer et configurer un projet Spring Boot simple avec une classe Greeting et un contrôleur, tout en vous aidant à résoudre les erreurs courantes que vous pourriez rencontrer en cours de route. Les images fournissent un support visuel pour chaque étape, rendant le processus plus facile à suivre. 📸

# ==> Étape suivante : Ajout de la persistance et de la base de données PostgreSQL


# Exercice : 
- Expliquez l'annotation @SpringBootApplication dans la classe principale.
  
```yaml
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```
