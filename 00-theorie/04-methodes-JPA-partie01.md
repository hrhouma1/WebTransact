# Question: Quand et pourquoi écrire une méthode personnalisée comme `findByCustomerId` dans un `Repository` Spring Data JPA ?

# 1. Introduction à Spring Data JPA et les Repositories
Spring Data JPA est un framework qui facilite l'accès aux bases de données dans les applications Java, en s'appuyant sur JPA (Java Persistence API). L'un des avantages de Spring Data JPA est qu'il fournit des interfaces prêtes à l'emploi, comme `CrudRepository`, qui offrent un ensemble de méthodes CRUD (Create, Read, Update, Delete) sans que vous ayez besoin de les implémenter manuellement.

# 2. Les Méthodes par Défaut de `CrudRepository`
Lorsque vous étendez `CrudRepository`, vous bénéficiez d'un ensemble de méthodes CRUD prédéfinies, telles que :
- `save(S entity)` : Pour sauvegarder ou mettre à jour une entité.
- `findById(ID id)` : Pour récupérer une entité par son ID.
- `findAll()` : Pour récupérer toutes les entités.
- `deleteById(ID id)` : Pour supprimer une entité par son ID.
- Et plusieurs autres...

Ces méthodes couvrent les opérations de base que vous effectuerez fréquemment. Cependant, dans certaines situations, vous aurez besoin d'effectuer des requêtes plus spécifiques qui ne sont pas couvertes par les méthodes standards de `CrudRepository`.

## Exercice : 

### 1️⃣ Cloner le projet
```bash
git clone https://github.com/hrhouma1/accounts-v1.git
```

### 2️⃣ Accéder au répertoire du projet
```bash
cd accounts-v1
```

### 3️⃣ Ouvrir le projet dans votre éditeur de code (par exemple, Visual Studio Code) et observez la classe AccountsRepository dans le dossier Repository

```bash
code .
```

```bash
package com.eazybytes.accounts.repository;

import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

import com.eazybytes.accounts.model.Accounts;

@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

	Accounts findByCustomerId(int customerId);

}

```



# Question:

Pourquoi le repository contient-il uniquement la méthode `findByCustomerId` ? Pourquoi les autres méthodes comme `save`, `delete`, ou `findAll` ne sont-elles pas visibles dans ce repository ? Expliquez la raison de leur absence apparente et comment elles sont réellement accessibles.

# 3. Quand écrire une méthode personnalisée comme `findByCustomerId` ?
Vous devez écrire une méthode personnalisée lorsque :
- **Vous avez besoin de requêtes spécifiques** : Lorsque vous devez interroger la base de données en fonction d'une ou plusieurs colonnes spécifiques qui ne sont pas l'ID primaire. Par exemple, rechercher un compte en fonction de l'ID du client plutôt qu'en utilisant l'ID du compte.
- **Vous souhaitez simplifier l'accès aux données** : Au lieu d'écrire une requête SQL personnalisée à chaque fois, vous pouvez créer une méthode dans le `Repository` pour rendre le code plus propre et réutilisable.
- **Vous avez besoin d'opérations complexes** : Parfois, vous devez interroger plusieurs colonnes ou appliquer des conditions spécifiques. Dans ce cas, une méthode personnalisée peut être plus appropriée.

# 4. Comment écrire une méthode personnalisée ?
Spring Data JPA permet de définir des méthodes personnalisées en se basant sur les conventions de nommage. Par exemple, pour créer une méthode qui recherche un compte par `customerId`, vous pouvez simplement déclarer une méthode comme suit :

```java
Accounts findByCustomerId(int customerId);
```

Spring Data JPA se base sur le nom de la méthode pour générer automatiquement l'implémentation de la requête SQL correspondante. Dans cet exemple :
- `findBy` : Indique que vous voulez effectuer une recherche.
- `CustomerId` : Spécifie le champ sur lequel la recherche doit être effectuée.

Spring Data JPA comprend ces conventions et génère une requête pour récupérer les comptes où `customerId` correspond à la valeur fournie.

# 5. Exemples de Méthodes Personnalisées
Voici quelques exemples de méthodes personnalisées que vous pourriez vouloir écrire dans un `Repository` :

- **Recherche par plusieurs champs** : Si vous voulez rechercher des comptes par `customerId` et `accountType`, vous pouvez déclarer :
  ```java
  Accounts findByCustomerIdAndAccountType(int customerId, String accountType);
  ```

- **Recherche par une partie d'un champ** : Si vous voulez rechercher des comptes où l'adresse de la branche (`branchAddress`) contient une chaîne de caractères spécifique, vous pouvez déclarer :
  ```java
  List<Accounts> findByBranchAddressContaining(String addressFragment);
  ```

- **Recherche en utilisant une plage de valeurs** : Si vous voulez rechercher des comptes créés après une certaine date, vous pouvez déclarer :
  ```java
  List<Accounts> findByCreateDtAfter(LocalDate date);
  ```

# 6. Avantages des Méthodes Personnalisées
- **Lisibilité** : Le code devient plus lisible, car vous pouvez nommer vos méthodes de manière descriptive.
- **Réutilisabilité** : Une fois définies, ces méthodes peuvent être réutilisées partout dans votre application.
- **Maintenance** : En utilisant des méthodes personnalisées, vous évitez d'avoir à écrire des requêtes SQL complexes partout dans votre code, ce qui facilite la maintenance.

# 7. Quand ne pas écrire de Méthodes Personnalisées
- **Lorsque les méthodes de `CrudRepository` sont suffisantes** : Si les méthodes standards couvrent vos besoins (par exemple, `findById` ou `findAll`), il n'est pas nécessaire de créer des méthodes supplémentaires.
- **Lorsque vous avez besoin de requêtes très complexes** : Dans certains cas, les méthodes personnalisées basées sur des conventions de nommage peuvent ne pas être suffisantes pour exprimer des requêtes SQL très complexes. Dans ces situations, vous devrez peut-être utiliser des requêtes JPQL ou Criteria API.

# 8. Conclusion
Écrire des méthodes personnalisées dans un `Repository` Spring Data JPA est une manière puissante de simplifier l'accès aux données et de rendre votre code plus lisible et maintenable. Vous devriez envisager d'écrire de telles méthodes chaque fois que vous avez besoin d'une requête spécifique qui n'est pas couverte par les méthodes CRUD par défaut. En comprenant les conventions de nommage, vous pouvez facilement créer des méthodes adaptées à vos besoins sans écrire de requêtes SQL complexes.

En adoptant cette pratique, vous contribuerez à une meilleure organisation et à une meilleure structure de votre code, facilitant ainsi la maintenance et l'évolution de votre application.
