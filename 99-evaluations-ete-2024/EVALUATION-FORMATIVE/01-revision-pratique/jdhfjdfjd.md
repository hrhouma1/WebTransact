# **Exercice 1 : Le Détective des Annotations**

Un contrôleur REST pour gérer des produits a été saboté ! Aide à restaurer le code en remplissant les annotations et paramètres manquants.

```java
// Complète les annotations manquantes pour que cette classe puisse répondre aux requêtes HTTP
@__________
@__________("/produits")
public class ProductController {

    // Complète pour gérer les requêtes GET à l'URL /produits
    @__________
    public List<Product> getAllProducts() {
        return Arrays.asList(
            new Product(1, "Ordinateur", "Electronics"),
            new Product(2, "Chaise", "Furniture")
        );
    }

    // Complète pour gérer une requête POST qui permet de créer un nouveau produit
    @__________("/create")
    public Product addProduct(@__________ Product product) {
        return product; // Simule la création du produit
    }

    // Complète pour gérer une requête GET avec un paramètre d'URL pour récupérer un produit par son ID
    @__________("/id/{productId}")
    public Product getProductById(@__________ int productId) {
        return new Product(productId, "Produit Existant", "Catégorie"); // Simule le retour d’un produit
    }
}
```















---

### **Exercice 2 : Choisis la Bonne Route**

Complète ce quiz en choisissant la bonne annotation ou option pour chaque situation.  

1. Si tu veux gérer une requête GET pour afficher une liste d'utilisateurs à l'URL `/users/all`, laquelle des annotations suivantes utiliserais-tu ?
   - A) `@RequestMapping("/users/all")`
   - B) `@GetMapping("/all")`
   - C) `@PostMapping("/all")`

2. Pour associer une méthode à l’URL `/items/{id}`, et faire en sorte que la variable `id` dans l’URL soit capturée dans un paramètre de méthode, laquelle des annotations suivantes est correcte ?
   - A) `@PathVariable`
   - B) `@RequestParam`
   - C) `@RequestBody`

3. Lorsque tu veux récupérer des données envoyées dans le corps d’une requête POST, tu dois utiliser :
   - A) `@RequestBody`
   - B) `@PathVariable`
   - C) `@RequestMapping`

**Bonus** : Explique pourquoi la méthode `@PostMapping` est plus appropriée pour la création de ressources.

---

### **Exercice 3 : Réécris l'Histoire**

Un développeur a mal implémenté les routes dans une application Spring Boot. 
Ta mission est de réécrire le code pour le rendre correct. Voici ce que tu dois corriger :

```java
@RestController
public class UserController {

    // Cette méthode doit gérer les requêtes POST pour créer un utilisateur, mais elle est incorrecte. Corrige-la.
    @RequestMapping(value = "/users", method = RequestMethod.GET)
    public User createUser(@RequestBody User user) {
        // Code pour créer l'utilisateur
        return user;
    }

    // Cette méthode est censée retourner un utilisateur par ID avec une requête GET, mais elle a des erreurs.
    @RequestMapping(value = "/users", method = RequestMethod.POST)
    public User getUserById(@PathVariable int id) {
        // Code pour retourner l'utilisateur
        return new User(id, "Jean", "Dupont");
    }
}
```

**Instructions** :
1. Corrige les annotations de chaque méthode.
2. Assure-toi que les méthodes correspondent aux bonnes routes et types de requêtes HTTP.
3. Explique pourquoi les changements que tu as faits sont corrects.

---

### **Exercice 4 : La Route Mystère**

Un client utilise une application pour commander des articles. Ton objectif est d'écrire une méthode REST dans un contrôleur Spring Boot qui permet de filtrer les commandes en fonction de leur **état** et de leur **client**.

```java
// Complète cette méthode pour filtrer les commandes par client et état.
// Les paramètres doivent être passés via des requêtes HTTP.
@__________("/orders")
public List<Order> getOrdersByStateAndClient(@__________(name = "state") String state, @__________(name = "client") String client) {
    // Code pour retourner les commandes filtrées
    return Arrays.asList(
        new Order(1, client, "Completed"),
        new Order(2, client, state)
    );
}
```

**Questions supplémentaires** :
1. **Comment pourrais-tu rendre les paramètres `state` et `client` optionnels dans cette méthode ?**
2. **Quelles bonnes pratiques recommanderais-tu pour la gestion des erreurs dans cette méthode ?**

---

### **Exercice 5 : Déboguage des Annotations**

Un étudiant a écrit le code suivant pour créer un endpoint dans une API, mais il y a plusieurs erreurs d'annotations et de logique. Aide-le à corriger le code.

```java
@RestController
@RequestMapping("/clients")
public class ClientController {

    @GetMapping("/{id}")
    public Client getClientById(@RequestBody int id) {
        // Erreur: mauvaise annotation pour capturer l'ID
        return new Client(id, "Alice", "Paris");
    }

    @PostMapping("/add")
    public Client addClient(@PathVariable Client client) {
        // Erreur: mauvaise annotation pour gérer le corps de la requête
        return client;
    }
}
```

**Instructions** :
1. Identifie et corrige les erreurs dans le code ci-dessus.
2. Explique chaque correction que tu as apportée et pourquoi elle est nécessaire.

---

Ces exercices permettent aux étudiants de manipuler des annotations, de comprendre les subtilités entre les différentes options, et d’évaluer leur logique tout en restant interactifs et motivants.
