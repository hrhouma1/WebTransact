# PARTIE 01

1. **Que fait l'annotation `@RestController` dans Spring Boot ?**
   - A) Elle configure une vue pour afficher les réponses.
   - B) Elle permet de gérer les requêtes HTTP REST et de renvoyer des données directement.
   - C) Elle associe une méthode à une URL spécifique.

2. **Laquelle des affirmations suivantes est vraie concernant `@RequestMapping` ?**
   - A) Elle est utilisée uniquement pour les méthodes GET.
   - B) Elle peut être utilisée pour associer une classe ou une méthode à un chemin URL.
   - C) Elle est nécessaire uniquement pour gérer des requêtes POST.

3. **Quelle est la différence entre `@GetMapping` et `@PostMapping` ?**
   - A) `@GetMapping` est utilisé pour récupérer des données, tandis que `@PostMapping` est utilisé pour envoyer des données au serveur.
   - B) `@GetMapping` est plus rapide que `@PostMapping`.
   - C) Il n'y a pas de différence.

4. **L'annotation `@RequestParam` est utilisée pour :**
   - A) Récupérer des variables d'URL dans le corps de la requête.
   - B) Extraire des paramètres de requête depuis l'URL (query parameters).
   - C) Renvoyer une vue personnalisée.

5. **Que fait l'annotation `@RequestBody` ?**
   - A) Elle associe une méthode à un chemin spécifique.
   - B) Elle permet de lier le corps de la requête HTTP à un objet Java.
   - C) Elle envoie une réponse JSON au client.

6. **À quoi sert `@PathVariable` dans une méthode Spring Boot ?**
   - A) À extraire des variables directement de l'URL.
   - B) À envoyer une variable au serveur depuis le client.
   - C) À définir un chemin fixe pour une méthode.

7. **Quelle méthode HTTP est généralement utilisée pour mettre à jour une ressource ?**
   - A) GET
   - B) POST
   - C) PUT

8. **Dans quel cas utiliseriez-vous `@DeleteMapping` ?**
   - A) Pour supprimer une ressource du serveur.
   - B) Pour récupérer une ressource.
   - C) Pour envoyer une requête avec un corps JSON.

9. **Que renvoie une méthode annotée avec `@PostMapping` par défaut si l'opération est réussie ?**
   - A) Un statut HTTP 200 (OK).
   - B) Un statut HTTP 201 (Created).
   - C) Un statut HTTP 404 (Not Found).

10. **Quel est le rôle de `@RequestMapping` lorsqu'il est appliqué à une classe entière ?**
    - A) Il permet de renvoyer une vue personnalisée.
    - B) Il définit un chemin de base pour toutes les méthodes de la classe.
    - C) Il associe chaque méthode de la classe à une URL différente automatiquement.

-------------------------------------------------
-------------------------------------------------
-------------------------------------------------


# PARTIE 02

11. **Que fait l'annotation `@GetMapping("/cartes/{id}")` dans cet exemple ?**
    ```java
    @GetMapping("/cartes/{id}")
    public Card getCardById(@PathVariable int id) {
        // Code pour récupérer une carte par ID
    }
    ```
    - A) Elle gère une requête POST à l'URL `/cartes/{id}`.
    - B) Elle gère une requête GET à l'URL `/cartes/{id}` et récupère l'ID à partir de l'URL.
    - C) Elle gère une requête DELETE à l'URL `/cartes/{id}`.

12. **Dans l'exemple ci-dessous, que fait `@RequestParam("type")` ?**
    ```java
    @GetMapping("/cartes")
    public List<Card> getCardsByType(@RequestParam("type") String type) {
        // Code pour retourner les cartes par type
    }
    ```
    - A) Il indique que le type est obligatoire et doit être extrait de l'URL.
    - B) Il indique que le paramètre `type` est extrait du corps de la requête.
    - C) Il ignore le paramètre `type` si celui-ci est absent.

