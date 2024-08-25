# 📚 **Évaluation Formative : Comprendre et Appliquer les Méthodes Personnalisées dans Spring Data JPA**

### **Objectif**
Cette évaluation formative vise à renforcer la compréhension des méthodes personnalisées dans Spring Data JPA, en les intégrant dans un contexte pratique. Vous allez écrire, tester et expliquer des méthodes personnalisées dans un repository, ainsi que justifier l'utilisation de telles méthodes.

---

### **1️⃣ Cloner le Projet et Configurer l'Environnement**

1. Clonez le projet à partir du dépôt Git suivant :
   ```bash
   git clone https://github.com/hrhouma1/accounts-v1.git
   ```
2. Accédez au répertoire du projet :
   ```bash
   cd accounts-v1
   ```
3. Ouvrez le projet dans votre éditeur de code (par exemple, Visual Studio Code) :
   ```bash
   code .
   ```
4. Assurez-vous que votre base de données PostgreSQL est correctement configurée et que l'application peut se connecter à la base de données. Les détails de configuration se trouvent dans le fichier `application.properties`.

---

### **2️⃣ Étendre le Repository avec des Méthodes Personnalisées**

#### **Exercice 1 : Méthode de Recherche Par Date**
- **Tâche** : Créez une méthode personnalisée dans `AccountsRepository` pour récupérer tous les comptes créés après une date donnée.
- **Indication** : Utilisez les conventions de nommage Spring Data JPA.
- **Code attendu** :

```java
import java.time.LocalDate;
import java.util.List;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;
import com.eazybytes.accounts.model.Accounts;

@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

    List<Accounts> findByCreateDtAfter(LocalDate date);
}
```

#### **Exercice 2 : Méthode de Recherche Par Plage d'Identifiants**
- **Tâche** : Utilisez JPQL pour créer une méthode dans `AccountsRepository` qui trouve des comptes dans une plage spécifique d'identifiants.
- **Indication** : Utilisez l'annotation `@Query`.
- **Code attendu** :

```java
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

    @Query("SELECT a FROM Accounts a WHERE a.accountNumber BETWEEN :startId AND :endId")
    List<Accounts> findAccountsInRange(@Param("startId") long startId, @Param("endId") long endId);
}
```

#### **Exercice 3 : Compter les Comptes Par Type**
- **Tâche** : Créez une méthode personnalisée utilisant JPQL pour compter le nombre de comptes d'un certain type.
- **Indication** : Utilisez l'annotation `@Query`.
- **Code attendu** :

```java
@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

    @Query("SELECT COUNT(a) FROM Accounts a WHERE a.accountType = :accountType")
    long countByAccountType(@Param("accountType") String accountType);
}
```

---

### **3️⃣ Intégrer les Méthodes dans le Service et le Contrôleur**

#### **Exercice 4 : Intégration dans le Service**
- **Tâche** : Ajoutez les méthodes que vous avez créées dans `AccountsService`. Implémentez les services correspondants pour chaque méthode personnalisée du repository.

```java
import java.time.LocalDate;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.repository.AccountsRepository;

@Service
public class AccountsService {

    @Autowired
    private AccountsRepository accountsRepository;

    public List<Accounts> findAccountsCreatedAfter(LocalDate date) {
        return accountsRepository.findByCreateDtAfter(date);
    }

    public List<Accounts> findAccountsInRange(long startId, long endId) {
        return accountsRepository.findAccountsInRange(startId, endId);
    }

    public long countAccountsByType(String accountType) {
        return accountsRepository.countByAccountType(accountType);
    }
}
```

#### **Exercice 5 : Exposer via le Contrôleur**
- **Tâche** : Ajoutez des endpoints dans `AccountsController` pour exposer les méthodes via des API REST. Chaque méthode personnalisée devrait avoir un endpoint distinct.

