# 🌟 **Projet 01 (suite de l'atelier 04) - Ajout de la base de données PostgreSQL avec Jakarta Persistence** 🌟

## 🗂️ **TABLE DES MATIÈRES**

1. [Rappel rapide](#1-rappel-rapide)
2. [Ajout de la base de données](#2-ajout-de-la-base-de-données)
   1. [(A) Les dépendances dans POM.XML](#21-a-les-dépendances-dans-pomxml)
   2. [(B) Modification du fichier application.properties](#22-b-modification-du-fichier-applicationproperties)
   3. [(C) Annotation du modèle ou du bean Greeting.java](#23-c-annotation-du-modèle-ou-du-bean-greetingjava)
   4. [(D) S’assurer que vous avez les getters et les setters et les constructeurs dans Greeting.java](#24-d-sassurer-que-vous-avez-les-getters-et-les-setters-et-les-constructeurs-dans-greetingjava)
   5. [(E) Création de la base de données haythem dans PostgreSQL avec les bons privilèges](#25-e-création-de-la-base-de-données-haythem-dans-postgresql-avec-les-bons-privilèges)
3. [Tester avec l'ORM et PostgreSQL](#3-tester-avec-lorm-et-postgresql)
4. [Exercice 1 : Refaire le projet avec Javax Persistence](#4-exercice-1-refaire-le-projet-avec-javax-persistence)
5. [Exercice 2 : Configuration avec application.yml](#5-exercice-2-configuration-avec-applicationyml)
6. [Exercice 3 : Supprimer les getters et setters avec Lombok](#6-exercice-3-supprimer-les-getters-et-setters-avec-lombok)
7. [Exercice 4 : Recréer la base de données automatiquement](#7-exercice-4-recréer-la-base-de-données-automatiquement)

---

## 1️⃣ **Rappel rapide**

### 🎯 **Objectifs**

1. **Requêter les données avec SQL dans une base de données réelle** : Utiliser PostgreSQL ou MySQL.
2. **Ajouter Lombok** : Simplifier le code en réduisant les répétitions.
3. **Requêter les données avec SQL en mémoire** : Utiliser H2, une base de données en mémoire.

---

## 2️⃣ **Ajout de la base de données**

### 2.1 (A) 📄 **Les dépendances dans POM.XML**

Pour ajouter le support de la base de données PostgreSQL et l'API de persistance JPA, nous allons utiliser Jakarta Persistence. Ajoutez les dépendances suivantes dans votre `pom.xml` :

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2.2 (B) 🛠️ **Modification du fichier application.properties**

Configurez votre application pour utiliser PostgreSQL en modifiant le fichier `application.properties` comme suit :

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/haythem?useSSL=false
spring.datasource.username=hrgres
spring.datasource.password=hrgres
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=create
```

### 2.3 (C) ✍️ **Annotation du modèle ou du bean Greeting.java**

Assurez-vous que votre classe `Greeting.java` est correctement annotée pour être gérée par Jakarta Persistence (JPA). Voici le code complet incluant les getters et setters :

```java
package com.example.demo;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "greeting")
public class Greeting {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "content", nullable = false)
    private String content;

    // Constructeur
    public Greeting(Long id, String content) {
        this.id = id;
        this.content = content;
    }

    // Getter pour l'ID
    public Long getId() {
        return id;
    }

    // Setter pour l'ID
    public void setId(Long id) {
        this.id = id;
    }

    // Getter pour le contenu
    public String getContent() {
        return content;
    }

    // Setter pour le contenu
    public void setContent(String content) {
        this.content = content;
    }
}
```

### 2.4 (D) ✔️ **S’assurer que vous avez les getters et les setters et les constructeurs dans Greeting.java**

Vérifiez que la classe `Greeting.java` contient bien les getters, setters et constructeurs nécessaires pour respecter les exigences de Spring Data.

### 2.5 (E) 🏗️ **Création de la base de données `haythem` dans PostgreSQL avec les bons privilèges**

**Important :** À ce stade, vous devez créer la base de données `haythem` dans PostgreSQL. Pour ce faire, suivez les étapes ci-dessous :

1. **Créer un rôle utilisateur** : Accédez à "Login/Group Roles" et créez un nouveau rôle `hrgres` avec les privilèges appropriés (*voir la figure ci-bas*).
2. **Configurer les privilèges** : Assurez-vous que le rôle dispose des privilèges nécessaires comme la possibilité de créer des bases de données.
![image](https://github.com/user-attachments/assets/c6539777-5fca-4366-ab00-6fe2a38749b5)
3. **Créer la base de données** : Créez une nouvelle base de données appelée `haythem` et attribuez-la à l'utilisateur `hrgres`.
![image](https://github.com/user-attachments/assets/26e1c3dc-675b-4324-ae5d-ea4cd00a0305)



---

## 3️⃣ **Tester avec l'ORM et PostgreSQL** 🛢️

### 3.1️⃣ - **Configurer le fichier `application.properties`** 🛠️

Pour utiliser PostgreSQL comme base de données avec Spring Data JPA, assurez-vous que votre fichier `application.properties` est configuré comme suit :

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/haythem?useSSL=false
spring.datasource.username=hrgres
spring.datasource.password=hrgres
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
```

### 3.2️⃣ - **Vérifier les annotations JPA** ✔️

Assurez-vous que votre classe `Greeting.java` est correctement annotée pour être gérée par JPA :

```java
package com.example.demo;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "greeting")
public class Greeting {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "content", nullable = false)
    private String content;

    public Greeting() {}

    public Greeting(Long id, String content) {
        this.id = id;
        this.content = content;
    }

    // Getter pour l'ID
    public Long getId() {
        return id;
    }

    // Setter pour l'ID
    public void setId(Long id) {
        this.id = id;
    }

    // Getter pour le contenu
    public String getContent() {
        return content;
    }

    // Setter pour le contenu
    public void setContent(String content) {
        this.content = content;
    }
}
```

### 3.3️⃣ - **Tester l'intégration avec PostgreSQL** 🧪

Après avoir configuré le fichier `application.properties` et annoté correctement la classe `Greeting.java`, lancez l'application Spring Boot. Ensuite, vous pouvez tester l'intégration avec PostgreSQL en utilisant les endpoints HTTP.

**Étapes pour tester l'intégration :**

1. **Lancer les commandes Maven** : 
   - Effectuez un **Maven clean** pour nettoyer le projet.
   - Suivi d'un **Maven install** pour compiler et installer les dépendances.
   - Enfin, lancez l'application avec **Spring Boot App**.


 ![image](https://github.com/user-attachments/assets/5d3ddf50-6f3b-4ce1-a1c8-c36e1d9b55d3)


2. **Accéder à l'URL suivante pour tester le endpoint** :

   [http://localhost:8080/greeting?name=SpringUser](http://localhost:8080/greeting?name=SpringUser)

3. **Vérifier la table dans PostgreSQL** :

   Après avoir effectué des requêtes via le navigateur, accédez à votre base de données PostgreSQL pour

 vérifier que les données sont bien enregistrées dans la table `greeting`.

   - Ouvrez votre outil de gestion de base de données PostgreSQL.
   - Naviguez vers la base de données `haythem` et sélectionnez la table `greeting` sous le schéma `public`.
   - Rafraîchissez la vue pour voir les nouvelles entrées dans la table `greeting` comme illustré dans l'image ci-dessous.

![image](https://github.com/user-attachments/assets/a5957ca0-3a93-4b33-948b-80681f463311)
![image](https://github.com/user-attachments/assets/f940fc50-b255-4ccd-a04a-b31ef8dbe693)



   - Vous pouvez exécuter la requête SQL suivante pour voir les données insérées :

   ```sql
   SELECT * FROM greeting;
   ```

   - Cette requête affichera toutes les entrées dans la table `greeting`, confirmant ainsi que les données envoyées via le navigateur ont bien été persistées dans la base de données.

---

## 4️⃣ **Exercice 1 : Refaire le projet avec Javax Persistence**

### 📝 **Enoncé**

Refaites le projet en utilisant Javax Persistence au lieu de Jakarta Persistence.

**Étapes :**
1. Modifiez les dépendances dans le fichier `pom.xml` pour utiliser Javax Persistence.
2. Mettez à jour les imports dans la classe `Greeting.java` pour utiliser `javax.persistence.*`.
3. Vérifiez que la classe `Greeting.java` contient les mêmes annotations et méthodes que dans le projet avec Jakarta.

### ✅ **Correction**

1. **Dépendances dans `pom.xml` :**

   ```xml
   <dependency>
       <groupId>org.postgresql</groupId>
       <artifactId>postgresql</artifactId>
       <scope>runtime</scope>
   </dependency>

   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-jpa</artifactId>
   </dependency>

   <dependency>
       <groupId>javax.persistence</groupId>
       <artifactId>javax.persistence-api</artifactId>
       <version>2.2</version>
   ```

2. **Classe `Greeting.java` avec Javax Persistence :**

   ```java
   package com.example.demo;

   import javax.persistence.Column;
   import javax.persistence.Entity;
   import javax.persistence.GeneratedValue;
   import javax.persistence.GenerationType;
   import javax.persistence.Id;
   import javax.persistence.Table;

   @Entity
   @Table(name = "greeting")
   public class Greeting {

       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;

       @Column(name = "content", nullable = false)
       private String content;

       public Greeting() {}

       public Greeting(Long id, String content) {
           this.id = id;
           this.content = content;
       }

       // Getter pour l'ID
       public Long getId() {
           return id;
       }

       // Setter pour l'ID
       public void setId(Long id) {
           this.id = id;
       }

       // Getter pour le contenu
       public String getContent() {
           return content;
       }

       // Setter pour le contenu
       public void setContent(String content) {
           this.content = content;
       }
   }
   ```

---

## 5️⃣ **Exercice 2 : Configuration avec application.yml**

### 📝 **Enoncé**

Configurez votre application pour utiliser PostgreSQL en utilisant un fichier `application.yml` au lieu d'un fichier `application.properties`.

**Étapes :**
1. Convertissez les propriétés du fichier `application.properties` en format YAML.
2. Remplacez le fichier `application.properties` par `application.yml` et testez votre application.

### ✅ **Correction**

1. **Contenu de `application.yml` :**

   ```yaml
   spring:
     datasource:
       url: jdbc:postgresql://localhost:5432/haythem?useSSL=false
       username: hrgres
       password: hrgres
     jpa:
       properties:
         hibernate:
           jdbc.lob.non_contextual_creation: true
           dialect: org.hibernate.dialect.PostgreSQLDialect
       hibernate:
         ddl-auto: create
   ```

---

## 6️⃣ **Exercice 3 : Supprimer les getters et setters avec Lombok**

### 📝 **Enoncé**

Supprimez les getters et setters manuels dans la classe `Greeting.java` et utilisez Lombok pour les générer automatiquement.

**Étapes :**
1. Supprimez les méthodes `getId()`, `setId()`, `getContent()`, et `setContent()` dans `Greeting.java`.
2. Ajoutez l'annotation `@Data` de Lombok en haut de la classe.
3. Recompilez et redémarrez votre application.
4. Vérifiez dans PostgreSQL si la table `greeting` est correctement générée.

### ✅ **Correction**

1. **Classe `Greeting.java` avec Lombok :**

   ```java
   package com.example.demo;

   import jakarta.persistence.Column;
   import jakarta.persistence.Entity;
   import jakarta.persistence.GeneratedValue;
   import jakarta.persistence.GenerationType;
   import jakarta.persistence.Id;
   import jakarta.persistence.Table;
   import lombok.Data;

   @Entity
   @Table(name = "greeting")
   @Data
   public class Greeting {

       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;

       @Column(name = "content", nullable = false)
       private String content;

       // Lombok génère automatiquement les getters, setters, et constructeurs.
   }
   ```

---

## 7️⃣ **Exercice 4 : Recréer la base de données automatiquement**

### 📝 **Enoncé**

Recréez la base de données `haythem` automatiquement sans avoir besoin de la créer manuellement dans PostgreSQL.

**Étapes :**
1. Configurez votre application pour que la base de données soit automatiquement créée si elle n'existe pas.
2. Testez votre application pour vérifier que la base de données et la table sont générées automatiquement.

### ✅ **Correction**

1. **Modification dans `application.properties` ou `application.yml` :**

   Ajoutez ou modifiez la ligne suivante pour permettre la création automatique de la base de données :

   ```properties
   spring.jpa.hibernate.ddl-auto=create-drop
   ```

   ou

   ```yaml
   spring:
     jpa:
       hibernate:
         ddl-auto: create-drop
   ```

   **⚠️ Explication :** Avec `create-drop`, la base de données est créée au démarrage de l'application et supprimée à l'arrêt. Cela vous permet de recréer automatiquement la base de données pour les tests, mais attention, cette configuration n'est pas recommandée en production.

---

🎓 **Ce tutoriel et ses exercices vous permettent non seulement de maîtriser l'intégration de PostgreSQL avec Jakarta Persistence, mais aussi d'explorer des alternatives comme Javax Persistence, l'utilisation de Lombok, et la configuration avancée avec `application.yml`.** 🌟

# ==> Étape suivante : Ajout de la base de donnée mémoire H2