13. **Que fait l'annotation `@PostMapping` dans cet exemple ?**
    ```java
    @PostMapping("/cartes")
    public Card createCard(@RequestBody Card card) {
        // Code pour créer une nouvelle carte
    }
    ```
    - A) Elle gère une requête GET pour créer une nouvelle carte.
    - B) Elle gère une requête POST pour créer une nouvelle carte à partir des données envoyées dans le corps de la requête.
    - C) Elle gère une requête DELETE pour supprimer une carte.

14. **Dans l'exemple suivant, pourquoi utilise-t-on `@RequestBody` ?**
    ```java
    @PostMapping("/cartes")
    public Card addCard(@RequestBody Card newCard) {
        // Code pour ajouter une nouvelle carte
    }
    ```
    - A) Pour extraire les données de la requête sous forme de paramètres de l'URL.
    - B) Pour extraire les données JSON envoyées dans le corps de la requête et les convertir en objet `Card`.
    - C) Pour renvoyer une réponse au format XML.

15. **Que fait l'annotation `@PutMapping("/{id}")` dans cet exemple ?**
    ```java
    @PutMapping("/cartes/{id}")
    public Card updateCard(@PathVariable int id, @RequestBody Card card) {
        // Code pour mettre à jour une carte
    }
    ```
    - A) Elle gère une requête PUT pour mettre à jour une carte avec l'ID fourni dans l'URL.
    - B) Elle gère une requête POST pour créer une nouvelle carte.
    - C) Elle gère une requête GET pour récupérer une carte.

16. **Quelle est la fonction de `@DeleteMapping("/{id}")` dans cet exemple ?**
    ```java
    @DeleteMapping("/cartes/{id}")
    public void deleteCard(@PathVariable int id) {
        // Code pour supprimer une carte
    }
    ```
    - A) Elle gère une requête GET pour récupérer une carte par ID.
    - B) Elle gère une requête DELETE pour supprimer une carte avec l'ID fourni dans l'URL.
    - C) Elle gère une requête POST pour supprimer une carte.

17. **Que se passe-t-il si on utilise `@RequestMapping(value = "/cartes", method = RequestMethod.GET)` au lieu de `@GetMapping("/cartes")` ?**
    ```java
    @RequestMapping(value = "/cartes", method = RequestMethod.GET)
    public List<Card> getAllCards() {
        // Code pour récupérer toutes les cartes
    }
    ```
    - A) Il n'y a aucune différence, les deux annotations fonctionnent de la même manière.
    - B) `@RequestMapping` n'est pas compatible avec les méthodes GET.
    - C) `@RequestMapping` est utilisé uniquement pour les méthodes POST.

18. **Dans cet exemple, comment le paramètre `id` est-il transmis à la méthode ?**
    ```java
    @GetMapping("/cartes/{id}")
    public Card getCardById(@PathVariable("id") int cardId) {
        // Code pour récupérer une carte par ID
    }
    ```
    - A) Le paramètre est extrait du corps de la requête HTTP.
    - B) Le paramètre est extrait directement de l'URL grâce à l'annotation `@PathVariable`.
    - C) Le paramètre est automatiquement rempli par Spring à partir d'une session.

19. **Pourquoi utilise-t-on `@ResponseStatus(HttpStatus.NO_CONTENT)` dans cet exemple ?**
    ```java
    @DeleteMapping("/cartes/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void deleteCard(@PathVariable int id) {
        // Code pour supprimer une carte
    }
    ```
    - A) Pour spécifier que la méthode renvoie une réponse HTTP avec le statut "204 No Content" après avoir supprimé une carte.
    - B) Pour indiquer que la méthode n'attend pas de réponse de la part du client.
    - C) Pour dire que la méthode renverra une vue HTML vide.

20. **Que se passe-t-il si l'on omet `@RequestBody` dans cet exemple ?**
    ```java
    @PostMapping("/cartes")
    public Card createCard(Card card) {
        // Code pour créer une nouvelle carte
    }
    ```
    - A) Spring renverra une erreur car il ne pourra pas lier le corps de la requête à l'objet `Card`.
    - B) Spring récupérera automatiquement les données JSON du corps de la requête.
    - C) Cela n'a aucun impact sur la requête.



