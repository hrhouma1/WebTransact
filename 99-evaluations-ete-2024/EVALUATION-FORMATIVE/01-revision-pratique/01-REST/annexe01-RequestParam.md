# `@RequestParam` vs  `@PathVariable`

```java
import org.springframework.web.bind.annotation.*;  // Import nécessaire pour les annotations

@RestController  // Indiquer que c'est un contrôleur REST
@RequestMapping("/produits")  // Spécifie la base de l'URL pour les requêtes
public class ProductController {

    // Gérer les requêtes GET pour l'URL /produits
    @GetMapping  // Pour les requêtes GET
    public List<Product> getAllProducts() {
        return Arrays.asList(
            new Product(1, "Ordinateur", "Electronics"),
            new Product(2, "Chaise", "Furniture")
        );
    }

    // Gérer les requêtes POST pour l'ajout d'un nouveau produit
    @PostMapping("/create")  // Pour les requêtes POST sur /create
    public Product addProduct(@RequestBody Product product) {  // @RequestBody pour envoyer des données dans le corps de la requête
        return product;
    }

    // Gérer les requêtes GET pour récupérer un produit par son ID
    @GetMapping("/id/{productId}")  // Pour les requêtes GET avec l'ID du produit dans l'URL
    public Product getProductById(@PathVariable int productId) {  // @PathVariable pour récupérer l'ID du produit dans l'URL
        return new Product(productId, "Produit Existant", "Catégorie");
    }
}
```

### Explications :
1. **Contrôleur REST** : On utilise `@RestController` pour indiquer que la classe gère des requêtes HTTP de type REST.
2. **Requêtes GET** :
   - `@GetMapping` est utilisé pour gérer les requêtes GET, par exemple pour obtenir la liste de tous les produits ou un produit par son ID.
   - `@PathVariable` est utilisé pour extraire l'ID du produit directement depuis l'URL.
3. **Requêtes POST** :
   - `@PostMapping("/create")` gère les requêtes POST pour ajouter un produit. 
   - `@RequestBody` est utilisé pour envoyer les données d'un produit dans le corps de la requête, ce qui est la méthode correcte dans ce cas.

### Concernant `@RequestParam` :
`@RequestParam` est utilisé pour extraire les paramètres de requête (query parameters) qui sont passés dans l'URL, par exemple : `/produits?id=1`. 
Cependant, ce n'est pas approprié ici, car tu récupères un **segment d'URL** (comme `"/id/{productId}"`), ce qui doit être fait avec `@PathVariable`.

En résumé, dans notre exemple pour récupérer un produit par son ID, il faut utiliser `@PathVariable` au lieu de `@RequestParam`.
