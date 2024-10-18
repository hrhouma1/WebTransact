# Examen : Projet Gestion des Livres et Auteurs avec Jakarta EE

# Partie 1 

# 1. Relations entre les entités

**Question** :  
Dessinez manuellement le diagramme de relations entre les entités suivantes : `Address`, `Author`, `Book`, `Reader`, et `Review`.  
Identifiez les types de relations (un à un, un à plusieurs, plusieurs à plusieurs) entre ces entités et expliquez brièvement la nature de ces relations.

---

# 2. Dépendances Maven dans le fichier `pom.xml`

**Question** :  
Proposez les dépendances à ajouter dans le fichier `pom.xml` pour chacun des éléments suivants :
  1. Base de données H2 en mémoire.
  2. Base de données PostgreSQL.
  3. Utilisation de JPA (Jakarta Persistence API).
  4. Implémentation des services web REST avec Jakarta EE.

---

# 3. Création d'une méthode dans le contrôleur pour ajouter un livre

**Question** :  
- Complétez le code suivant dans un contrôleur pour exposer un service REST permettant d'ajouter un nouveau livre dans la base de données. 
- Utilisez les couches service et repository. Les informations fournies sont : le titre, le sous-titre, le nombre de pages, la langue, et l'auteur.

### Code partiellement fourni à compléter :

#### 1. **BookController.java** (contrôleur)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/books")
public class BookController {

    @Autowired
    private BookService bookService;

    @PostMapping("/add")
    public Book addBook(@RequestBody Book book) {
        // Appelez la méthode de service pour ajouter le livre
        return ___________;
    }
}
```

#### 2. **BookService.java** (service)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class BookService {

    @Autowired
    private BookRepository bookRepository;

    public Book addBook(Book book) {
        // Utilisez le repository pour sauvegarder le livre
        return ___________;
    }
}
```

#### 3. **BookRepository.java** (repository)

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface BookRepository extends JpaRepository<Book, Integer> {
    // Ajoutez la ou les méthodes ici, si nécessaire
}
```

---

# 4. Création d'une méthode dans le contrôleur pour récupérer un livre par son ID

**Question** :  
Complétez le code suivant pour exposer un service REST permettant de récupérer un livre à partir de son ID. Utilisez les couches service et repository.

### Code partiellement fourni à compléter :

#### 1. **BookController.java** (contrôleur)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/books")
public class BookController {

    @Autowired
    private BookService bookService;

    @GetMapping("/{id}")
    public Book getBookById(@PathVariable int id) {
        // Appelez la méthode de service pour récupérer le livre
        return ___________;
    }
}
```

#### 2. **BookService.java** (service)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.Optional;

@Service
public class BookService {

    @Autowired
    private BookRepository bookRepository;

    public Book getBookById(int id) {
        // Utilisez le repository pour trouver le livre par son ID
        Optional<Book> book = ___________;
        // Gérez le cas où le livre n'est pas trouvé
        if (book.isPresent()) {
            return book.get();
        } else {
            throw new RuntimeException("Livre non trouvé pour l'ID : " + id);
        }
    }
}
```

#### 3. **BookRepository.java** (repository)

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface BookRepository extends JpaRepository<Book, Integer> {
    // Ajoutez ici une méthode pour rechercher un livre par son id si nécessaire
}
```

---

# 5. Création d'une méthode dans le contrôleur pour rechercher un livre par son titre

**Question** :  
Complétez le code suivant pour implémenter une méthode qui permet de rechercher un livre par son titre. Utilisez les couches service et repository.

### Code partiellement fourni à compléter :

#### 1. **BookController.java** (contrôleur)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/books")
public class BookController {

    @Autowired
    private BookService bookService;

    @GetMapping("/title/{title}")
    public Book getBookByTitle(@PathVariable String title) {
        // Appelez la méthode de service pour rechercher le livre par son titre
        return ___________;
    }
}
```

#### 2. **BookService.java** (service)

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class BookService {

    @Autowired
    private BookRepository bookRepository;

    public Book getBookByTitle(String title) {
        // Utilisez le repository pour rechercher le livre par son titre
        Book book = ___________;
        if (book != null) {
            return book;
        } else {
            throw new RuntimeException("Livre non trouvé pour le titre : " + title);
        }
    }
}
```

#### 3. **BookRepository.java** (repository)

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface BookRepository extends JpaRepository<Book, Integer> {
    // Ajoutez ici une méthode pour rechercher un livre par son titre si nécessaire
}
```

---

# 6. Proposer une méthode de votre choix

**Question** :  
Proposez et implémentez une méthode de votre choix. Par exemple, ajoutez un auteur, ajoutez un commentaire de review, ou toute autre fonctionnalité pertinente. Implémentez cette méthode dans les couches `Controller`, `Service`, et `Repository`.