------------------------------
------------------------------
------------------------------


# PARTIE 03

### **Instructions :**  
Pour chaque question, complétez les annotations manquantes ou proposez l’appel API correct. L'objectif est de vous assurer que vous maîtrisez la mise en place des bonnes annotations et que vous savez formuler correctement les appels API REST.

---

### 1. **Compléter l'annotation manquante pour gérer une requête GET**
  
Complétez l'annotation pour une méthode qui récupère un utilisateur via son **ID**.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/utilisateurs/id/{userId}
public User getUserById(@PathVariable int userId) {
    // Retourne les détails de l'utilisateur par son ID
}
```
**Options :**
- A) `@PostMapping("/id/{userId}")`
- B) `@GetMapping("/id/{userId}")`
- C) `@RequestMapping("/id/{userId}")`

---

### 2. **Compléter l'annotation pour gérer une requête POST**

Complétez l'annotation pour une méthode qui permet d'ajouter un utilisateur.

```java
// Complétez l'annotation ici pour gérer une requête POST à l'URL : /api/v1/utilisateurs/create
public User addUser(@RequestBody User user) {
    // Logique pour ajouter un utilisateur
}
```

**Options :**
- A) `@GetMapping("/create")`
- B) `@PutMapping("/create")`
- C) `@PostMapping("/create")`

---

### 3. **Compléter l'annotation pour gérer une requête GET avec des paramètres optionnels**

Complétez l'annotation pour une méthode qui récupère les utilisateurs en fonction de leur **rôle** (optionnel) et de leur statut **actif**.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/utilisateurs
public List<User> getUsersByRole(@RequestParam(required = false) String role, 
                                 @RequestParam(defaultValue = "false") boolean active) {
    // Logique pour filtrer les utilisateurs par rôle et statut
}
```

**Options :**
- A) `@GetMapping`
- B) `@PostMapping`
- C) `@DeleteMapping`

---

### 4. **Quel appel API permet de récupérer un utilisateur avec ID 3 et rôle "Admin" ?**

Choisissez l'appel API correct pour récupérer un utilisateur ayant l'ID 3 et le rôle **Admin**.

**Options :**
- A) `GET http://localhost:8080/api/v1/utilisateurs/id/3?role=Admin`
- B) `POST http://localhost:8080/api/v1/utilisateurs/id/3?role=Admin`
- C) `PUT http://localhost:8080/api/v1/utilisateurs/id/3?role=Admin`

---

### 5. **Compléter l'annotation pour gérer une requête DELETE**

Complétez l'annotation pour une méthode qui permet de **supprimer** un utilisateur via son **ID**.

```java
// Complétez l'annotation ici pour gérer une requête DELETE à l'URL : /api/v1/utilisateurs/id/{userId}
public void deleteUser(@PathVariable int userId) {
    // Logique pour supprimer un utilisateur
}
```

**Options :**
- A) `@DeleteMapping("/id/{userId}")`
- B) `@GetMapping("/id/{userId}")`
- C) `@PutMapping("/id/{userId}")`

---

### 6. **Quel appel API permet de créer un nouvel utilisateur ?**

Quel est l'appel API correct pour **ajouter un utilisateur** avec les données suivantes : `id: 4, name: "David", role: "Manager"` ?

**Options :**
- A) `POST http://localhost:8080/api/v1/utilisateurs/create`
```json
{
  "id": 4,
  "name": "David",
  "role": "Manager"
}
```
- B) `GET http://localhost:8080/api/v1/utilisateurs/create`
```json
{
  "id": 4,
  "name": "David",
  "role": "Manager"
}
```
- C) `DELETE http://localhost:8080/api/v1/utilisateurs/create`
```json
{
  "id": 4,
  "name": "David",
  "role": "Manager"
}
```

---

### 7. **Quel appel API permet de récupérer une liste d'utilisateurs actifs avec le rôle "User" ?**

Choisissez l'appel API correct pour récupérer des utilisateurs ayant le rôle **User** et étant **actifs**.

