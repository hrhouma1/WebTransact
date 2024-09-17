
### 1. **Classe `Movie` :**

```java
public class Movie {
    private int id;
    private String title;
    private String director;
    private int releaseYear;

    // Constructeur par défaut
    public Movie() {
    }

    // Constructeur avec paramètres
    public Movie(int id, String title, String director, int releaseYear) {
        this.id = id;
        this.title = title;
        this.director = director;
        this.releaseYear = releaseYear;
    }

    // Getters et setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getDirector() {
        return director;
    }

    public void setDirector(String director) {
        this.director = director;
    }

    public int getReleaseYear() {
        return releaseYear;
    }

    public void setReleaseYear(int releaseYear) {
        this.releaseYear = releaseYear;
    }
}
```

---

### 2. **Contrôleur `MovieController` :**

#### **Étape 1 : Créer la classe `MovieController`**

```java
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("/movies")  // Route de base
public class MovieController {

    private List<Movie> movieList = new ArrayList<>(); // Simule une base de données

    // Méthode pour récupérer tous les films
    @GetMapping
    public List<Movie> getAllMovies() {
        return movieList;  // Retourne la liste de tous les films
    }

    // Méthode pour ajouter un nouveau film
    @PostMapping("/create")
    public Movie addMovie(@RequestBody Movie movie) {
        movieList.add(movie);  // Ajoute le film à la liste
        return movie;  // Retourne le film ajouté
    }

    // Méthode pour récupérer un film par ID
    @GetMapping("/{movieId}")
    public Movie getMovieById(@PathVariable int movieId) {
        return movieList.stream()
                        .filter(movie -> movie.getId() == movieId)
                        .findFirst()
                        .orElse(null);  // Retourne le film si trouvé, sinon null
    }

    // Méthode pour supprimer un film
    @DeleteMapping("/{movieId}")
    public String deleteMovie(@PathVariable int movieId) {
        boolean removed = movieList.removeIf(movie -> movie.getId() == movieId);
        return removed ? "Film supprimé" : "Film non trouvé";
    }
}
```

---

### 3. **Fichier `.http` pour tester l'API :**

```http
# Récupérer tous les films
GET http://localhost:8080/movies

###

# Ajouter un nouveau film
POST http://localhost:8080/movies/create
Content-Type: application/json

{
  "id": 1,
  "title": "Inception",
  "director": "Christopher Nolan",
  "releaseYear": 2010
}

###

# Récupérer un film spécifique par ID
GET http://localhost:8080/movies/1

###

# Supprimer un film par ID
DELETE http://localhost:8080/movies/1
```

---

### 4. **Explications des points clés :**

1. **Classe `Movie`** : Cette classe modélise les films avec des attributs basiques comme `id`, `title`, `director`, et `releaseYear`. Elle inclut également des getters, setters et deux constructeurs (un par défaut et un avec paramètres).
   
2. **Contrôleur `MovieController`** :
   - La méthode `getAllMovies` utilise l'annotation `@GetMapping` pour gérer les requêtes GET sur `/movies`.
   - La méthode `addMovie` utilise `@PostMapping` pour ajouter un film à la liste des films.
   - La méthode `getMovieById` utilise `@GetMapping("/{movieId}")` pour récupérer un film spécifique par son ID.
   - La méthode `deleteMovie` utilise `@DeleteMapping("/{movieId}")` pour supprimer un film par son ID et renvoyer un message approprié.

3. **Fichier `.http`** : Ce fichier contient les appels API pour tester chaque fonctionnalité de l'API REST. Il utilise les bonnes méthodes HTTP (`GET`, `POST`, `DELETE`) et inclut les requêtes JSON pour tester l'ajout d'un film.

