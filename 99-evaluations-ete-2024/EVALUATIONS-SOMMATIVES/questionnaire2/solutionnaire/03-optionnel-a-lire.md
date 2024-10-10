# Tutoriel : Calcul de la moyenne des numéros de siège (Question d’évaluation)

### Contexte

Dans cet exercice, nous allons examiner un cas où les numéros de siège dans une base de données sont stockés sous forme de chaînes de caractères alphanumériques (par exemple, `'12A'`, `'14B'`, etc.). Le but est de **calculer la moyenne des numéros de siège** d'un vol donné, mais pour cela, il est nécessaire d'extraire la partie numérique des chaînes de caractères avant de réaliser le calcul.

### Problème à résoudre

Dans la base de données, les numéros de siège sont stockés sous forme de chaînes de caractères dans la table `Passenger`, ce qui rend impossible un calcul direct de la moyenne à partir du champ `seatNumber`. Par exemple, voici la requête que vous devez résoudre :

```sql
SELECT AVG(seatNumber) FROM Passenger WHERE flightId = 1;
```

### Objectif

**Votre objectif** est d'extraire la partie numérique de chaque numéro de siège et de calculer la moyenne sur ces valeurs numériques. Cette question est classée comme difficile car elle nécessite de manipuler les données alphanumériques pour les rendre utilisables dans un calcul numérique.

### Étapes à suivre

1. **Extraire la partie numérique des numéros de siège :** 
   - La première étape consiste à extraire uniquement les chiffres des chaînes de caractères. Par exemple, `'12A'` devient `12`.
   
2. **Convertir les chaînes en entiers :**
   - Une fois la partie numérique extraite, il faut convertir cette valeur en entier (`Integer` en Java) pour effectuer le calcul.

3. **Calculer la moyenne :**
   - Enfin, vous devrez calculer la moyenne des valeurs extraites.

### Restrictions et contraintes

- Vous ne pouvez pas résoudre cette question directement via **JPQL** car il n’existe pas de fonction pour manipuler les chaînes de caractères de cette manière dans **JPQL**. Vous devrez donc effectuer cette transformation directement dans le code Java après avoir récupéré les données via une requête JPQL.

### Exemple d'implémentation en Java

Vous pouvez récupérer les numéros de siège d'un vol donné via une requête JPQL et transformer ces données dans votre service Java. Voici un exemple de code pour vous guider :

#### 1. Récupérer les numéros de siège via JPQL

```java
@Query("SELECT p.seatNumber FROM Passenger p WHERE p.flight.flightId = :flightId")
List<String> findSeatNumbersByFlightId(@Param("flightId") Long flightId);
```

#### 2. Transformer les données et calculer la moyenne dans le service

```java
public double calculateAverageSeatNumber(Long flightId) {
    List<String> seatNumbers = passengerRepository.findSeatNumbersByFlightId(flightId);
    List<Integer> numericSeatNumbers = seatNumbers.stream()
        .map(seat -> {
            // Extraire la partie numérique de chaque numéro de siège
            String numericPart = seat.replaceAll("[^0-9]", "");
            return Integer.parseInt(numericPart);
        })
        .collect(Collectors.toList());

    // Calculer la moyenne des numéros de siège
    return numericSeatNumbers.stream()
        .mapToInt(Integer::intValue)
        .average()
        .orElse(0); // Retourne 0 si aucun résultat
}
```

### Explications techniques

1. **Extraction de la partie numérique** :
   - La méthode `replaceAll("[^0-9]", "")` permet de retirer tous les caractères non numériques de chaque numéro de siège, ne conservant que les chiffres.

2. **Conversion en entier** :
   - Après avoir extrait les chiffres, `Integer.parseInt()` permet de convertir la chaîne résultante en un entier.

3. **Calcul de la moyenne** :
   - En utilisant `stream()` et `mapToInt()`, vous pouvez calculer la moyenne des entiers obtenus à partir des numéros de siège.

### Conclusion

Cette question est difficile car elle nécessite de **prétraiter les données** avant de pouvoir les utiliser dans un calcul numérique. C’est un exemple classique de ce que l’on peut rencontrer dans la manipulation des données brutes. 

Ce tutoriel vous montre comment récupérer des données complexes depuis une base de données et les transformer afin de les rendre utilisables dans des opérations comme le calcul de la moyenne.

Bravo pour vos efforts et bonne chance pour la suite de l’évaluation !