**Options :**
- A) `GET http://localhost:8080/api/v1/utilisateurs?role=User&active=true`
- B) `POST http://localhost:8080/api/v1/utilisateurs?role=User&active=true`
- C) `PUT http://localhost:8080/api/v1/utilisateurs?role=User&active=true`

---

### 8. **Compléter l'annotation pour récupérer un utilisateur par son ID et rôle (obligatoire)**

Complétez l'annotation pour une méthode qui récupère un utilisateur via son **ID** et son **rôle**, ces deux paramètres étant obligatoires.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/utilisateurs/id/{userId}/role/{role}
public User getUserWithRole(@PathVariable int userId, 
                            @PathVariable String role) {
    // Logique pour récupérer l'utilisateur par son ID et rôle
}
```

**Options :**
- A) `@GetMapping("/id/{userId}/role/{role}")`
- B) `@PostMapping("/id/{userId}/role/{role}")`
- C) `@DeleteMapping("/id/{userId}/role/{role}")`

---

### 9. **Quel appel API permet de supprimer un utilisateur avec l'ID 5 ?**

Choisissez l'appel API correct pour **supprimer** un utilisateur ayant l'ID 5.

**Options :**
- A) `DELETE http://localhost:8080/api/v1/utilisateurs/id/5`
- B) `GET http://localhost:8080/api/v1/utilisateurs/id/5`
- C) `POST http://localhost:8080/api/v1/utilisateurs/id/5`

---

### 10. **Compléter l'annotation pour récupérer des utilisateurs avec des paramètres obligatoires**

Complétez l'annotation pour une méthode qui récupère les utilisateurs avec des paramètres obligatoires pour le **rôle** et le **statut actif**.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/utilisateurs/filter
public List<User> getUsersByRoleAndStatus(@RequestParam String role, 
                                          @RequestParam boolean active) {
    // Logique pour récupérer les utilisateurs par rôle et statut
}
```

**Options :**
- A) `@GetMapping("/filter")`
- B) `@PostMapping("/filter")`
- C) `@PutMapping("/filter")`


------------------------------
------------------------------
------------------------------


# PARTIE 04 - Annotations et API avec paramètres et variables dans l'URL


# Objectif: 
- Gérer des **paramètres optionnels**, des **ID optionnels**, et des **URL avec plusieurs variables** dans un contrôleur REST Spring Boot.



# 1. **Compléter l'annotation pour une méthode avec paramètres optionnels**

Complétez l'annotation pour une méthode qui récupère une liste d'utilisateurs en fonction de leur **rôle** (optionnel) et de leur **statut actif** (optionnel avec une valeur par défaut).

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/users
public List<User> getUsers(@RequestParam(required = false) String role, 
                           @RequestParam(defaultValue = "false") boolean active) {
    // Logique pour récupérer les utilisateurs
}
```

**Options :**
- A) `@PostMapping`
- B) `@GetMapping`
- C) `@PutMapping`

---

# 2. **Quel appel API permet de récupérer des utilisateurs actifs avec le rôle "Admin" ?**

Choisissez l'appel API correct pour récupérer les utilisateurs ayant le rôle **Admin** et étant **actifs** (les paramètres étant optionnels).

**Options :**
- A) `GET http://localhost:8080/api/v1/users?role=Admin&active=true`
- B) `POST http://localhost:8080/api/v1/users?role=Admin&active=true`
- C) `DELETE http://localhost:8080/api/v1/users?role=Admin&active=true`

---

# 3. **Compléter l'annotation pour une méthode avec ID optionnel**

