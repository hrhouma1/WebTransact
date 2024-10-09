-----------------------------
# 1 - Questions - Maîtrise de **ResponseEntity** dans Spring Boot
-----------------------------

# Objectif de l’évaluation
Cette évaluation a pour objectif de tester votre compréhension et votre capacité à utiliser **ResponseEntity** dans les contrôleurs Spring Boot. Vous devrez manipuler les statuts HTTP, les corps de réponses, et les en-têtes pour retourner des réponses adaptées aux différentes situations.

# Instructions :

1. **Complétez la colonne "Combinaison ResponseEntity"** en dérivant les bonnes méthodes et combinaisons pour chaque scénario.
2. Respectez la syntaxe des méthodes **ResponseEntity** (ex: `.ok()`, `.status(HttpStatus)`, `.body()`).
3. Vous avez **20 questions** valant chacune **5 points**, pour un total de **100 points**.
4. **Classement des questions** :
   - Niveau **Facile** (1 à 10) : Manipulation simple de ResponseEntity.
   - Niveau **Moyen** (11 à 15) : Gestion de conditions avec ResponseEntity.
   - Niveau **Difficile** (16 à 20) : Manipulation avancée avec en-têtes, erreurs, et réponses complexes.

---

# 2 - Tableau des questions

| **Niveau**   | **Scénario**                                                                                              | **Indice**                                                           | **Combinaison ResponseEntity**                                     |
|--------------|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| **Facile**   | Retourner une réponse HTTP avec un message `"Hello, World!"` et un statut **200 OK**.                      | Utilisez `.ok()` et `.body()`.                                        |                                                                    |
| **Facile**   | Retourner une réponse avec un statut **201 Created** et l’objet `User` créé dans le corps de la réponse.    | Utilisez `.status(HttpStatus.CREATED)` et `.body()`.                  |                                                                    |
| **Facile**   | Retourner un statut **404 Not Found** si un utilisateur n’est pas trouvé.                                  | Utilisez `.notFound().build()`.                                       |                                                                    |
| **Facile**   | Retourner une réponse avec un statut **204 No Content** lorsque la suppression d’un élément est réussie.    | Utilisez `.noContent().build()`.                                      |                                                                    |
| **Facile**   | Ajouter un en-tête HTTP `Custom-Header` avec la valeur `test` à la réponse.                                | Utilisez `.header()` pour ajouter l’en-tête.                          |                                                                    |
| **Facile**   | Retourner une réponse avec un fichier PDF en spécifiant un en-tête **Content-Disposition**.                | Utilisez `.headers()` et `.body()` pour le fichier.                   |                                                                    |
| **Facile**   | Retourner un message d’erreur `"Invalid data"` avec un statut **400 Bad Request**.                         | Utilisez `.badRequest().body()`.                                      |                                                                    |
| **Facile**   | Retourner une réponse avec un statut **202 Accepted** et un message `"Request accepted"`.                  | Utilisez `.accepted().body()`.                                        |                                                                    |
| **Facile**   | Retourner une réponse avec un objet **JSON** comme contenu, et le statut **200 OK**.                       | Utilisez `.ok().contentType(MediaType.APPLICATION_JSON).body()`.      |                                                                    |
| **Facile**   | Retourner un statut **301 Moved Permanently** avec un en-tête **Location** pour une redirection.           | Utilisez `.status(HttpStatus.MOVED_PERMANENTLY).header("Location")`.  |                                                                    |
| **Moyen**    | Si un utilisateur existe, retourner un **200 OK**, sinon un **404 Not Found**.                            | Utilisez `.ok()` ou `.notFound().build()`.                            |                                                                    |
| **Moyen**    | Retourner un statut **400 Bad Request** si une validation échoue, sinon un **201 Created** avec le corps.  | Utilisez `.badRequest()` ou `.status(HttpStatus.CREATED).body()`.     |                                                                    |
| **Moyen**    | Retourner une réponse avec plusieurs en-têtes personnalisés et un corps.                                   | Utilisez `.headers()` avec plusieurs en-têtes et `.body()`.           |                                                                    |
| **Moyen**    | Ajouter un en-tête personnalisé **X-Response-Time** avec une valeur dynamique dans la réponse.             | Utilisez `.header()` pour ajouter cet en-tête.                        |                                                                    |
| **Moyen**    | Retourner une réponse avec un en-tête **Cache-Control** et le statut **200 OK**.                           | Utilisez `.ok().header("Cache-Control", "no-cache")`.                 |                                                                    |
| **Difficile**| Retourner une réponse complexe avec un en-tête personnalisé, un corps JSON, et un statut **206 Partial Content**. | Utilisez `.status(HttpStatus.PARTIAL_CONTENT).header().body()`.       |                                                                    |
| **Difficile**| Retourner une réponse avec un statut **201 Created**, un en-tête **Location** et un corps JSON pour un objet créé. | Utilisez `.created(URI).body()`.                                      |                                                                    |
| **Difficile**| Gérer une erreur interne du serveur en retournant un statut **500 Internal Server Error** avec un message d’erreur. | Utilisez `.status(HttpStatus.INTERNAL_SERVER_ERROR).body()`.          |                                                                    |
| **Difficile**| Retourner une réponse avec une collection d’objets, un statut **200 OK**, et un type de contenu JSON.      | Utilisez `.ok().contentType(MediaType.APPLICATION_JSON).body()`.      |                                                                    |
| **Difficile**| Utiliser **ResponseEntity** pour retourner une réponse sans corps avec un en-tête **X-Empty-Response** et un statut **204 No Content**. | Utilisez `.noContent().header("X-Empty-Response", "true").build()`.   |                                                                    |