Cordialement,  
**Haythem Rehouma**

-----------------------
# Annexe  : Est ce que JPQL est suffisant pour  gérer des opérations de manipulation complexes de chaînes de caractères. C'est quoi son utilité ?
-----------------------


# Réponse : 

- Bien que **JPQL** (Java Persistence Query Language) ne puisse pas gérer des opérations de manipulation complexes de chaînes de caractères comme l'extraction de la partie numérique d'une chaîne, il reste très utile dans un grand nombre de situations. Voici pourquoi on utilise **JPQL** et ses avantages dans un projet Spring Boot, même s'il ne peut pas effectuer certaines manipulations complexes directement :

### 1. **Abstraction et compatibilité avec les bases de données**
   - **JPQL** est une surcouche qui permet d'écrire des requêtes de manière abstraite, indépendamment de la base de données sous-jacente (PostgreSQL, MySQL, etc.). En écrivant des requêtes JPQL, tu t’assures que ton code reste **portatif** et **compatibles** avec plusieurs types de bases de données.
   - Si tu écris des requêtes en SQL natif, ces requêtes peuvent ne pas fonctionner sur une autre base de données en raison des différences de syntaxe SQL. **JPQL** t'évite ce problème.

### 2. **Utilisation des entités Java**
   - **JPQL** est conçu pour travailler directement avec les **entités** Java (les classes annotées avec `@Entity`). Cela signifie que tu écris des requêtes en te basant sur les attributs des objets Java plutôt que sur les colonnes de la base de données.
   - Par exemple, avec **JPQL**, tu peux interroger un champ d'une entité Java, même s'il est mappé à plusieurs tables ou colonnes dans la base de données. C’est un avantage en termes de **clarté** et de **lisibilité** du code.

### 3. **Gestion des relations entre les entités**
   - **JPQL** est excellent pour **naviguer dans les relations entre entités**. Par exemple, tu peux facilement interroger des entités liées avec des jointures (`@ManyToOne`, `@OneToMany`, etc.) sans avoir à te soucier des détails complexes de la jointure en SQL.
   - Si tu veux récupérer tous les passagers d’un vol, **JPQL** te permet d’écrire des requêtes simples en fonction des entités, comme :
     ```java
     @Query("SELECT p FROM Passenger p WHERE p.flight.flightId = :flightId")
     List<Passenger> findPassengersByFlightId(@Param("flightId") Long flightId);
     ```

### 4. **Facilité d’utilisation dans les projets Spring Boot**
   - **JPQL** s'intègre parfaitement avec Spring Data JPA, ce qui permet d'automatiser et de simplifier la création de nombreuses méthodes de requêtes (par exemple, `findBy`, `countBy`, etc.).
   - Tu peux également personnaliser les requêtes avec des annotations comme `@Query` pour des besoins plus spécifiques sans avoir à écrire du SQL natif.

### 5. **Optimisation des performances**
   - **JPQL** permet de gérer le *lazy loading* et le *fetching* de données de manière efficace. Tu peux spécifier la manière dont les relations sont chargées (par exemple `JOIN FETCH` pour charger des relations en une seule requête), ce qui peut considérablement améliorer les performances dans certains cas.

### 6. **Sécurité et protection contre les injections SQL**
   - **JPQL** protège automatiquement contre les injections SQL, car il ne permet pas de concaténer des chaînes de requêtes de manière dangereuse. Les paramètres sont passés de manière sécurisée via `@Param`, ce qui rend ton code moins vulnérable.

---

### Conclusion : Pourquoi utiliser **JPQL** malgré ses limitations ?
Même si **JPQL** ne gère pas des transformations complexes de données (comme l'extraction de la partie numérique d'une chaîne), il reste un outil **extrêmement puissant** pour :
- Interroger les bases de données de manière **abstraite** et **indépendante**,
- Gérer les **relations entre entités** de façon fluide,
- Maintenir la **portabilité** de ton code,
- Améliorer la **sécurité** et les **performances**.

Dans des cas comme celui de l'extraction de la partie numérique, il est plus efficace de laisser **JPQL** récupérer les données, puis de faire les transformations complexes dans le code Java. Cela te permet de tirer parti des avantages de **JPQL** tout en gérant des opérations spécifiques que JPQL ne prend pas en charge.

Ainsi, **JPQL** et le code Java travaillent ensemble pour offrir une solution complète.
