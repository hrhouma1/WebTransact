# 1. **@RestController**
- **Description** : Cette annotation indique que la classe est un contrôleur Spring qui gère les requêtes HTTP REST. Elle combine `@Controller` et `@ResponseBody`, ce qui signifie que les méthodes renvoient directement les données (au format JSON ou XML) au lieu de renvoyer une vue.

```java
@RestController
public class MonControleur {
    // Méthodes de gestion des requêtes ici
}
```

# 2. **@RequestMapping**
- **Description** : Elle est utilisée pour associer une classe ou une méthode à un chemin spécifique. Elle peut aussi être utilisée pour indiquer le type de requête HTTP (GET, POST, etc.) à gérer.
- **Paramètres** :
  - `value` : Le chemin URL auquel la méthode répond.
  - `method` : Le type de méthode HTTP (GET, POST, PUT, DELETE, etc.).
  
```java
@RequestMapping(value = "/cartes", method = RequestMethod.GET)
public List<Card> getAllCards() {
    // Code pour retourner toutes les cartes
}
```

# 3. **@GetMapping**
- **Description** : Spécifie qu’une méthode doit gérer les requêtes HTTP de type GET. Elle est une version spécialisée de `@RequestMapping`.
- **Paramètres** :
  - `value` ou `path` : Le chemin URL auquel la méthode doit répondre.
  
```java
@GetMapping("/cartes/{id}")
public Card getCardById(@PathVariable int id) {
    // Code pour retourner une carte par ID
}
```

# 4. **@PostMapping**
- **Description** : Utilisée pour gérer les requêtes HTTP de type POST, qui sont généralement utilisées pour créer de nouvelles ressources.
- **Paramètres** :
  - `value` ou `path` : Le chemin URL pour la requête POST.

```java
@PostMapping("/cartes")
public Card createCard(@RequestBody Card card) {
    // Code pour créer une nouvelle carte
}
```

# 5. **@RequestParam**
- **Description** : Utilisée pour extraire les paramètres de requête (query parameters) passés dans l'URL. Ces paramètres sont optionnels ou obligatoires selon la configuration.
- **Paramètres** :
  - `value` : Le nom du paramètre dans l'URL.
  - `required` : Indique si le paramètre est obligatoire (par défaut `true`).

```java
@GetMapping("/cartes")
public List<Card> getCardsByType(@RequestParam(name = "type", required = false) String type) {
    // Code pour retourner les cartes selon le type (si fourni)
}
```

# 6. **@RequestBody**
- **Description** : Cette annotation est utilisée pour lier le corps de la requête HTTP à un objet Java. Elle est typiquement utilisée dans les requêtes POST ou PUT, où le client envoie des données JSON/XML qui doivent être converties en objets Java.

```java
@PostMapping("/cartes")
public Card addCard(@RequestBody Card newCard) {
    // Code pour ajouter une nouvelle carte en utilisant les données envoyées dans le corps de la requête
}
```

# 7. **@PathVariable**
- **Description** : Utilisée pour extraire des variables directement de l’URL (souvent utilisé pour des identifiants).
- **Paramètres** :
  - `value` : Le nom de la variable dans l'URL.

```java
@GetMapping("/cartes/{id}")
public Card getCard(@PathVariable("id") int cardId) {
    // Code pour récupérer une carte avec un ID spécifique
}
```

# Exemple Complet

```java
@RestController
@RequestMapping("/cartes")
public class CardController {

    @GetMapping("/{id}")
    public Card getCardById(@PathVariable int id) {
        // Code pour récupérer une carte par ID
    }

    @PostMapping
    public Card createCard(@RequestBody Card card) {
        // Code pour créer une nouvelle carte
    }

    @GetMapping
    public List<Card> getCardsByType(@RequestParam(name = "type", required = false) String type) {
        // Code pour récupérer des cartes selon le type, si fourni
    }
}
```

Cet exemple montre comment utiliser ces annotations pour gérer des requêtes HTTP GET et POST, extraire des paramètres depuis l'URL ou le corps de la requête, et renvoyer les réponses sous forme d'objets Java.



------------
# Annexe - **Exemple d’utilisation de `@RequestMapping` au niveau de la classe**
------------

Voici un exemple d'utilisation de l'annotation `@RequestMapping` pour une **classe** et pour une **méthode** :



Lorsqu'on utilise `@RequestMapping` sur une classe, cela définit une URL de base (ou chemin racine) pour toutes les méthodes de la classe. Chaque méthode pourra ensuite utiliser des sous-chemins pour répondre à différentes requêtes.

```java
@RestController
@RequestMapping("/cartes")
public class CardController {

    // Cette méthode répondra aux requêtes GET sur l'URL /cartes/hello
    @GetMapping("/hello")
    public String helloCard() {
        return "Hello, Card!";
    }

    // Cette méthode répondra aux requêtes GET sur l'URL /cartes/{id}
    @GetMapping("/{id}")
    public Card getCardById(@PathVariable int id) {
        // Code pour retourner une carte par ID
        return new Card(id, "1234-5678-9012-3456", "Visa");
    }
}
```

#### Explication :
- L'annotation `@RequestMapping("/cartes")` au niveau de la **classe** associe toutes les requêtes commençant par `/cartes` à ce contrôleur.
- Chaque méthode définit ensuite un chemin relatif (par exemple, `/hello` ou `/{id}`), qui est ajouté au chemin racine défini par `@RequestMapping` sur la classe.

### 2. **Exemple d’utilisation de `@RequestMapping` au niveau de la méthode**

On peut aussi utiliser `@RequestMapping` directement sur une méthode pour associer une URL et un type de requête HTTP spécifique à cette méthode.

```java
@RestController
public class CardController {

    // Cette méthode répondra aux requêtes GET sur l'URL /cartes
    @RequestMapping(value = "/cartes", method = RequestMethod.GET)
    public List<Card> getAllCards() {
        // Code pour retourner toutes les cartes
        return List.of(
            new Card(1, "1234-5678-9012-3456", "Visa"),
            new Card(2, "9876-5432-1098-7654", "MasterCard")
        );
    }

    // Cette méthode répondra aux requêtes POST sur l'URL /cartes
    @RequestMapping(value = "/cartes", method = RequestMethod.POST)
    public Card createCard(@RequestBody Card newCard) {
        // Code pour créer une nouvelle carte
        return newCard; // Juste pour l'exemple
    }
}
```

#### Explication :
- L'annotation `@RequestMapping` au niveau de la **méthode** permet d'associer cette méthode à une URL spécifique (ici, `/cartes`), ainsi qu'à un type de requête HTTP (`GET` ou `POST` dans cet exemple).
- Cela permet d'avoir plus de contrôle granulaire sur les routes gérées par chaque méthode.

### Différence entre les deux :
- **Niveau classe** : Utiliser `@RequestMapping` sur une classe permet de définir une URL de base pour toutes les méthodes de cette classe.
- **Niveau méthode** : Utiliser `@RequestMapping` sur une méthode permet d'associer une URL et un type de requête spécifique à une seule méthode.

En combinant les deux approches, tu peux organiser les routes de ton API de manière claire et intuitive.
