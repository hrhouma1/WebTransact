# Réponses Questionnaire 3

| **#** | **Scénario** | **Combinaison 1** | **Combinaison 2** |
|-------|--------------|-------------------|-------------------|
| 1 | Retourner une réponse HTTP avec un message `"Hello, World!"` et un statut **200 OK**. | `return ResponseEntity.ok("Hello, World!");` | `return new ResponseEntity<>("Hello, World!", HttpStatus.OK);` |
| 2 | Retourner une réponse avec un statut **201 Created** et l'objet `User` dans le corps. | `return ResponseEntity.status(HttpStatus.CREATED).body(user);` | `return new ResponseEntity<>(user, HttpStatus.CREATED);` |
| 3 | Retourner un statut **404 Not Found** si un utilisateur n'est pas trouvé. | `return ResponseEntity.notFound().build();` | `return new ResponseEntity<>(HttpStatus.NOT_FOUND);` |
| 4 | Retourner une réponse avec un statut **204 No Content** après suppression d'un élément. | `return ResponseEntity.noContent().build();` | `return new ResponseEntity<>(HttpStatus.NO_CONTENT);` |
| 5 | Retourner un message d'erreur `"Données invalides"` avec un statut **400 Bad Request**. | `return ResponseEntity.badRequest().body("Données invalides");` | `return new ResponseEntity<>("Données invalides", HttpStatus.BAD_REQUEST);` |
| 6 | Retourner une réponse avec un statut **202 Accepted** et un message `"Traitement en cours"`. | `return ResponseEntity.accepted().body("Traitement en cours");` | `return new ResponseEntity<>("Traitement en cours", HttpStatus.ACCEPTED);` |
| 7 | Retourner une réponse avec un objet **JSON** contenant `User` et un statut **200 OK**. | `return ResponseEntity.ok(user);` | `return new ResponseEntity<>(user, HttpStatus.OK);` |
| 8 | Retourner un message `"Accès refusé"` avec un statut **403 Forbidden**. | `return ResponseEntity.status(HttpStatus.FORBIDDEN).body("Accès refusé");` | `return new ResponseEntity<>("Accès refusé", HttpStatus.FORBIDDEN);` |
| 9 | Retourner un statut **301 Moved Permanently** avec un en-tête **Location** pour une redirection. | `return ResponseEntity.status(HttpStatus.MOVED_PERMANENTLY).header("Location", "http://newurl.com").build();` | `HttpHeaders headers = new HttpHeaders(); headers.add("Location", "http://newurl.com"); return new ResponseEntity<>(headers, HttpStatus.MOVED_PERMANENTLY);` |
| 10 | Retourner une réponse avec un message `"Opération réussie"` et un statut **200 OK**. | `return ResponseEntity.ok("Opération réussie");` | `return new ResponseEntity<>("Opération réussie", HttpStatus.OK);` |
| 11 | Retourner une réponse avec un message `"Enregistrement mis à jour"` et un statut **200 OK**. | `return ResponseEntity.ok("Enregistrement mis à jour");` | `return new ResponseEntity<>("Enregistrement mis à jour", HttpStatus.OK);` |
| 12 | Retourner une réponse avec un statut **400 Bad Request** si une validation échoue. | `return ResponseEntity.badRequest().build();` | `return new ResponseEntity<>(HttpStatus.BAD_REQUEST);` |
| 13 | Retourner un statut **401 Unauthorized** avec un message `"Non autorisé"` en cas d'échec d'authentification. | `return ResponseEntity.status(HttpStatus.UNAUTHORIZED).body("Non autorisé");` | `return new ResponseEntity<>("Non autorisé", HttpStatus.UNAUTHORIZED);` |
| 14 | Retourner un message `"Aucun résultat trouvé"` et un statut **204 No Content**. | `return ResponseEntity.status(HttpStatus.NO_CONTENT).body("Aucun résultat trouvé");` | `return new ResponseEntity<>("Aucun résultat trouvé", HttpStatus.NO_CONTENT);` |
| 15 | Retourner une réponse avec un objet **JSON** vide et un statut **200 OK**. | `return ResponseEntity.ok().body(new JSONObject());` | `return new ResponseEntity<>(new JSONObject(), HttpStatus.OK);` |
| 16 | Retourner un statut **403 Forbidden** avec un en-tête personnalisé `X-Error` et la valeur `Accès refusé`. | `return ResponseEntity.status(HttpStatus.FORBIDDEN).header("X-Error", "Accès refusé").build();` | `HttpHeaders headers = new HttpHeaders(); headers.add("X-Error", "Accès refusé"); return new ResponseEntity<>(headers, HttpStatus.FORBIDDEN);` |
| 17 | Retourner un statut **200 OK** avec un en-tête personnalisé `X-Status` et la valeur `Succès`. | `return ResponseEntity.ok().header("X-Status", "Succès").build();` | `HttpHeaders headers = new HttpHeaders(); headers.add("X-Status", "Succès"); return new ResponseEntity<>(headers, HttpStatus.OK);` |
| 18 | Retourner un message `"Requête en cours de traitement"` avec un statut **202 Accepted**. | `return ResponseEntity.accepted().body("Requête en cours de traitement");` | `return new ResponseEntity<>("Requête en cours de traitement", HttpStatus.ACCEPTED);` |
| 19 | Retourner une réponse avec un statut **409 Conflict** si un conflit est détecté. | `return ResponseEntity.status(HttpStatus.CONFLICT).build();` | `return new ResponseEntity<>(HttpStatus.CONFLICT);` |
| 20 | Retourner une réponse avec un statut **200 OK** et un message `"L'opération est terminée"`. | `return ResponseEntity.ok("L'opération est terminée");` | `return new ResponseEntity<>("L'opération est terminée", HttpStatus.OK);` |

# Citations:

[1] https://sudarshandoiphode.hashnode.dev/responseentity

[2] https://www.danvega.dev/blog/spring-response-entity

[3] https://www.geeksforgeeks.org/how-to-use-spring-responseentity-to-manipulate-the-http-response/

[4] https://codingnomads.com/spring-responseentity

[5] https://docs.spring.io/spring-framework/docs/4.1.0.RC1_to_4.1.0.RC2/Spring%20Framework%204.1.0.RC2/org/springframework/http/ResponseEntity.html

[6] https://www.baeldung.com/spring-response-entity
