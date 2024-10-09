# Évaluation avancée : Maîtrise de **ResponseEntity** dans Spring Boot

# Objectif de l’évaluation
Cette évaluation a pour but de tester votre capacité à utiliser **ResponseEntity** dans Spring Boot en explorant plusieurs combinaisons pour retourner des réponses HTTP. Vous devez proposer **4 méthodes différentes** pour chaque scénario.

---

# Exemples pour vous aider :

## Exemple 1 : Retourner une réponse HTTP avec un message `"Bienvenue dans l'évaluation"` et un statut **200 OK**

1. **Combinaison 1** :
   ```java
   return ResponseEntity.ok("Bienvenue dans l'évaluation");
   ```

2. **Combinaison 2** :
   ```java
   return new ResponseEntity<>("Bienvenue dans l'évaluation", HttpStatus.OK);
   ```

3. **Combinaison 3** :
   ```java
   return ResponseEntity.status(HttpStatus.OK).body("Bienvenue dans l'évaluation");
   ```

4. **Combinaison 4** :
   ```java
   HttpHeaders headers = new HttpHeaders();
   return new ResponseEntity<>("Bienvenue dans l'évaluation", headers, HttpStatus.OK);
   ```

## Exemple 2 : Retourner une réponse avec un statut **201 Created** et l’objet `User` créé dans le corps de la réponse

1. **Combinaison 1** :
   ```java
   return ResponseEntity.status(HttpStatus.CREATED).body(user);
   ```

2. **Combinaison 2** :
   ```java
   return ResponseEntity.created(new URI("/users/" + user.getId())).body(user);
   ```

3. **Combinaison 3** :
   ```java
   return new ResponseEntity<>(user, HttpStatus.CREATED);
   ```

4. **Combinaison 4** :
   ```java
   HttpHeaders headers = new HttpHeaders();
   headers.add("Location", "/users/" + user.getId());
   return new ResponseEntity<>(user, headers, HttpStatus.CREATED);
   ```

Ces exemples montrent comment utiliser différentes combinaisons pour retourner des réponses HTTP. Utilisez ce modèle pour les autres scénarios dans l’évaluation.

---

🚀 **MAINTENANT, IL EST TEMPS DE COMMENCER !** 🎯
----

## Évaluation : Complétez les scénarios

### Instructions :

1. **Complétez les colonnes "Combinaison 1" à "Combinaison 4"** en proposant quatre façons différentes de répondre à chaque scénario.
2. Utilisez les méthodes statiques de **ResponseEntity** (ex: `.ok()`, `.status(HttpStatus)`, `.body()`).
3. Chaque question est notée sur **10 points**, pour un total de **200 points**.

---

### Tableau d'évaluation

| **#** | **Points** | **Scénario**                                                                                              | **Combinaison 1**                                                    | **Combinaison 2**                                                   | **Combinaison 3**                                                   | **Combinaison 4**                                                   |
|-------|------------|-----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------|
| 1     | 10         | Retourner une réponse HTTP avec un message `"Welcome!"` et un statut **200 OK**.                           |                                                                     |                                                                      |                                                                      |                                                                      |
| 2     | 10         | Retourner une réponse avec un statut **201 Created** et l’objet `User` créé dans le corps de la réponse.    |                                                                     |                                                                      |                                                                      |                                                                      |
| 3     | 10         | Retourner un statut **404 Not Found** si un utilisateur n’est pas trouvé.                                  |                                                                     |                                                                      |                                                                      |                                                                      |
| 4     | 10         | Retourner une réponse avec un statut **204 No Content** lorsque la suppression d’un élément est réussie.    |                                                                     |                                                                      |                                                                      |                                                                      |
| 5     | 10         | Ajouter un en-tête HTTP **Custom-Header** avec la valeur `success` à la réponse.                           |                                                                     |                                                                      |                                                                      |                                                                      |
| 6     | 10         | Retourner une réponse avec un fichier PDF en spécifiant un en-tête **Content-Disposition**.                |                                                                     |                                                                      |                                                                      |                                                                      |
| 7     | 10         | Retourner un message d’erreur `"Bad request"` avec un statut **400 Bad Request**.                          |                                                                     |                                                                      |                                                                      |                                                                      |
| 8     | 10         | Retourner une réponse avec un statut **202 Accepted** et un message `"Processing started"`.                |                                                                     |                                                                      |                                                                      |                                                                      |
| 9     | 10         | Retourner une réponse avec un objet **JSON** comme contenu et un statut **200 OK**.                        |                                                                     |                                                                      |                                                                      |                                                                      |
| 10    | 10         | Retourner un statut **301 Moved Permanently** avec un en-tête **Location** pour rediriger vers une nouvelle URL. |                                                                     |                                                                      |                                                                      |                                                                      |
| 11    | 10         | Retourner une réponse avec un fichier **CSV** en spécifiant un en-tête **Content-Disposition** pour forcer le téléchargement. |                                                                     |                                                                      |                                                                      |                                                                      |
| 12    | 10         | Gérer une erreur **500 Internal Server Error** et retourner un message d’erreur détaillé dans le corps de la réponse. |                                                                     |                                                                      |                                                                      |                                                                      |
| 13    | 10         | Ajouter un en-tête HTTP **Authorization** avec un token JWT et retourner un statut **200 OK**.             |                                                                     |                                                                      |                                                                      |                                                                      |
| 14    | 10         | Retourner une réponse avec un en-tête **Cache-Control** avec une durée de mise en cache de 60 secondes et un statut **200 OK**. |                                                                     |                                                                      |                                                                      |                                                                      |
| 15    | 10         | Retourner une réponse avec un en-tête **ETag** pour la validation de cache et un statut **200 OK**.        |                                                                     |                                                                      |                                                                      |                                                                      |
| 16    | 10         | Gérer une authentification échouée en retournant un en-tête **WWW-Authenticate** et un statut **401 Unauthorized**. |                                                                     |                                                                      |                                                                      |                                                                      |
| 17    | 10         | Retourner un statut **403 Forbidden** avec un message `"Access Denied"` lorsque l'accès est refusé.         |                                                                     |                                                                      |                                                                      |                                                                      |
| 18    | 10         | Gérer un délai d'attente dépassé (statut **408 Request Timeout**) avec un message personnalisé dans le corps. |                                                                     |                                                                      |                                                                      |                                                                      |
| 19    | 10         | Retourner une réponse avec un en-tête **Pagination** et un statut **200 OK**, en fournissant une collection d’objets JSON. |                                                                     |                                                                      |                                                                      |                                                                      |
| 20    | 10         | Retourner un statut **206 Partial Content** avec un en-tête personnalisé et un corps **JSON** partiel.     |                                                                     |                                                                      |                                                                      |                                                                      |



### Critères de notation :

- **Total de 200 points**, avec 10 points pour chaque question.
- Vous devez proposer **quatre combinaisons** pour chaque scénario, démontrant votre compréhension des différentes façons d’utiliser **ResponseEntity**.