Complétez l'annotation pour une méthode qui récupère un utilisateur par son **ID** (paramètre optionnel) ou bien retourne tous les utilisateurs si aucun ID n'est fourni.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/users/{userId}
public List<User> getUsers(@PathVariable(required = false) Integer userId) {
    // Logique pour récupérer un utilisateur ou tous les utilisateurs
}
```

**Options :**
- A) `@GetMapping("/users/{userId}")`
- B) `@PostMapping("/users/{userId}")`
- C) `@DeleteMapping("/users/{userId}")`

---

# 4. **Quel appel API permet de récupérer un utilisateur avec ID 5 ?**

Choisissez l'appel API correct pour récupérer l'utilisateur ayant l'ID **5**, sachant que l'ID est optionnel dans l'URL.

**Options :**
- A) `GET http://localhost:8080/api/v1/users/5`
- B) `POST http://localhost:8080/api/v1/users/5`
- C) `PUT http://localhost:8080/api/v1/users/5`

---

# 5. **Compléter l'annotation pour une méthode avec plusieurs variables dans l'URL**

Complétez l'annotation pour une méthode qui récupère un utilisateur via son **ID**, son **rôle**, et son **statut** (tous obligatoires).

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/users/{userId}/role/{role}/status/{status}
public User getUserByRoleAndStatus(@PathVariable int userId, 
                                   @PathVariable String role, 
                                   @PathVariable String status) {
    // Logique pour récupérer l'utilisateur par son ID, rôle et statut
}
```

**Options :**
- A) `@GetMapping("/users/{userId}/role/{role}/status/{status}")`
- B) `@PostMapping("/users/{userId}/role/{role}/status/{status}")`
- C) `@DeleteMapping("/users/{userId}/role/{role}/status/{status}")`

---

# 6. **Quel appel API permet de récupérer un utilisateur avec ID 3, rôle "Admin" et statut "active" ?**

Choisissez l'appel API correct pour récupérer un utilisateur ayant l'ID **3**, le rôle **Admin**, et le statut **active**.

**Options :**
- A) `GET http://localhost:8080/api/v1/users/3/role/Admin/status/active`
- B) `POST http://localhost:8080/api/v1/users/3/role/Admin/status/active`
- C) `DELETE http://localhost:8080/api/v1/users/3/role/Admin/status/active`

---

# 7. **Quel appel API permet de récupérer tous les utilisateurs, sans fournir d'ID ?**

Choisissez l'appel API correct pour récupérer **tous les utilisateurs**, sachant que l'ID est optionnel.

**Options :**
- A) `GET http://localhost:8080/api/v1/users`
- B) `POST http://localhost:8080/api/v1/users`
- C) `DELETE http://localhost:8080/api/v1/users`

---

# 8. **Compléter l'annotation pour une méthode avec plusieurs paramètres et variables dans l'URL**

Complétez l'annotation pour une méthode qui accepte **trois** variables dans l'URL : `userId`, `role`, et `department`.

```java
// Complétez l'annotation ici pour gérer une requête GET à l'URL : /api/v1/users/{userId}/role/{role}/department/{department}
public User getUserDetails(@PathVariable int userId, 
                           @PathVariable String role, 
                           @PathVariable String department) {
    // Logique pour récupérer les détails de l'utilisateur
}
```

**Options :**
- A) `@GetMapping("/users/{userId}/role/{role}/department/{department}")`
- B) `@PostMapping("/users/{userId}/role/{role}/department/{department}")`
- C) `@DeleteMapping("/users/{userId}/role/{role}/department/{department}")`




---------------------------------------------------
---------------------------------------------------
---------------------------------------------------

# Annexe 01 

### Exercice 06 : Compléter les annotations et les appels API dans un contrôleur REST

**Objectif :**  
L'objectif est de compléter les annotations dans un contrôleur REST pour la gestion des utilisateurs via des requêtes HTTP, tout en suivant les bonnes pratiques du versionnement d'API avec `/api/v1`. Vous devez gérer différents types de requêtes (GET, POST) et configurer les paramètres obligatoires et optionnels dans ces méthodes.

---

## 1. **Compléter les annotations manquantes dans le contrôleur REST**

Complétez les annotations du contrôleur `UserController` pour gérer les utilisateurs via des requêtes GET et POST. Voici quelques exemples de routes, où vous devrez décider des annotations à utiliser :

