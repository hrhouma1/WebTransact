# **Examen de Développement d'API : Gestion d'une Animalerie avec API REST**

# **Contexte :**
Dans cet exercice, vous allez travailler sur la gestion d'une animalerie à l'aide d'une API REST. Vous devez compléter les annotations et les méthodes d'un contrôleur qui permet de gérer les animaux disponibles dans l'animalerie, ainsi que d'autres fonctionnalités liées à la gestion des animaux, comme l'ajout de nouveaux animaux, la mise à jour de leurs informations et la récupération de détails spécifiques.

Dans la partie 1 de l'exercice 1, vous devrez choisir la ou les bonne.(s) annotations pour exposer les méthodes du contrôleur et proposer des appels API qui pourraient être utilisés pour interagir avec l'inventaire de l'animalerie.

---

# **Exercice 01 : Compléter les annotations et les appels API**

L'objectif de cet exercice est de compléter les annotations nécessaires dans un contrôleur REST pour gérer les animaux de l'animalerie. Vous devrez aussi proposer des appels API appropriés pour chaque méthode.

---

# Partie 1. Compléter les annotations manquantes pour que cette classe réponde aux requêtes HTTP
# 📢

```java
// Compléter les annotations appropriées pour gérer les animaux via des requêtes HTTP

@Possibilité 1 : @RestController  
@Possibilité 2 : @Controller  
@Possibilité 3 : @Service  
@Possibilité 4 : @Component  
@Possibilité 5 : @RequestMapping("/animaux")

public class AnimalController {

    // Gérer les requêtes GET pour lister tous les animaux disponibles
    @Possibilité 1 : @GetMapping  
    @Possibilité 2 : @RequestMapping(method = RequestMethod.GET)  
    @Possibilité 3 : @PostMapping  
    @Possibilité 4 : @PutMapping  
    @Possibilité 5 : @DeleteMapping  

    public List<Animal> getAllAnimals() {
        return Arrays.asList(
            new Animal(1, "Chien", "Bulldog"),
            new Animal(2, "Chat", "Siamois")
        );
    }

    // Gérer les requêtes POST pour ajouter un nouvel animal
    @Possibilité 1 : @PostMapping("/ajouter")  
    @Possibilité 2 : @RequestMapping(value = "/ajouter", method = RequestMethod.POST)  
    @Possibilité 3 : @PutMapping("/ajouter")  
    @Possibilité 4 : @DeleteMapping("/ajouter")  
    @Possibilité 5 : @PatchMapping("/ajouter")  

    public Animal addAnimal(@Possibilité 1 : @RequestBody Animal animal, 
                            @Possibilité 2 : @ModelAttribute Animal animal, 
                            @Possibilité 3 : @RequestParam Animal animal, 
                            @Possibilité 4 : @SessionAttribute Animal animal, 
                            @Possibilité 5 : @PathVariable Animal animal) {
        return animal;
    }

    // Gérer les requêtes GET pour récupérer les détails d'un animal par son ID
    @Possibilité 1 : @GetMapping("/id/{animalId}")  
    @Possibilité 2 : @RequestMapping(value = "/id/{animalId}", method = RequestMethod.GET)  
    @Possibilité 3 : @PostMapping("/id/{animalId}")  
    @Possibilité 4 : @PatchMapping("/id/{animalId}")  
    @Possibilité 5 : @DeleteMapping("/id/{animalId}")  

    public Animal getAnimalById(@Possibilité 1 : @PathVariable int animalId, 
                                @Possibilité 2 : @RequestParam int animalId, 
                                @Possibilité 3 : @RequestHeader int animalId, 
                                @Possibilité 4 : @CookieValue int animalId, 
                                @Possibilité 5 : @SessionAttribute int animalId) {
        return new Animal(animalId, "Animal Existant", "Race Inconnue");
    }
}
```

---

# Partie 2. Proposez 5 possibilités d'appels API pour chaque méthode

Je vous propose plusieurs exemples d'appels API accompagnés de commentaires. Merci de les lire attentivement et de me dire si vous estimez que mes remarques sont correctes ou non.

# **Lister tous les animaux :**

```http
### Possibilité 1
GET http://localhost:8080/animaux
Accept: application/json

### Possibilité 2
GET http://localhost:8080/animaux
Accept: application/xml

### Possibilité 3
GET http://localhost:8080/api/animaux
Accept: application/json

### Possibilité 4
GET http://localhost:8080/v1/animaux
Accept: application/json

### Possibilité 5
GET http://localhost:8080/api/v1/animaux
Accept: application/json
```

---

##### **Ajouter un nouvel animal :**

