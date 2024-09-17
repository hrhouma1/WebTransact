# **Exercice 02: Compléter les annotations et les appels API**

L'objectif de cet exercice est de compléter les annotations et les appels API dans un contrôleur REST pour la gestion des utilisateurs. Plusieurs possibilités sont offertes pour chaque annotation ainsi que pour les appels API, vous devez choisir celles qui vous semblent les plus appropriées.

---

### 1. Compléter les annotations manquantes pour que cette classe puisse répondre aux requêtes HTTP

```java
// Compléter les annotations manquantes pour que cette classe gère les utilisateurs via des requêtes HTTP

____(1)____

public class UserController {

    // Gérer les requêtes GET pour l'URL /users
    ____(2)____

    public List<User> getAllUsers() {
        return Arrays.asList(
            new User(1, "Alice", "Developer"),
            new User(2, "Bob", "Manager")
        );
    }

    // Gérer les requêtes POST pour l'ajout d'un nouvel utilisateur
    ____(3)____

    public User addUser(____(4)____) {
        return user;
    }

    // Gérer les requêtes GET pour récupérer un utilisateur par son ID
    ____(5)____

    public User getUserById(____(6)____) {
        return new User(userId, "Utilisateur Existant", "Role");
    }
}
```

### Explications :
- **(1)** : Annotation pour définir que la classe est un contrôleur qui gère les requêtes HTTP.
- **(2)** : Annotation pour spécifier que la méthode gère les requêtes GET sur `/users`.
- **(3)** : Annotation pour spécifier que la méthode gère les requêtes POST pour ajouter un utilisateur.
- **(4)** : Type d'annotation pour spécifier que l'utilisateur est passé dans le corps de la requête.
- **(5)** : Annotation pour spécifier que la méthode gère les requêtes GET pour récupérer un utilisateur par ID.
- **(6)** : Annotation pour spécifier que l'ID est passé dans l'URL de la requête.

---

### 2. Compléter les appels API pour chaque méthode

# **Récupérer tous les utilisateurs**

```http
### Possibilité 1
____(7)____ http://localhost:8080/users
Accept: application/json

### Possibilité 2
____(8)____ http://localhost:8080/users
Accept: application/xml
```

# **Ajouter un nouvel utilisateur**

```http
### Possibilité 1
____(9)____ http://localhost:8080/users/create
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "Designer"
}
```

# **Récupérer un utilisateur par son ID**

```http
### Possibilité 1
____(10)____ http://localhost:8080/users/id/1
Accept: application/json
```

### Explications :
- **(7)** : Type de requête (GET) pour récupérer tous les utilisateurs.
- **(8)** : Une autre option de format d'acceptation pour la réponse (XML).
- **(9)** : Type de requête (POST) pour ajouter un nouvel utilisateur avec les détails fournis dans le corps de la requête.
- **(10)** : Type de requête (GET) pour récupérer un utilisateur spécifique par son ID.



# Annexe - version 1


```java
@RestController
@RequestMapping("/produits")
public class ProductController {

    // Gérer les requêtes GET pour l'URL /produits
    @GetMapping
    public List<Product> getAllProducts() {
        return Arrays.asList(
            new Product(1, "Ordinateur", "Electronics"),
            new Product(2, "Chaise", "Furniture")
        );
    }

    // Gérer les requêtes POST pour l'ajout d'un nouveau produit
    @PostMapping("/create")
    public Product addProduct(@RequestBody Product product) {
        return product;
    }

    // Gérer les requêtes GET pour récupérer un produit par son ID
    @GetMapping("/id/{productId}")
    public Product getProductById(@PathVariable int productId) {
        return new Product(productId, "Produit Existant", "Catégorie");
    }
}
```

### Explications des choix :
1. **Controller HTTP** : `@RestController` pour indiquer que cette classe gère des requêtes REST (le contrôle de produits ici).
2. **Mapping URL** : `@RequestMapping("/produits")` définit le préfixe commun pour les routes de la classe.
3. **Méthode GET pour récupérer tous les produits** : `@GetMapping` correspond à une méthode GET sans besoin d'indiquer le chemin supplémentaire.
4. **Méthode POST pour ajouter un produit** : `@PostMapping("/create")` pour gérer les requêtes POST à l'URL `/create` et `@RequestBody` pour lier le corps de la requête à un objet `Product`.
5. **Méthode GET pour récupérer un produit par son ID** : `@GetMapping("/id/{productId}")` pour une requête GET avec un paramètre d'URL et `@PathVariable` pour lier le segment `{productId}` au paramètre de méthode. 



# Annexe - version 2 - alternative utilisant `@RequestMapping` pour toutes les routes au lieu de `@GetMapping` et `@PostMapping` :

```java
import org.springframework.web.bind.annotation.*;  // Import nécessaire pour les annotations

@RestController  // Indique que c'est un contrôleur REST
@RequestMapping("/users")  // Spécifie la base de l'URL pour les requêtes
public class UserController {

    // Gérer les requêtes GET pour l'URL /users
    @RequestMapping(method = RequestMethod.GET)  // Gérer la requête GET pour /users
    public List<User> getAllUsers() {
        return Arrays.asList(
            new User(1, "Alice", "Developer"),
            new User(2, "Bob", "Manager")
        );
    }

    // Gérer les requêtes POST pour l'ajout d'un nouvel utilisateur
    @RequestMapping(method = RequestMethod.POST)  // Gérer la requête POST pour /users
    public User addUser(@RequestBody User user) {
        return user;
    }

    // Gérer les requêtes GET pour récupérer un utilisateur par son ID
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)  // Gérer la requête GET avec un paramètre ID
    public User getUserById(@PathVariable("id") int userId) {
        return new User(userId, "Utilisateur Existant", "Role");
    }
}
```

Dans cette version :

1. On utilise systématiquement `@RequestMapping` avec le paramètre `method` pour définir le type de requête HTTP (`RequestMethod.GET` pour GET et `RequestMethod.POST` pour POST).
2. Pour les requêtes avec des paramètres, comme l'ID de l'utilisateur, on utilise `@RequestMapping(value = "/{id}", method = RequestMethod.GET)` pour spécifier la route avec le paramètre ID.

Cela permet de gérer tous les types de requêtes avec une seule annotation (`@RequestMapping`).