```java
@RestController // Possibilité 1 : @RestController | Possibilité 2 : @Controller
@RequestMapping("/api/v1/utilisateurs")
public class UserController {

    // Méthode GET pour récupérer un utilisateur par ID, avec un rôle optionnel
    @GetMapping("/id/{userId}")
    public User getUserById(@PathVariable int userId, 
                            @RequestParam(required = false) String role) {
        return new User(userId, "Utilisateur Existant", role != null ? role : "Inconnu");
    }

    // Méthode GET pour récupérer un utilisateur par ID et rôle, paramètres obligatoires
    @GetMapping("/id/{userId}/role/{role}")
    public User getUserWithRole(@PathVariable int userId, 
                                @PathVariable String role) {
        return new User(userId, "Utilisateur Existant", role);
    }

    // Méthode POST pour ajouter un nouvel utilisateur
    @PostMapping("/create")
    public User addUser(@RequestBody User user) {
        return user;
    }

    // Méthode GET pour récupérer des utilisateurs selon un rôle et un statut actifs (paramètres optionnels)
    @GetMapping
    public List<User> getUsersByRole(@RequestParam(required = false) String role, 
                                     @RequestParam(defaultValue = "false") boolean active) {
        return Arrays.asList(
            new User(1, "Alice", role != null ? role : "Admin", active),
            new User(2, "Bob", role != null ? role : "User", active)
        );
    }

    // Méthode GET avec paramètres obligatoires pour rôle et statut
    @GetMapping("/filter")
    public List<User> getUsersByRoleAndStatus(@RequestParam String role, 
                                              @RequestParam boolean active) {
        return Arrays.asList(
            new User(1, "Alice", role, active),
            new User(2, "Bob", role, active)
        );
    }
}
```

---

## 2. **Proposer 5 possibilités d'appels API pour chaque méthode**

Proposez plusieurs exemples d'appels API pour chaque méthode du contrôleur `UserController`.

### 2.1 **Récupérer un utilisateur par son ID avec rôle optionnel**

- **Méthode :** `GET /id/{userId}`
```http
### Possibilité 1
GET http://localhost:8080/api/v1/utilisateurs/id/1
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/v1/utilisateurs/id/1?role=Admin
Accept: application/json

### Possibilité 3
GET http://localhost:8080/api/v1/utilisateurs/id/2?role=User
Accept: application/json

### Possibilité 4
GET http://localhost:8080/api/v1/utilisateurs/id/3
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/utilisateurs/id/4?role=Manager
Accept: application/json
```

---

### 2.2 **Récupérer un utilisateur par ID et rôle (paramètres obligatoires)**

- **Méthode :** `GET /id/{userId}/role/{role}`
```http
### Possibilité 1
GET http://localhost:8080/api/v1/utilisateurs/id/1/role/Admin
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/v1/utilisateurs/id/2/role/User
Accept: application/json

### Possibilité 3
GET http://localhost:8080/api/v1/utilisateurs/id/3/role/Manager
Accept: application/json

### Possibilité 4
GET http://localhost:8080/api/v1/utilisateurs/id/4/role/Developer
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/utilisateurs/id/5/role/CEO
Accept: application/json
```

---

### 2.3 **Ajouter un nouvel utilisateur**

- **Méthode :** `POST /create`
```http
### Possibilité 1
POST http://localhost:8080/api/v1/utilisateurs/create
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "User"
}

### Possibilité 2
POST http://localhost:8080/api/v1/utilisateurs/create
Content-Type: application/json

{
  "id": 4,
  "name": "David",
  "role": "Admin"
}

### Possibilité 3
POST http://localhost:8080/api/v1/utilisateurs/create
Content-Type: application/json

{
  "id": 5,
  "name": "Eva",
  "role": "Manager"
}

### Possibilité 4
POST http://localhost:8080/api/v1/utilisateurs/create
Content-Type: application/json

{
  "id": 6,
  "name": "Frank",
  "role": "Developer"
}

### Possibilité 5
POST http://localhost:8080/api/v1/utilisateurs/create
Content-Type: application/json

{
  "id": 7,
  "name": "George",
  "role": "CEO"
}
```