```java
import java.time.LocalDate;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
public class AccountsController {

    @Autowired
    private AccountsService accountsService;

    @GetMapping("/findAccountsByDate")
    public List<Accounts> findAccountsByDate(@RequestParam String date) {
        return accountsService.findAccountsCreatedAfter(LocalDate.parse(date));
    }

    @GetMapping("/findAccountsInRange")
    public List<Accounts> findAccountsInRange(@RequestParam long startId, @RequestParam long endId) {
        return accountsService.findAccountsInRange(startId, endId);
    }

    @GetMapping("/countAccountsByType")
    public long countAccountsByType(@RequestParam String accountType) {
        return accountsService.countAccountsByType(accountType);
    }
}
```

---

### **4️⃣ Tester les Méthodes et Documenter le Code**

#### **Exercice 6 : Tester avec Postman**
- **Tâche** : Utilisez Postman pour tester chaque endpoint que vous avez créé. Vérifiez que les résultats retournés par l'API sont corrects en fonction des critères donnés.

#### **Exercice 7 : Documenter avec Swagger**
- **Tâche** : Assurez-vous que chaque endpoint est correctement documenté avec Swagger. Vérifiez que la documentation est accessible et descriptive.

---

### **5️⃣ Explication et Justification**

#### **Exercice 8 : Rédaction d'une Explication**
- **Tâche** : Rédigez une courte explication (150-200 mots) expliquant pourquoi vous avez choisi d'utiliser des méthodes personnalisées pour ces cas d'utilisation spécifiques. Justifiez l'utilisation de JPQL pour certaines méthodes.

---

### **6️⃣ Génération de la Javadoc**

#### **Étape 1 : Configurer Maven pour Générer la Javadoc**

1. Ajoutez le plugin `maven-javadoc-plugin` au fichier `pom.xml` de votre projet, dans la section `<plugins>` :
   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-javadoc-plugin</artifactId>
               <version>3.3.1</version>
               <executions>
                   <execution>
                       <goals>
                           <goal>javadoc</goal>
                       </goals>
                   </execution>
               </executions>
           </plugin>
       </plugins>
   </build>
   ```

#### **Étape 2 : Générer la Javadoc avec Maven**

2. Exécutez la commande suivante dans le répertoire racine de votre projet pour générer la Javadoc :
   ```bash
   mvn javadoc:javadoc
   ```

#### **Étape 3 : Accéder à la Documentation Générée**

3. La documentation Javadoc sera générée dans le dossier `target/site/apidocs/` de votre projet. Ouvrez le fichier `index.html` dans un navigateur pour visualiser la documentation.

#### **Étape 4 : Personnalisation et Options**

4. Pour personnaliser davantage la Javadoc, vous pouvez ajouter des informations supplémentaires dans la configuration du plugin, comme l'auteur, la version, etc.

---

### **7️⃣ Soumission**

- **Tâche** : Une fois tous les exercices terminés, soumettez votre code sur une branche distincte de votre dépôt GitHub et envoyez un lien vers votre repository pour évaluation.

---

### **Code Complet avec Javadoc**

Voici le code complet avec les commentaires Javadoc ajoutés :

#### **AccountsRepository.java**

```java
package com.eazybytes.accounts.repository;

import com.eazybytes.accounts.model.Accounts;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

import java.time.LocalDate;
import java.util.List;

/**
 * Repository pour gérer les entités Accounts.
 * Cette interface étend CrudRepository, ce qui lui permet d'hériter de toutes les méthodes CRUD de base.
 */
@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

    /**
     * Méthode personnalisée pour trouver les comptes créés après une date spécifique.
     *
     * @param date la date après laquelle les comptes doivent avoir été créés
     * @return une liste de comptes créés après la date spécifiée
     */
    List<Accounts> findByCreateDtAfter(LocalDate date);

    /**
     * Méthode JPQL pour trouver des comptes dont les identifiants sont dans une plage donnée.
     * @Query permet de définir une requête JPQL personnalisée.
     *
     * @param startId l'identifiant de départ de la plage
     * @param endId   l'identifiant de fin de la plage
     * @return une liste de comptes dont l'identifiant est dans la plage spécifiée
     */
    @Query("SELECT a FROM Accounts a WHERE a.accountNumber

 BETWEEN :startId AND :endId")
    List<Accounts> findAccountsInRange(long startId, long endId);

    /**
     * Méthode JPQL pour compter le nombre de comptes d'un certain type.
     * Cette méthode retourne le nombre de comptes correspondant au type spécifié.
     *
     * @param accountType le type de compte (par exemple, "Savings" ou "Checking")
     * @return le nombre de comptes du type spécifié
     */
    @Query("SELECT COUNT(a) FROM Accounts a WHERE a.accountType = :accountType")
    long countByAccountType(String accountType);
}
```

#### **AccountsService.java**

```java
package com.eazybytes.accounts.service;

