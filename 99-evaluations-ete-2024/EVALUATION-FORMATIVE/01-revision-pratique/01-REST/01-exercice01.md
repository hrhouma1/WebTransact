# **Exercice 01: Compléter les annotations et les appels API**

L'objectif de cet exercice est de compléter les annotations et les appels API dans un contrôleur REST pour la gestion de produits. Plusieurs possibilités sont offertes pour chaque annotation ainsi que pour les appels API, vous devez choisir celles qui vous semblent les plus appropriées.

# 1. Compléter les annotations manquantes pour que cette classe puisse répondre aux requêtes HTTP

```java
// Compléter les annotations manquantes pour que cette classe gère les produits via des requêtes HTTP

@Possibilité 1 : @RestController
@Possibilité 2 : @Controller
@Possibilité 3 : @Component
@Possibilité 4 : @Service
@Possibilité 5 : @RequestMapping("/produits")

public class ProductController {

    // Gérer les requêtes GET pour l'URL /produits
    @Possibilité 1 : @GetMapping
    @Possibilité 2 : @RequestMapping(method = RequestMethod.GET)
    @Possibilité 3 : @PostMapping
    @Possibilité 4 : @DeleteMapping
    @Possibilité 5 : @PatchMapping

    public List<Product> getAllProducts() {
        return Arrays.asList(
            new Product(1, "Ordinateur", "Electronics"),
            new Product(2, "Chaise", "Furniture")
        );
    }

    // Gérer les requêtes POST pour l'ajout d'un nouveau produit
    @Possibilité 1 : @PostMapping("/create")
    @Possibilité 2 : @RequestMapping(value = "/create", method = RequestMethod.POST)
    @Possibilité 3 : @PutMapping("/create")
    @Possibilité 4 : @PatchMapping("/create")
    @Possibilité 5 : @DeleteMapping("/create")

    public Product addProduct(@Possibilité 1 : @RequestBody Product product, 
                              @Possibilité 2 : @ModelAttribute Product product, 
                              @Possibilité 3 : @PathVariable Product product, 
                              @Possibilité 4 : @RequestParam Product product, 
                              @Possibilité 5 : @SessionAttribute Product product) {
        return product;
    }

    // Gérer les requêtes GET pour récupérer un produit par son ID
    @Possibilité 1 : @GetMapping("/id/{productId}")
    @Possibilité 2 : @RequestMapping(value = "/id/{productId}", method = RequestMethod.GET)
    @Possibilité 3 : @PostMapping("/id/{productId}")
    @Possibilité 4 : @PatchMapping("/id/{productId}")
    @Possibilité 5 : @DeleteMapping("/id/{productId}")

    public Product getProductById(@Possibilité 1 : @PathVariable int productId, 
                                  @Possibilité 2 : @RequestParam int productId, 
                                  @Possibilité 3 : @RequestHeader int productId, 
                                  @Possibilité 4 : @CookieValue int productId, 
                                  @Possibilité 5 : @SessionAttribute int productId) {
        return new Product(productId, "Produit Existant", "Catégorie");
    }
}
```

# 2. Proposez 5 possibilités d'appels API pour chaque méthode

# **Récupérer tous les produits**

```http
### Possibilité 1
GET http://localhost:8080/produits
Accept: application/json

### Possibilité 2
GET http://localhost:8080/produits
Accept: application/xml

### Possibilité 3
GET http://localhost:8080/api/produits
Accept: application/json

### Possibilité 4
GET http://localhost:8080/v1/produits
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/produits
Accept: application/json
```

# **Ajouter un nouveau produit**

```http
### Possibilité 1
POST http://localhost:8080/produits/create
Content-Type: application/json

{
  "id": 3,
  "name": "Table",
  "category": "Furniture"
}

### Possibilité 2
POST http://localhost:8080/api/produits/create
Content-Type: application/json

{
  "id": 3,
  "name": "Table",
  "category": "Furniture"
}

### Possibilité 3
POST http://localhost:8080/v1/produits/create
Content-Type: application/json

{
  "id": 3,
  "name": "Table",
  "category": "Furniture"
}

### Possibilité 4
POST http://localhost:8080/produits
Content-Type: application/json

{
  "id": 3,
  "name": "Table",
  "category": "Furniture"
}

### Possibilité 5
POST http://localhost:8080/produits/add
Content-Type: application/json

{
  "id": 3,
  "name": "Table",
  "category": "Furniture"
}
```

# **Récupérer un produit par son ID**

```http
### Possibilité 1
GET http://localhost:8080/produits/id/1
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/produits/id/1
Accept: application/json

### Possibilité 3
GET http://localhost:8080/v1/produits/id/1
Accept: application/json

### Possibilité 4
GET http://localhost:8080/produits/1
Accept: application/json

### Possibilité 5
GET http://localhost:8080/produits/find/1
Accept: application/json
```


