# **Examen Partie 1 : Gestion d'une Librairie en ligne avec API REST**

# **Contexte :**
Dans cet exercice, vous allez travailler sur la gestion d'une librairie en ligne à l'aide d'une API REST. Vous devez compléter les annotations et les méthodes d'un contrôleur qui permet de gérer les livres disponibles dans la librairie, ainsi que d'autres fonctionnalités liées à la gestion des livres, comme l'ajout de nouveaux ouvrages, la mise à jour de leurs informations, et la récupération de détails spécifiques.

Dans la partie 1 de l'exercice 1, vous devrez choisir la ou les bonne(s) annotations pour exposer les méthodes du contrôleur et proposer des appels API qui pourraient être utilisés pour interagir avec l'inventaire de la librairie.

---

# **Exercice 01 : Compléter les annotations et les appels API**

L'objectif de cet exercice est de compléter les annotations nécessaires dans un contrôleur REST pour gérer les livres de la librairie. Vous devrez aussi proposer des appels API appropriés pour chaque méthode.

---

# Partie 1. Compléter les annotations manquantes pour que cette classe réponde aux requêtes HTTP
# 📢

```java
// Compléter les annotations appropriées pour gérer les livres via des requêtes HTTP

@Possibilité 1 : @RestController  
@Possibilité 2 : @Controller  
@Possibilité 3 : @Service  
@Possibilité 4 : @Component  
@Possibilité 5 : @RequestMapping("/livres")

public class LivreController {

    // Gérer les requêtes GET pour lister tous les livres disponibles
    @Possibilité 1 : @GetMapping  
    @Possibilité 2 : @RequestMapping(method = RequestMethod.GET)  
    @Possibilité 3 : @PostMapping  
    @Possibilité 4 : @PutMapping  
    @Possibilité 5 : @DeleteMapping  

    public List<Livre> getAllBooks() {
        return Arrays.asList(
            new Livre(1, "1984", "George Orwell"),
            new Livre(2, "Le Petit Prince", "Antoine de Saint-Exupéry")
        );
    }

    // Gérer les requêtes POST pour ajouter un nouveau livre
    @Possibilité 1 : @PostMapping("/ajouter")  
    @Possibilité 2 : @RequestMapping(value = "/ajouter", method = RequestMethod.POST)  
    @Possibilité 3 : @PutMapping("/ajouter")  
    @Possibilité 4 : @DeleteMapping("/ajouter")  
    @Possibilité 5 : @PatchMapping("/ajouter")  

    public Livre addBook(@Possibilité 1 : @RequestBody Livre livre, 
                         @Possibilité 2 : @ModelAttribute Livre livre, 
                         @Possibilité 3 : @RequestParam Livre livre, 
                         @Possibilité 4 : @SessionAttribute Livre livre, 
                         @Possibilité 5 : @PathVariable Livre livre) {
        return livre;
    }

    // Gérer les requêtes GET pour récupérer les détails d'un livre par son ID
    @Possibilité 1 : @GetMapping("/id/{livreId}")  
    @Possibilité 2 : @RequestMapping(value = "/id/{livreId}", method = RequestMethod.GET)  
    @Possibilité 3 : @PostMapping("/id/{livreId}")  
    @Possibilité 4 : @PatchMapping("/id/{livreId}")  
    @Possibilité 5 : @DeleteMapping("/id/{livreId}")  

    public Livre getBookById(@Possibilité 1 : @PathVariable int livreId, 
                             @Possibilité 2 : @RequestParam int livreId, 
                             @Possibilité 3 : @RequestHeader int livreId, 
                             @Possibilité 4 : @CookieValue int livreId, 
                             @Possibilité 5 : @SessionAttribute int livreId) {
        return new Livre(livreId, "Titre Existant", "Auteur Inconnu");
    }
}
```

---

# Partie 2. Proposez 5 possibilités d'appels API pour chaque méthode

# **Lister tous les livres :**

```http
### Possibilité 1
GET http://localhost:8080/livres
Accept: application/json

### Possibilité 2
GET http://localhost:8080/livres
Accept: application/xml

### Possibilité 3
GET http://localhost:8080/api/livres
Accept: application/json

### Possibilité 4
GET http://localhost:8080/v1/livres
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/livres
Accept: application/json
```

---

##### **Ajouter un nouveau livre :**

