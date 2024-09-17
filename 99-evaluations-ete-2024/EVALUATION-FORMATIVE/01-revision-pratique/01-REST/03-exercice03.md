# **Exercice 3 : Implémenter un contrôleur REST pour la gestion des livres**

L'objectif de cet exercice est de créer un contrôleur REST pour la gestion des livres dans une bibliothèque. Vous devrez implémenter les méthodes du contrôleur et rédiger les appels API dans un fichier `.http`. Cet exercice demande une compréhension des annotations Spring, des concepts REST, et des outils de test d'API.

---

# 1. Modèle de base : `Book`

Voici la classe `Book` que vous allez utiliser pour cet exercice. Ne modifiez pas cette classe.

```java
public class Book {
    private int id;
    private String title;
    private String author;

    public Book(int id, String title, String author) {
        this.id = id;
        this.title = title;
        this.author = author;
    }

    // Getters et setters (générer automatiquement)
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }
}
```

---

# 2. Instructions pour implémenter le contrôleur `BookController`

### **Étape 1 : Créer la classe `BookController`**

1. **Ajouter l'annotation nécessaire** pour indiquer que cette classe est un contrôleur REST.
2. **Définir la route de base** pour toutes les requêtes liées aux livres (URL : `/books`).

### **Étape 2 : Méthode pour récupérer tous les livres**

1. Créer une méthode appelée `getAllBooks` qui :
   - Retourne une liste d'objets `Book`.
   - Gère les requêtes GET pour l'URL `/books`.
2. Utilisez `Arrays.asList` pour retourner les livres suivants :
   - Livre 1 : `id = 1`, `title = "Le Petit Prince"`, `author = "Antoine de Saint-Exupéry"`
   - Livre 2 : `id = 2`, `title = "1984"`, `author = "George Orwell"`

### **Étape 3 : Méthode pour ajouter un livre**

1. Créer une méthode appelée `addBook` qui :
   - Accepte un objet `Book` dans le corps de la requête.
   - Gère les requêtes POST pour l'URL `/books/create`.
   - Retourne le livre ajouté.

### **Étape 4 : Méthode pour récupérer un livre par son ID**

1. Créer une méthode appelée `getBookById` qui :
   - Accepte un identifiant de livre (int) dans l'URL.
   - Gère les requêtes GET pour l'URL `/books/{bookId}`.
   - Retourne un objet `Book` avec l'ID donné.

### **Étape 5 : Méthode pour supprimer un livre**

1. Créer une méthode appelée `deleteBook` qui :
   - Accepte un identifiant de livre (int) dans l'URL.
   - Gère les requêtes DELETE pour l'URL `/books/{bookId}`.
   - Retourne un message indiquant que le livre a été supprimé.

---

# 3. Créer un fichier `.http` pour tester votre API

Vous devez rédiger les appels API dans un fichier nommé `library-api.http` pour tester les routes que vous venez d'implémenter.

### **Exemple d'appels API à inclure dans `library-api.http` :**

1. **Récupérer tous les livres :**
   ```http
   GET http://localhost:8080/books
   Accept: application/json
   ```

2. **Ajouter un nouveau livre :**
   ```http
   POST http://localhost:8080/books/create
   Content-Type: application/json

   {
     "id": 3,
     "title": "Moby Dick",
     "author": "Herman Melville"
   }
   ```

3. **Récupérer un livre par son ID :**
   ```http
   GET http://localhost:8080/books/1
   Accept: application/json
   ```

4. **Supprimer un livre par son ID :**
   ```http
   DELETE http://localhost:8080/books/2
   ```

---

# Résumé des points essentiels à respecter

1. Utilisez les annotations Spring appropriées pour les méthodes de votre contrôleur.
2. Assurez-vous que chaque méthode renvoie la réponse attendue (liste de livres, livre spécifique, ou message de suppression).
3. Rédigez un fichier `.http` contenant des appels API pour tester les différentes routes.

---

Bonne chance ! 🎯