```http
### Possibilité 1
POST http://localhost:8080/animaux/ajouter
Content-Type: application/json

{
  "id": 3,
  "type": "Poisson",
  "race": "Goldfish"
}

### Possibilité 2
POST http://localhost:8080/api/animaux/ajouter
Content-Type: application/json

{
  "id": 4,
  "type": "Lapin",
  "race": "Angora"
}

### Possibilité 3
POST http://localhost:8080/v1/animaux/ajouter
Content-Type: application/json

{
  "id": 5,
  "type": "Oiseau",
  "race": "Canari"
}

### Possibilité 4
POST http://localhost:8080/animaux
Content-Type: application/json

{
  "id": 6,
  "type": "Reptile",
  "race": "Iguane"
}

### Possibilité 5
POST http://localhost:8080/animaux/add
Content-Type: application/json

{
  "id": 7,
  "type": "Chien",
  "race": "Labrador"
}
```

---

##### **Récupérer un animal par son ID :**

```http
### Possibilité 1
GET http://localhost:8080/animaux/id/1
Accept: application/json

### Possibilité 2
GET http://localhost:8080/api/animaux/id/1
Accept: application/json

### Possibilité 3
GET http://localhost:8080/v1/animaux/id/1
Accept: application/json

### Possibilité 4
GET http://localhost:8080/animaux/1
Accept: application/json

### Possibilité 5
GET http://localhost:8080/animaux/find/1
Accept: application/json
```




# Partie à compléter ( Remplir la dernière colonne) : 

# 📢

| **Section**                    | **Exemple d'appel API** | **Ce que je suggère**                            | **Commentaire**                                                                                                                     | **Votre commentaire (Correct ou Non Correct)** |
|---------------------------------|-------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| **Lister tous les animaux**      | Possibilité 1            | Correct                              | Cet appel est bien structuré et respecte les conventions REST.                                                                                       |                            |
|                                 | Possibilité 2            | Correct                              | Correct également, mais attention au format de réponse si XML est utilisé.                                                                           |                            |
|                                 | Possibilité 3            | Correct mais redondant               | Si vous n'avez pas besoin de préfixer par `/api`, simplifiez l'URL. Sinon, ajoutez `@RequestMapping("/api/animaux")` à la classe.                     |                            |
|                                 | Possibilité 4            | Correct mais nécessite ajustement    | Si vous optez pour `/v1`, ajoutez `@RequestMapping("/v1/animaux")` pour correspondre à la version API.                                                |                            |
|                                 | Possibilité 5            | Correct mais nécessite ajustement    | Comme pour la possibilité 4, pensez à aligner l'URL et l'annotation avec `/api/v1/animaux`.                                                          |                            |
| **Ajouter un nouvel animal**     | Possibilité 1            | Correct mais pas optimal             | Vous pouvez simplifier en supprimant `/ajouter` et utiliser simplement `/animaux` pour une meilleure conformité REST.                                |                            |
|                                 | Possibilité 2            | Correct mais pas optimal             | Même remarque : supprimez `/ajouter` et utilisez directement `/animaux`.                                                                            |                            |
|                                 | Possibilité 3            | Correct mais pas optimal             | Idem que **Possibilité 1** et **2**. Ajoutez `@RequestMapping("/v1/animaux")` si vous conservez `/v1` dans l'URL.                                    |                            |
|                                 | Possibilité 4            | Correct                              | Aucune modification nécessaire. C'est la meilleure approche RESTful pour ajouter un animal.                                                          |                            |
|                                 | Possibilité 5            | Incorrect                            | Remplacez `/add` par simplement `/animaux` pour respecter les conventions REST.                                                                     |                            |
| **Récupérer un animal par ID**   | Possibilité 1            | Correct mais optimisable             | Vous pouvez supprimer `/id` et utiliser directement `/animaux/{animalId}` pour simplifier.                                                          |                            |
|                                 | Possibilité 2            | Correct                              | Aucune modification nécessaire.                                                                                                                     |                            |
|                                 | Possibilité 3            | Correct mais nécessite ajustement    | Utilisez `/v1` seulement si vous avez plusieurs versions d'API, et ajoutez `@RequestMapping("/v1/animaux")` au niveau de la classe.                 |                            |
|                                 | Possibilité 4            | Correct et optimal                   | Aucune modification nécessaire. Utiliser `/animaux/{animalId}` est conforme aux bonnes pratiques REST.                                               |                            |
|                                 | Possibilité 5            | Correct mais pas optimal             | Remplacez `/find/{id}` par simplement `/animaux/{animalId}`. Le verbe "find" est inutile en REST.                                                   |                            |


### **Pensez-vous que mon explication ci-bas est correcte ?:**

1. **Ajout de versions dans les chemins d'URL** : Si vous utilisez des versions comme `/v1` ou `/api`, il est nécessaire de le refléter dans le code en modifiant l'annotation `@RequestMapping` au niveau de la classe contrôleur. Par exemple, si vous souhaitez utiliser l'URL `/v1/animaux`, vous devrez ajouter cette annotation au-dessus de la déclaration de la classe :

   ```java
   @RestController
   @RequestMapping("/v1/animaux")
   public class AnimalController {
       // méthodes ici
   }
   ```

Cela sert à organiser et versionner les API, ce qui est utile lorsque l'application évolue dans le temps.


# 📢

# Votre réponse : ....