```http
### Possibilité 1
POST http://localhost:8080/livres/ajouter
Content-Type: application/json

{
  "id": 3,
  "titre": "Fahrenheit 451",
  "auteur": "Ray Bradbury"
}

### Possibilité 2
POST http://localhost:8080/api/livres/ajouter
Content-Type: application/json

{
  "id": 4,
  "titre": "Les Misérables",
  "auteur": "Victor Hugo"
}

### Possibilité 3
POST http://localhost:8080/v1/livres/ajouter
Content-Type: application/json

{
  "id": 5,
  "titre": "Moby Dick",
  "auteur": "Herman Melville"
}

### Possibilité 4
POST http://localhost:8080/livres
Content-Type: application/json

{
  "id": 6,
  "titre": "Don Quichotte",
  "auteur": "Miguel de Cervantes"
}

### Possibilité 5
POST http://localhost:8080/livres/add
Content-Type: application/json

{
  "id": 7,
  "titre": "Germinal",
  "auteur": "Émile Zola"
}
```

---

##### **Récupérer un livre par son ID :**

```http
### Possibilité 1
GET http://localhost:8080/livres/id/1
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/livres/id/1
Accept: application/json

### Possibilité 3
GET http://localhost:8080/v1/livres/id/1
Accept: application/json

### Possibilité 4
GET http://localhost:8080/livres/1
Accept: application/json

### Possibilité 5
GET http://localhost:8080/livres/find/1
Accept: application/json
```

---

# Partie à compléter (Remplir la dernière colonne) : 

| **Section**                    | **Exemple d'appel API** | **Ce que je suggère**                            | **Commentaire**                                                                                                                     | **Votre commentaire (Correct ou Non Correct)** |
|---------------------------------|-------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| **Lister tous les livres**       | Possibilité 1            | Correct                              | Cet appel est bien structuré et respecte les conventions REST.                                                                                       |                            |
|                                 | Possibilité 2            | Correct                              | Correct également, mais attention au format de réponse si XML est utilisé.                                                                           |                            |
|                                 | Possibilité 3            | Correct mais redondant               | Si vous n'avez pas besoin de préfixer par `/api`, simplifiez l'URL. Sinon, ajoutez `@RequestMapping("/api/livres")` à la classe.                     |                            |
|                                 | Possibilité 4            | Correct mais nécessite ajustement    | Si vous optez pour `/v1`, ajoutez `@RequestMapping("/v1/livres")` pour correspondre à la version API.                                                |                            |
|                                 | Possibilité 5            | Correct mais nécessite ajustement    | Comme pour la possibilité 4, pensez à aligner l'URL et l'annotation avec `/api/v1/livres`.                                                          |                            |
| **Ajouter un nouveau livre**     | Possibilité 1            | Correct mais pas optimal             | Vous pouvez simplifier en supprimant `/ajouter` et utiliser simplement `/livres` pour une meilleure conformité REST.                                |                            |
|                                 | Possibilité 2            | Correct mais pas optimal             | Même remarque : supprimez `/ajouter` et utilisez directement `/livres`.                                                                            |                            |
|                                 | Possibilité 3            | Correct mais pas optimal             | Idem que **Possibilité 1** et **2**. Ajoutez `@RequestMapping("/v1/livres")` si vous conservez `/v1` dans l'URL.                                    |                            |
|                                 | Possibilité 4            | Correct                              | Aucune modification nécessaire. C'est la meilleure approche RESTful pour ajouter un livre.                                                          |                            |
|                                 | Possibilité 5            | Incorrect                            | Remplacez `/add` par simplement `/livres` pour respecter les conventions REST.                                                                     |                            |
| **Récupérer un livre par ID**    | Possibilité 1            | Correct mais optimisable             | Vous pouvez supprimer `/id` et utiliser directement `/livres/{livreId}` pour simplifier.                                                          |                            |
|                                 | Possibilité 2            | Correct                              | Aucune modification nécessaire.

                                                                                                                     |                            |
|                                 | Possibilité 3            | Correct mais nécessite ajustement    | Utilisez `/v1` seulement si vous avez plusieurs versions d'API, et ajoutez `@RequestMapping("/v1/livres")` au niveau de la classe.                 |                            |
|                                 | Possibilité 4            | Correct et optimal                   | Aucune modification nécessaire. Utiliser `/livres/{livreId}` est conforme aux bonnes pratiques REST.                                               |                            |
|                                 | Possibilité 5            | Correct mais pas optimal             | Remplacez `/find/{id}` par simplement `/livres/{livreId}`. Le verbe "find" est inutile en REST.                                                   |                            |

