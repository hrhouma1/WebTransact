# 🖥️ **Questionnaire 3  : Travailler avec ResponseEntity dans Spring Boot**

## 🎯 Objectif de l’évaluation  
Cette évaluation vise à tester votre capacité à utiliser **ResponseEntity** pour retourner des réponses HTTP simples dans Spring Boot. Vous devez proposer **2 méthodes différentes** pour chaque scénario.

---

### 📚 **Exemple pour vous aider** :

### 🎓 **Exemple 1** :  
**Scénario** : Retourner une réponse HTTP avec un message `"Bonjour, monde!"` et un statut **200 OK**. 

1. **Combinaison 1** :
   ```java
   return ResponseEntity.ok("Bonjour, monde!");
   ```

2. **Combinaison 2** :
   ```java
   return new ResponseEntity<>("Bonjour, monde!", HttpStatus.OK);
   ```

---

# 🚀 **MAINTENANT, IL EST TEMPS DE COMMENCER !** 🎯

---

## **Questionnaire 3** : Complétez les scénarios

### Instructions :

1. **Complétez les colonnes "Combinaison 1" et "Combinaison 2"** en proposant deux façons différentes de répondre à chaque scénario.
2. Utilisez des méthodes simples de **ResponseEntity** comme `.ok()`, `.status(HttpStatus)` et `.body()`.
3. Chaque question est notée sur **5 points**, pour un total de **100 points**.

---

### 📝 Tableau d'évaluation très simplifié :

| **#** | **Points** | **Scénario**                                                                                           | **Combinaison 1**                                               | **Combinaison 2**                                               |
|-------|------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|----------------------------------------------------------------|
| 1     | 5          | Retourner une réponse HTTP avec un message `"Hello, World!"` et un statut **200 OK**.                   |                                                                |                                                                |
| 2     | 5          | Retourner une réponse avec un statut **201 Created** et l’objet `User` dans le corps.                   |                                                                |                                                                |
| 3     | 5          | Retourner un statut **404 Not Found** si un utilisateur n’est pas trouvé.                               |                                                                |                                                                |
| 4     | 5          | Retourner une réponse avec un statut **204 No Content** après suppression d’un élément.                 |                                                                |                                                                |
| 5     | 5          | Retourner un message d’erreur `"Données invalides"` avec un statut **400 Bad Request**.                 |                                                                |                                                                |
| 6     | 5          | Retourner une réponse avec un statut **202 Accepted** et un message `"Traitement en cours"`.            |                                                                |                                                                |
| 7     | 5          | Retourner une réponse avec un objet **JSON** contenant `User` et un statut **200 OK**.                  |                                                                |                                                                |
| 8     | 5          | Retourner un message `"Accès refusé"` avec un statut **403 Forbidden**.                                 |                                                                |                                                                |
| 9     | 5          | Retourner un statut **301 Moved Permanently** avec un en-tête **Location** pour une redirection.        |                                                                |                                                                |
| 10    | 5          | Retourner une réponse avec un message `"Opération réussie"` et un statut **200 OK**.                    |                                                                |                                                                |
| 11    | 5          | Retourner une réponse avec un message `"Enregistrement mis à jour"` et un statut **200 OK**.            |                                                                |                                                                |
| 12    | 5          | Retourner une réponse avec un statut **400 Bad Request** si une validation échoue.                      |                                                                |                                                                |
| 13    | 5          | Retourner un statut **401 Unauthorized** avec un message `"Non autorisé"` en cas d’échec d’authentification. |                                                                |                                                                |
| 14    | 5          | Retourner un message `"Aucun résultat trouvé"` et un statut **204 No Content**.                        |                                                                |                                                                |
| 15    | 5          | Retourner une réponse avec un objet **JSON** vide et un statut **200 OK**.                              |                                                                |                                                                |
| 16    | 5          | Retourner un statut **403 Forbidden** avec un en-tête personnalisé `X-Error` et la valeur `Accès refusé`. |                                                                |                                                                |
| 17    | 5          | Retourner un statut **200 OK** avec un en-tête personnalisé `X-Status` et la valeur `Succès`.           |                                                                |                                                                |
| 18    | 5          | Retourner un message `"Requête en cours de traitement"` avec un statut **202 Accepted**.               |                                                                |                                                                |
| 19    | 5          | Retourner une réponse avec un statut **409 Conflict** si un conflit est détecté.                        |                                                                |                                                                |
| 20    | 5          | Retourner une réponse avec un statut **200 OK** et un message `"L'opération est terminée"`.            |                                                                |                                                                |

---

### **Critères de notation** :

- **Total de 100 points**, avec 5 points pour chaque question.
- Vous devez proposer **deux combinaisons** pour chaque scénario, en utilisant des méthodes simples de **ResponseEntity**.