---

### 2.4 **Récupérer des utilisateurs par rôle et statut actifs (paramètres optionnels)**

- **Méthode :** `GET /`
```http
### Possibilité 1
GET http://localhost:8080/api/v1/utilisateurs?role=Admin&active=true
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/v1/utilisateurs?role=User&active=false
Accept: application/json

### Possibilité 3
GET http://localhost:8080/api/v1/utilisateurs?role=Manager
Accept: application/json

### Possibilité 4
GET http://localhost:8080/api/v1/utilisateurs?active=true
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/utilisateurs
Accept: application/json
```

---

### 2.5 **Filtrer les utilisateurs par rôle et statut (paramètres obligatoires)**

- **Méthode :** `GET /filter`
```http
### Possibilité 1
GET http://localhost:8080/api/v1/utilisateurs/filter?role=Admin&active=true
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/v1/utilisateurs/filter?role=User&active=false
Accept: application/json

### Possibilité 3
GET http://localhost:8080/api/v1/utilisateurs/filter?role=Manager&active=true
Accept: application/json

### Possibilité 4
GET http://localhost:8080/api/v1/utilisateurs/filter?role=Developer&active=false
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/utilisateurs/filter?role=CEO&active=true
Accept: application/json
```

---

### Conclusion :
Cet exercice vous aidera à configurer les bonnes annotations pour vos méthodes et à comprendre comment structurer vos routes d'API REST en suivant les bonnes pratiques de versionnement avec `/api/v1`. Vous apprendrez également à gérer des paramètres optionnels et obligatoires dans vos routes.



---------------------------------------------------
---------------------------------------------------
---------------------------------------------------

# Annexe 02 - Exemple avec paramètres optionnels

Dans cet exemple, les paramètres `role` et `active` sont optionnels :

#### Méthode Java :
```java
@GetMapping("/users")
public List<User> getUsers(@RequestParam(required = false) String role, 
                           @RequestParam(defaultValue = "false") boolean active) {
    return userService.findUsers(role, active);
}
```

#### Appels API possibles :
```http
### Possibilité 1 (avec les deux paramètres optionnels)
GET http://localhost:8080/api/v1/users?role=Admin&active=true
Accept: application/json

### Possibilité 2 (avec seulement le paramètre 'active')
GET http://localhost:8080/api/v1/users?active=false
Accept: application/json

### Possibilité 3 (sans aucun paramètre)
GET http://localhost:8080/api/v1/users
Accept: application/json
```

---

### 2. **Exemple avec ID optionnel**

Dans cet exemple, l'ID de l'utilisateur est optionnel, et si non fourni, tous les utilisateurs sont retournés :

#### Méthode Java :
```java
@GetMapping("/users/{userId}")
public List<User> getUsers(@PathVariable(required = false) Integer userId) {
    return userId != null ? List.of(userService.findUserById(userId)) : userService.findAllUsers();
}
```

#### Appels API possibles :
```http
### Possibilité 1 (avec ID fourni)
GET http://localhost:8080/api/v1/users/1
Accept: application/json

### Possibilité 2 (sans ID, tous les utilisateurs sont retournés)
GET http://localhost:8080/api/v1/users
Accept: application/json
```

---

### 3. **Exemple avec au moins 3 variables dans l'URL**

Ici, les paramètres **userId**, **role**, et **status** sont tous obligatoires dans l'URL :

#### Méthode Java :
```java
@GetMapping("/users/{userId}/role/{role}/status/{status}")
public User getUserByRoleAndStatus(@PathVariable int userId, 
                                   @PathVariable String role, 
                                   @PathVariable String status) {
    return userService.findUser(userId, role, status);
}
```

#### Appels API possibles :
```http
### Possibilité 1
GET http://localhost:8080/api/v1/users/1/role/Admin/status/active
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/v1/users/2/role/Manager/status/inactive
Accept: application/json
```

---

Ces exemples couvrent des cas avec **paramètres optionnels**, **ID optionnel**, et des **routes complexes** avec plusieurs variables dans l'URL.
