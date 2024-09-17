# **Exercice 04 : Implémenter un contrôleur REST pour la gestion des films**

L'objectif de cet exercice est de créer un contrôleur REST pour la gestion des films dans une base de données de films. Vous devez implémenter les méthodes du contrôleur et rédiger les appels API dans un fichier `.http`. Cet exercice demande une maîtrise des annotations Spring et des concepts REST.

---

## 1. Créer la classe `Movie`

Vous devez créer une classe appelée `Movie` avec les champs suivants :
- `id` (int) : l'identifiant unique du film.
- `title` (String) : le titre du film.
- `director` (String) : le réalisateur du film.
- `releaseYear` (int) : l'année de sortie du film.

N'oubliez pas d'inclure les **constructeurs**, **getters**, et **setters** pour cette classe. Cette classe représentera le modèle de données pour votre API REST.

---

## 2. Instructions pour implémenter le contrôleur `MovieController`

### **Étape 1 : Créer la classe `MovieController`**

1. Ajoutez l'annotation nécessaire pour indiquer que cette classe est un contrôleur REST.
2. Définissez la route de base pour toutes les requêtes liées aux films (URL : `/movies`).

### **Étape 2 : Méthode pour récupérer tous les films**

1. Créez une méthode appelée `getAllMovies` qui retourne une liste d'objets `Movie`.
2. Cette méthode doit gérer les requêtes GET sur l'URL `/movies`.

### **Étape 3 : Méthode pour ajouter un nouveau film**

1. Créez une méthode appelée `addMovie` qui accepte un objet `Movie` dans le corps de la requête.
2. Cette méthode doit gérer les requêtes POST sur l'URL `/movies/create` et retourner le film ajouté.

### **Étape 4 : Méthode pour récupérer un film par son ID**

1. Créez une méthode appelée `getMovieById` qui accepte un identifiant de film (int) dans l'URL.
2. Cette méthode doit gérer les requêtes GET sur l'URL `/movies/{movieId}` et retourner un objet `Movie`.

### **Étape 5 : Méthode pour supprimer un film**

1. Créez une méthode appelée `deleteMovie` qui accepte un identifiant de film (int) dans l'URL.
2. Cette méthode doit gérer les requêtes DELETE sur l'URL `/movies/{movieId}` et retourner un message indiquant que le film a été supprimé.

---

## 3. Rédiger un fichier `.http` pour tester votre API

Vous devez rédiger les appels API pour tester toutes les routes que vous venez d'implémenter. Créez un fichier appelé `movie-api.http` contenant les appels pour :
- Récupérer tous les films.
- Ajouter un nouveau film avec les détails fournis dans le corps de la requête.
- Récupérer un film spécifique par son ID.
- Supprimer un film par son ID.

### Indications :
- Utilisez les méthodes HTTP appropriées (GET, POST, DELETE).
- Rédigez les corps de requête JSON lorsque c'est nécessaire (pour l'ajout d'un film).
- Utilisez l'URL de base `http://localhost:8080/movies` pour tester vos appels API.

---

## Résumé des points essentiels à respecter

- Créez la classe `Movie` avec les attributs appropriés.
- Implémentez le contrôleur `MovieController` avec les méthodes demandées pour gérer les films.
- Rédigez un fichier `.http` pour tester votre API.

---

**À vous de jouer !** Vous devez implémenter toutes les parties de cet exercice par vous-même. 🎬
