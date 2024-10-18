# **Examen Final**  
## **Projet : Gestion des Livres et Auteurs avec Jakarta EE**

---

# **Partie 3 : Travailler avec `ResponseEntity` dans Spring Boot**  
### *(30 points)*


# Objectif : 
Cette évaluation teste votre capacité à utiliser **ResponseEntity** pour retourner des réponses HTTP appropriées dans des scénarios liés à la gestion des livres, auteurs, critiques et lecteurs dans Spring Boot.

---

### Instructions :
- Complétez chaque scénario en fournissant une implémentation de la réponse HTTP appropriée en utilisant **ResponseEntity**.
- Utilisez des méthodes simples de **ResponseEntity** comme `.ok()`, `.status(HttpStatus)` et `.body()` pour formuler vos réponses.
- Chaque question est notée sur **3 points**, pour un total de **30 points**.

---

### Scénarios :

| **#** | **Points** | **Scénario**                                                                                           | **Réponse**                                                     |
|-------|------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| 1     | 3          | Retourner une réponse HTTP avec un message `"Livre ajouté avec succès"` et un statut **201 Created**.   |                                                                |
| 2     | 3          | Retourner une réponse avec un statut **200 OK** et l’objet `Book` dans le corps de la réponse.          |                                                                |
| 3     | 3          | Retourner un statut **404 Not Found** si un auteur n’est pas trouvé par son ID.                        |                                                                |
| 4     | 3          | Retourner une réponse avec un statut **204 No Content** après suppression d’un livre.                  |                                                                |
| 5     | 3          | Retourner un message d’erreur `"Données invalides pour l'adresse"` avec un statut **400 Bad Request**.  |                                                                |
| 6     | 3          | Retourner une réponse avec un statut **202 Accepted** et un message `"Traitement en cours"`.            |                                                                |
| 7     | 3          | Retourner une réponse avec un objet **JSON** contenant l’`Author` et un statut **200 OK**.             |                                                                |
| 8     | 3          | Retourner un message `"Accès refusé"` avec un statut **403 Forbidden**.                                 |                                                                |
| 9     | 3          | Retourner une réponse avec une liste de livres (`List<Book>`) et un statut **200 OK**.                 |                                                                |
| 10    | 3          | **Difficile** : Retourner un statut **409 Conflict** si un conflit est détecté lors de la mise à jour d'un livre, avec un message `"Conflit lors de la mise à jour du livre"`. |                                                                |

---

### Exemple :  
Pour le scénario 9 : retourner une liste de livres avec un statut **200 OK**.

```java
public ResponseEntity<List<Book>> getAllBooks() {
    List<Book> books = bookService.findAllBooks();
    return ResponseEntity.ok(books);
}
```

---

### Critères de notation :
- **Total de 30 points**, avec 3 points pour chaque question.
- Fournissez une seule méthode **ResponseEntity** pour chaque scénario.


