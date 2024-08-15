# Suivre les étapes dans le document suivant (01-projet01-partie01.docx) dans le dossier Documents
- 01-spring-boot-backend/01-Projet 1 - Hello World/Documents
- https://github.com/hrhouma1/WebTransact/blob/main/01-spring-boot-backend/01-Projet%201%20-%20Hello%20World/Documents/01-projet01-partie01.docx

# Veuillez trouver les notes de support ci-bas : 

---

# Projet 01 - « Greeting »
---

## TABLE DES MATIÈRES

1. [Créer et importer le projet](#1---créer-et-importer-le-projet)
   1. [Starter ou Spring Initializr](#11--starter-ou-spring-initializr)
   2. [Ajout des dépendances](#12--ajout-des-dépendances)
   3. [Ouvrir à STS, effectuer un import de type « Maven Projects », et sélection de pom.xml](#13--ouvrir-à-sts-effectuer-un-import-de-type-maven-projects-et-sélection-de-pomxml)
   4. [Créez la classe Greeting.java](#14--créez-la-classe-greetingjava)
   5. [Créez la classe GreetingController.java](#15--créez-la-classe-greetingcontrollerjava)
   6. [Observez et testez](#16--observez-et-testez)
      - [Résolution de problèmes #1](#171--résolution-de-problèmes-1)
      - [Résolution de problèmes #2](#172--résolution-de-problèmes-2)

---

## 1 - Créer et importer le projet

### 1.1- Starter ou Spring Initializr

Pour démarrer le projet, utilisez [Spring Initializr](https://start.spring.io/). Choisissez les dépendances nécessaires et configurez votre projet comme illustré ci-dessous :

![Spring Initializr](file-HgnCesVSgr9iOLaPgCgSc4lQ)

### 1.2. Ajout des dépendances

Ajoutez les dépendances essentielles pour votre projet dans le fichier `pom.xml`. Voici les dépendances recommandées :

![Ajout des dépendances](file-0kSFlMhig9GFBcitAjm4w34C)

- **Spring Web** : Pour créer des applications web RESTful.
- **Lombok** : Pour réduire le code boilerplate.
- **Spring Data JPA** : Pour la persistance des données avec JPA.
- **PostgreSQL Driver** : Pour connecter l'application à une base de données PostgreSQL.

### 1.3. Ouvrir à STS, effectuer un import de type « Maven Projects », et sélection de pom.xml

Une fois le projet généré, déplacez-le dans votre workspace et importez-le dans Spring Tool Suite (STS) comme un projet Maven :

![Ouvrir à STS](file-Wty1bcIaGhAKAr5uN0kMZJpX)

1. Cliquez sur **File > Import**.
2. Sélectionnez **Maven Projects** et importez le fichier `pom.xml` de votre projet.

![Sélection de pom.xml](file-qX6u5pH1o47sf3SRkPerpY2V)

### 1.4. Créez la classe Greeting.java

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

![Créer la classe Greeting.java](file-jmG0ylEvKMc1MPRPYoa9bqu4)

### 1.5. Créez la classe GreetingController.java

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

![Créer la classe GreetingController.java](file-cHJAkNOl40viDWIRKO2fWjqO)

### 1.6. Observez et testez

Après avoir configuré les classes, il est temps de tester votre projet. Exécutez les commandes Maven suivantes pour nettoyer, compiler et lancer l'application :

1. **Maven clean** : Nettoie le projet.
2. **Maven install** : Compile et installe les dépendances nécessaires.
3. **Spring Boot app** : Lance l'application.

Ensuite, saisissez l'URL suivante dans votre navigateur pour tester l'application : [http://localhost:8080/greeting?name=armestrong](http://localhost:8080/greeting?name=armestrong).

![Observez et testez](file-SqkDW3KHTQEeDAjvfActhaT5)

### 1.7. Résolution d’erreurs

#### 1.7.1. Résolution de problèmes #1

Si vous rencontrez une erreur de configuration, vérifiez si vous avez ajouté des dépendances inutilisées. Supprimez-les comme illustré :

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

#### 1.7.2. Résolution de problèmes #2

Si le port 8080 est déjà utilisé, vous pouvez soit changer de port dans `application.properties`, soit tuer le processus en cours.

- **Solution 1** : Changer de port dans `application.properties` ou `application.yml`.
  ```properties
  server.port=8081
  ```

  ```yaml
  server:
    port: 8081
  ```

- **Solution 2** : Tuer le processus utilisant le port 8080.
  ```bash
  netstat -noa | findstr :8080
  taskkill /F /PID pid_number
  ```

![Résolution d’erreurs](file-7m2bZZ1AbFbcgeGFaGyE6vs3)

---

Ce tuto vous guide étape par étape pour créer et configurer un projet Spring Boot simple avec une classe Greeting et un contrôleur, tout en vous aidant à résoudre les erreurs courantes que vous pourriez rencontrer en cours de route. Les images fournissent un support visuel pour chaque étape, rendant le processus plus facile à suivre.