---

### Critères de notation :

- **Total de 100 points**, avec 5 points pour chaque question.
- Les méthodes **ResponseEntity** doivent être correctement combinées pour gérer les différents cas (statut, en-têtes, corps).
- Vous devez démontrer une bonne compréhension des différentes méthodes statiques de **ResponseEntity** et comment les utiliser dans un contexte Spring Boot.


------------------------------
# 3 - Réponses
------------------------------

| **Niveau**   | **Scénario**                                                                                              | **Indice**                                                           | **Combinaison ResponseEntity**                                     |
|--------------|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| **Facile**   | Retourner une réponse HTTP avec un message `"Hello, World!"` et un statut **200 OK**.                      | Utilisez `.ok()` et `.body()`.                                        | `ResponseEntity.ok().body("Hello, World!");`                       |
| **Facile**   | Retourner une réponse avec un statut **201 Created** et l’objet `User` créé dans le corps de la réponse.    | Utilisez `.status(HttpStatus.CREATED)` et `.body()`.                  | `ResponseEntity.status(HttpStatus.CREATED).body(user);`            |
| **Facile**   | Retourner un statut **404 Not Found** si un utilisateur n’est pas trouvé.                                  | Utilisez `.notFound().build()`.                                       | `ResponseEntity.notFound().build();`                               |
| **Facile**   | Retourner une réponse avec un statut **204 No Content** lorsque la suppression d’un élément est réussie.    | Utilisez `.noContent().build()`.                                      | `ResponseEntity.noContent().build();`                              |
| **Facile**   | Ajouter un en-tête HTTP `Custom-Header` avec la valeur `test` à la réponse.                                | Utilisez `.header()` pour ajouter l’en-tête.                          | `ResponseEntity.ok().header("Custom-Header", "test").build();`      |
| **Facile**   | Retourner une réponse avec un fichier PDF en spécifiant un en-tête **Content-Disposition**.                | Utilisez `.headers()` et `.body()` pour le fichier.                   | `ResponseEntity.ok().headers(headers).body(pdfContent);`           |
| **Facile**   | Retourner un message d’erreur `"Invalid data"` avec un statut **400 Bad Request**.                         | Utilisez `.badRequest().body()`.                                      | `ResponseEntity.badRequest().body("Invalid data");`                |
| **Facile**   | Retourner une réponse avec un statut **202 Accepted** et un message `"Request accepted"`.                  | Utilisez `.accepted().body()`.                                        | `ResponseEntity.accepted().body("Request accepted");`              |
| **Facile**   | Retourner une réponse avec un objet **JSON** comme contenu, et le statut **200 OK**.                       | Utilisez `.ok().contentType(MediaType.APPLICATION_JSON).body()`.      | `ResponseEntity.ok().contentType(MediaType.APPLICATION_JSON).body(jsonData);` |
| **Facile**   | Retourner un statut **301 Moved Permanently** avec un en-tête **Location** pour une redirection.           | Utilisez `.status(HttpStatus.MOVED_PERMANENTLY).header("Location")`.  | `ResponseEntity.status(HttpStatus.MOVED_PERMANENTLY).header("Location", "/new-url").build();` |
| **Moyen**    | Si un utilisateur existe, retourner un **200 OK**, sinon un **404 Not Found**.                            | Utilisez `.ok()` ou `.notFound().build()`.                            | `return user != null ? ResponseEntity.ok(user) : ResponseEntity.notFound().build();` |
| **Moyen**    | Retourner un statut **400 Bad Request** si une validation échoue, sinon un **201 Created** avec le corps.  | Utilisez `.badRequest()` ou `.status(HttpStatus.CREATED).body()`.     | `return isValid ? ResponseEntity.status(HttpStatus.CREATED).body(newUser) : ResponseEntity.badRequest().body("Invalid data");` |
| **Moyen**    | Retourner une réponse avec plusieurs en-têtes personnalisés et un corps.                                   | Utilisez `.headers()` avec plusieurs en-têtes et `.body()`.           | `ResponseEntity.ok().header("X-Header-1", "Value1").header("X-Header-2", "Value2").body(content);` |
| **Moyen**    | Ajouter un en-tête personnalisé **X-Response-Time** avec une valeur dynamique dans la réponse.             | Utilisez `.header()` pour ajouter cet en-tête.                        | `ResponseEntity.ok().header("X-Response-Time", timeValue).body(data);` |
| **Moyen**    | Retourner une réponse avec un en-tête **Cache-Control** et le statut **200 OK**.                           | Utilisez `.ok().header("Cache-Control", "no-cache")`.                 | `ResponseEntity.ok().header("Cache-Control", "no-cache").body(data);` |
| **Difficile**| Retourner une réponse complexe avec un en-tête personnalisé, un corps JSON, et un statut **206 Partial Content**. | Utilisez `.status(HttpStatus.PARTIAL_CONTENT).header().body()`.       | `ResponseEntity.status(HttpStatus.PARTIAL_CONTENT).header("Custom-Header", "value").contentType(MediaType.APPLICATION_JSON).body(jsonData);` |
| **Difficile**| Retourner une réponse avec un statut **201 Created**, un en-tête **Location** et un corps JSON pour un objet créé. | Utilisez `.created(URI).body()`.                                      | `ResponseEntity.created(locationURI).body(createdResource);`       |
| **Difficile**| Gérer une erreur interne du serveur en retournant un statut **500 Internal Server Error** avec un message d’erreur. | Utilisez `.status(HttpStatus.INTERNAL_SERVER_ERROR).body()`.          | `ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Internal Server Error");` |
| **Difficile**| Retourner une réponse avec une collection d’objets, un statut **200 OK**, et un type de contenu JSON.      | Utilisez `.ok().contentType(MediaType.APPLICATION_JSON).body()`.      | `ResponseEntity.ok().contentType(MediaType.APPLICATION_JSON).body(listOfObjects);` |
| **Difficile**| Utiliser **ResponseEntity** pour retourner une réponse sans corps avec un en-tête **X-Empty-Response** et un statut **204 No Content**. | Utilisez `.noContent().header("X-Empty-Response", "true").build()`.   | `ResponseEntity.noContent().header("X-Empty-Response", "true").build();` |

---

### Critères de notation :
- **5 points** pour chaque combinaison correcte de **ResponseEntity**.
- **Total : 100 points**.
