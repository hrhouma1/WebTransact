# Les services web avec spring-boot

- `spring-boot-starter-web` est une dépendance de Spring Boot qui fournit les composants nécessaires pour développer des applications web, y compris les API REST. Il inclut des outils pour gérer les requêtes HTTP, JSON, des contrôleurs REST, et un serveur intégré (comme Tomcat).
- `@RestController` est une annotation Spring qui combine `@Controller` et `@ResponseBody`. 
- Elle indique qu'une classe va gérer des requêtes HTTP REST, en renvoyant directement les réponses (généralement en JSON ou XML) sans passer par une vue (interface utilisateur). 
- Elle est utilisée pour construire des API REST où chaque méthode répond à une requête HTTP (GET, POST, PUT, DELETE).


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

- Cet exemple présenté ci-haut montre comment utiliser ces annotations pour gérer des requêtes HTTP GET et POST, extraire des paramètres depuis l'URL ou le corps de la requête, et renvoyer les réponses sous forme d'objets Java.



------------
# Annexe 1 - **Exemple d’utilisation de `@RequestMapping` au niveau de la classe**
------------

# Exemple d'utilisation de l'annotation `@RequestMapping` pour une **classe** et pour une **méthode** :



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


---
# Annexe 2 -
---


Pour compléter ton exemple avec des requêtes `GET`, `POST`, `PUT`, et `DELETE`, voici un modèle complet qui illustre les différentes opérations CRUD (Create, Read, Update, Delete) dans un contrôleur Spring Boot. 

### 1. **GET** - Récupérer une carte par ID
```java
@GetMapping("/{id}")
public ResponseEntity<Card> getCardById(@PathVariable int id) {
    // Code pour récupérer une carte par son ID
    Card card = cardService.findCardById(id);
    return ResponseEntity.ok(card);
}
```

#### Exécution:
```bash
GET /cartes/1
```

#### Réponse JSON:
```json
{
  "id": 1,
  "number": "1234-5678-9012-3456",
  "type": "Visa"
}
```

---

### 2. **POST** - Créer une nouvelle carte
```java
@PostMapping
public ResponseEntity<Card> createCard(@RequestBody Card card) {
    // Code pour créer une nouvelle carte
    Card newCard = cardService.saveCard(card);
    return ResponseEntity.status(HttpStatus.CREATED).body(newCard);
}
```

#### Exécution:
```bash
POST /cartes
Content-Type: application/json

{
  "number": "1111-2222-3333-4444",
  "type": "MasterCard"
}
```

#### Réponse JSON:
```json
{
  "id": 2,
  "number": "1111-2222-3333-4444",
  "type": "MasterCard"
}
```

---

### 3. **PUT** - Mettre à jour une carte existante
```java
@PutMapping("/{id}")
public ResponseEntity<Card> updateCard(@PathVariable int id, @RequestBody Card cardDetails) {
    // Code pour mettre à jour une carte par ID
    Card updatedCard = cardService.updateCard(id, cardDetails);
    return ResponseEntity.ok(updatedCard);
}
```

#### Exécution:
```bash
PUT /cartes/1
Content-Type: application/json

{
  "number": "9876-5432-1098-7654",
  "type": "Visa"
}
```

#### Réponse JSON:
```json
{
  "id": 1,
  "number": "9876-5432-1098-7654",
  "type": "Visa"
}
```

---

### 4. **DELETE** - Supprimer une carte par ID
```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteCard(@PathVariable int id) {
    // Code pour supprimer une carte par ID
    cardService.deleteCardById(id);
    return ResponseEntity.noContent().build();
}
```

#### Exécution:
```bash
DELETE /cartes/1
```

#### Réponse:
```json
{
  "message": "Carte supprimée avec succès"
}
```

---
# Exemple  avec les 4 méthodes dans un contrôleur `RestController` :
---


```java
@RestController
@RequestMapping("/cartes")
public class CardController {

    @GetMapping("/{id}")
    public ResponseEntity<Card> getCardById(@PathVariable int id) {
        Card card = cardService.findCardById(id);
        return ResponseEntity.ok(card);
    }

    @PostMapping
    public ResponseEntity<Card> createCard(@RequestBody Card card) {
        Card newCard = cardService.saveCard(card);
        return ResponseEntity.status(HttpStatus.CREATED).body(newCard);
    }

    @PutMapping("/{id}")
    public ResponseEntity<Card> updateCard(@PathVariable int id, @RequestBody Card cardDetails) {
        Card updatedCard = cardService.updateCard(id, cardDetails);
        return ResponseEntity.ok(updatedCard);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteCard(@PathVariable int id) {
        cardService.deleteCardById(id);
        return ResponseEntity.noContent().build();
    }
}
```

### Modèles JSON de requête pour POST et PUT :
- **POST** (Créer une nouvelle carte):
  ```json
  {
    "number": "1111-2222-3333-4444",
    "type": "MasterCard"
  }
  ```

- **PUT** (Mettre à jour une carte existante):
  ```json
  {
    "number": "9876-5432-1098-7654",
    "type": "Visa"
  }
  ```

Ces exemples montrent comment manipuler les opérations CRUD avec un contrôleur Spring, incluant la gestion du corps JSON via `@RequestBody` et la gestion des URL variables avec `@PathVariable`.
