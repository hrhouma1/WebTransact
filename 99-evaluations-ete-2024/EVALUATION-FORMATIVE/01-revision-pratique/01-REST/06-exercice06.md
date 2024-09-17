# **Exercice 06 : Compléter les annotations et les appels API dans un contrôleur REST**

**Objectif :**  
L'objectif de cet exercice est de compléter les annotations et de configurer les appels API d'un contrôleur REST dans un système sécurisé pour la gestion des utilisateurs. Le système doit suivre les bonnes pratiques de versionnement d'API via l'usage du préfixe `/api/v1`. Vous devrez mettre en place des méthodes de gestion des utilisateurs à travers différents types de requêtes HTTP (GET, POST), avec des paramètres obligatoires et optionnels.

---

## 1. **Compléter les annotations manquantes dans le contrôleur REST**

Dans cette première partie, vous devez compléter les annotations du contrôleur REST `UserController` afin que celui-ci puisse correctement répondre aux différentes requêtes HTTP. Vous devez gérer les requêtes de type **GET** pour récupérer les informations des utilisateurs en fonction de différents critères (ID, rôle, etc.) ainsi que les requêtes **POST** pour l'ajout de nouveaux utilisateurs. 

### Contraintes :
- Utiliser les bonnes pratiques pour le versionnement d'API via le préfixe `/api/v1`.
- Gérer des paramètres obligatoires et optionnels dans les méthodes GET.
- Les annotations possibles sont fournies dans chaque section.

```java
// Compléter les annotations manquantes pour que cette classe gère les utilisateurs via des requêtes HTTP

@Possibilité 1 : @RestController
@Possibilité 2 : @Controller
@Possibilité 3 : @RequestMapping("/api/v1/utilisateurs")

public class UserController {

    // Gérer les requêtes GET pour récupérer un utilisateur par son ID avec un rôle optionnel
    @Possibilité 1 : @GetMapping("/id/{userId}")
    @Possibilité 2 : @RequestMapping(value = "/id/{userId}", method = RequestMethod.GET)

    public User getUserById(@PathVariable int userId, 
                            @RequestParam(required = false) String role) {
        return new User(userId, "Utilisateur Existant", role != null ? role : "Inconnu");
    }

    // Gérer les requêtes GET pour récupérer un utilisateur par son ID et son rôle (paramètres obligatoires)
    @Possibilité 1 : @GetMapping("/id/{userId}/role/{role}")
    @Possibilité 2 : @RequestMapping(value = "/id/{userId}/role/{role}", method = RequestMethod.GET)

    public User getUserWithRole(@PathVariable int userId, 
                                @PathVariable String role) {
        return new User(userId, "Utilisateur Existant", role);
    }

    // Gérer les requêtes POST pour ajouter un nouvel utilisateur
    @Possibilité 1 : @PostMapping("/create")
    @Possibilité 2 : @RequestMapping(value = "/create", method = RequestMethod.POST)

    public User addUser(@Possibilité 1 : @RequestBody User user) {
        return user;
    }

    // Gérer les requêtes GET avec des paramètres optionnels pour filtrer par rôle et statut
    @Possibilité 1 : @GetMapping
    @Possibilité 2 : @RequestMapping(method = RequestMethod.GET)

    public List<User> getUsersByRole(@RequestParam(required = false) String role, 
                                     @RequestParam(defaultValue = "false") boolean active) {
        return Arrays.asList(
            new User(1, "Alice", role != null ? role : "Admin", active),
            new User(2, "Bob", role != null ? role : "User", active)
        );
    }

    // Gérer les requêtes GET avec des paramètres obligatoires pour filtrer par rôle et statut
    @Possibilité 1 : @GetMapping("/filter")
    @Possibilité 2 : @RequestMapping(value = "/filter", method = RequestMethod.GET)

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

Vous devez maintenant proposer plusieurs possibilités d'appels API qui permettront d’interagir avec le contrôleur `UserController` mis en place. Vous utiliserez le préfixe `/api/v1` pour chaque route afin de respecter le versionnement d’API.

### 2.1 **Récupérer un utilisateur par son ID et son rôle (rôle optionnel)**

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

### 2.2 **Récupérer un utilisateur par son ID et son rôle (paramètres dans le chemin)**

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
POST http://localhost:8080/api/v1/utilisateurs/add
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "User"
}

### Possibilité 3
POST http://localhost:8080/api/v1/utilisateurs
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "User"
}

### Possibilité 4
POST http://localhost:8080/api/v1/users
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "User"
}

### Possibilité 5
POST http://localhost:8080/api/v1/utilisateurs/create-user
Content-Type: application/json

{
  "id": 3,
  "name": "Charlie",
  "role": "User"
}
```

---

### 2.4 **Récupérer une liste d'utilisateurs par rôle et statut actif (paramètres optionnels)**

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

### Conclusion :

Ce projet vous permettra de :
- Gérer différentes méthodes HTTP (**GET**, **POST**) dans un contrôleur REST en respectant les bonnes pratiques de versionnement.
- Comprendre la gestion de paramètres dans les URLs, qu’ils soient obligatoires ou optionnels.
- Travailler avec des appels API dans un environnement sécurisé et versionné via `/api/v1`.




# Annexe 1 - Correction du contrôleur pour prendre en charge les paramètres `role` et `active` dans les requêtes GET

```java
// Compléter les annotations manquantes pour que cette classe gère les utilisateurs via des requêtes HTTP

@RestController
@RequestMapping("/api/v1/utilisateurs")
public class UserController {

    // Gérer les requêtes GET avec des paramètres optionnels (role et active)
    @GetMapping
    public List<User> getUsersByRoleAndStatus(@RequestParam(required = false) String role, 
                                              @RequestParam(defaultValue = "false") boolean active) {
        // Simulation de la logique de récupération des utilisateurs
        return Arrays.asList(
            new User(1, "Alice", role != null ? role : "Admin", active),
            new User(2, "Bob", role != null ? role : "User", active)
        );
    }

    // Gérer les requêtes GET pour récupérer un utilisateur par son ID avec un rôle optionnel
    @GetMapping("/id/{userId}")
    public User getUserById(@PathVariable int userId, 
                            @RequestParam(required = false) String role) {
        return new User(userId, "Utilisateur Existant", role != null ? role : "Inconnu");
    }

    // Gérer les requêtes POST pour ajouter un nouvel utilisateur
    @PostMapping("/create")
    public User addUser(@RequestBody User user) {
        return user;
    }
}
```

### Détails des méthodes :
1. **`getUsersByRoleAndStatus()`** : Cette méthode accepte deux paramètres optionnels :
   - `role` : Spécifie le rôle de l'utilisateur (par exemple, Admin, User, etc.).
   - `active` : Un paramètre boolean (vrai ou faux) qui indique si l'utilisateur est actif.
   
   Si les deux paramètres sont présents dans la requête, la méthode les utilisera pour filtrer les résultats.

2. **`getUserById()`** : Cette méthode accepte un paramètre obligatoire dans le chemin (userId) et un paramètre optionnel `role` dans la requête.

3. **`addUser()`** : Méthode POST pour ajouter un nouvel utilisateur.

---

### Appels API correspondants

#### **Récupérer une liste d'utilisateurs par rôle et statut actif (paramètres optionnels)**

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

### Explication :
- La méthode **`getUsersByRoleAndStatus`** est maintenant bien alignée avec les appels API tels que `GET http://localhost:8080/api/v1/utilisateurs?role=User&active=false`.
- Si les paramètres `role` et `active` ne sont pas fournis, des valeurs par défaut sont utilisées (par exemple, `role="Admin"` et `active=false`).
  