import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.repository.AccountsRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.time.LocalDate;
import java.util.List;

/**
 * Service pour gérer la logique métier associée aux comptes.
 * Ce service utilise AccountsRepository pour accéder à la base de données.
 */
@Service
public class AccountsService {

    @Autowired
    AccountsRepository accountsRepository;

    /**
     * Utilise la méthode findByCreateDtAfter() pour trouver des comptes créés après une date donnée.
     *
     * @param date la date après laquelle les comptes doivent avoir été créés
     * @return une liste de comptes créés après la date spécifiée
     */
    public List<Accounts> findAccountsCreatedAfter(LocalDate date) {
        return accountsRepository.findByCreateDtAfter(date);
    }

    /**
     * Utilise la méthode findAccountsInRange() pour trouver des comptes dans une plage d'identifiants.
     *
     * @param startId l'identifiant de départ
     * @param endId   l'identifiant de fin
     * @return une liste de comptes correspondant à la plage d'identifiants
     */
    public List<Accounts> findAccountsInRange(long startId, long endId) {
        return accountsRepository.findAccountsInRange(startId, endId);
    }

    /**
     * Utilise la méthode countByAccountType() pour compter les comptes d'un certain type.
     *
     * @param accountType le type de compte à compter
     * @return le nombre de comptes du type spécifié
     */
    public long countAccountsByType(String accountType) {
        return accountsRepository.countByAccountType(accountType);
    }
}
```

#### **AccountsController.java**

```java
package com.eazybytes.accounts.controller;

import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.service.AccountsService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDate;
import java.util.List;

/**
 * Contrôleur REST pour gérer les requêtes HTTP associées aux comptes bancaires.
 * Ce contrôleur expose des endpoints qui permettent d'interagir avec les comptes via des requêtes HTTP.
 */
@RestController
public class AccountsController {

    @Autowired
    private AccountsService accountsService;

    /**
     * Endpoint pour récupérer les comptes créés après une date spécifique.
     *
     * @param date la date après laquelle les comptes doivent avoir été créés
     * @return une liste de comptes créés après la date spécifiée
     */
    @GetMapping("/findAccountsByDate")
    public List<Accounts> findAccountsByDate(@RequestParam String date) {
        return accountsService.findAccountsCreatedAfter(LocalDate.parse(date));
    }

    /**
     * Endpoint pour trouver des comptes dans une plage d'identifiants.
     *
     * @param startId l'identifiant de départ
     * @param endId   l'identifiant de fin
     * @return une liste de comptes correspondant à la plage d'identifiants
     */
    @GetMapping("/findAccountsInRange")
    public List<Accounts> findAccountsInRange(@RequestParam long startId, @RequestParam long endId) {
        return accountsService.findAccountsInRange(startId, endId);
    }

    /**
     * Endpoint pour compter les comptes d'un certain type.
     *
     * @param accountType le type de compte à compter
     * @return le nombre de comptes du type spécifié
     */
    @GetMapping("/countAccountsByType")
    public long countAccountsByType(@RequestParam String accountType) {
        return accountsService.countAccountsByType(accountType);
    }
}
```

---

### **Conclusion**

Cette évaluation formative vous permet d'appliquer les concepts théoriques dans un contexte pratique tout en développant des compétences en codage, en intégration, en documentation, et en justification des choix techniques. Les apprenants seront en mesure de comprendre les avantages de l'utilisation de méthodes personnalisées dans Spring Data JPA, ainsi que l'importance de la documentation pour rendre leur code plus compréhensible et maintenable.
