# **Examen Final**  
## **Projet : Gestion des Livres et Auteurs avec Jakarta EE**


# **Partie 2 : Méthodes dérivées avec Spring Data JPA**  
**(40 points)**


### Objectif: 
Cet exercice vous demande de compléter les noms de méthodes JPA dérivées à partir des requêtes SQL correspondant à votre projet **Gestion des Livres et Auteurs avec Jakarta EE**.

---

### Instructions :
1. **Complétez la colonne "Nom de la méthode JPA"** en dérivant les méthodes à partir des requêtes SQL fournies.
2. Respectez la syntaxe des méthodes JPA avec des préfixes comme `findBy`, `countBy`, `deleteBy`, et utilisez les bons opérateurs (`And`, `Or`, `GreaterThan`, etc.).
3. Vous avez 20 questions, chacune valant **2 points**, pour un total de **40 points**.
4. **Indication :** Une des méthodes devra être implémentée via une requête JPQL. Il vous revient de l’identifier et de la proposer correctement.

---

### Tableau des questions

| **Requête SQL**                                                                                                                               | **Indice**                                                          | **Nom de la méthode JPA**              |
|------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|-----------------------------------------|
| `SELECT * FROM Author;`                                                                                                                        | Récupérer tous les auteurs.                                           |                                         |
| `SELECT * FROM Book;`                                                                                                                          | Récupérer tous les livres.                                            |                                         |
| `SELECT * FROM Review;`                                                                                                                        | Récupérer toutes les critiques.                                       |                                         |
| `SELECT * FROM Address WHERE id = 1;`                                                                                                          | Récupérer une adresse par son ID.                                     |                                         |
| `SELECT * FROM Book WHERE id = 2;`                                                                                                             | Récupérer un livre par son ID.                                        |                                         |
| `SELECT * FROM Author WHERE id = 3;`                                                                                                           | Récupérer un auteur par son ID.                                       |                                         |
| `SELECT * FROM Book WHERE language = 'English';`                                                                                               | Récupérer les livres en anglais.                                      |                                         |
| `SELECT * FROM Review WHERE bookId = 1;`                                                                                                       | Récupérer les critiques d’un livre donné.                             |                                         |
| `SELECT * FROM Book WHERE pages > 300;`                                                                                                        | Rechercher les livres ayant plus de 300 pages.                        |                                         |
| `SELECT * FROM Author WHERE lastname = 'Smith';`                                                                                               | Rechercher un auteur par son nom de famille.                          |                                         |
| `SELECT * FROM Book WHERE title LIKE 'H%';`                                                                                                    | Rechercher les livres dont le titre commence par 'H'.                 |                                         |
| `SELECT * FROM Reader WHERE email = 'test@example.com';`                                                                                       | Rechercher un lecteur par son email.                                  |                                         |
| `SELECT COUNT(*) FROM Book WHERE language = 'French';`                                                                                         | Compter les livres en français.                                       |                                         |
| `SELECT AVG(pages) FROM Book WHERE authorId = 1;`                                                                                              | **JPQL Requise :** Calculer la moyenne des pages des livres d’un auteur spécifique. |                                         |
| `SELECT * FROM Book WHERE pages BETWEEN 100 AND 500;`                                                                                          | Rechercher les livres ayant entre 100 et 500 pages.                   |                                         |
| `SELECT * FROM Book b JOIN Author a ON b.authorId = a.id WHERE a.lastname = 'Smith';`                                                          | Rechercher les livres écrits par un auteur dont le nom est 'Smith'.   |                                         |
| `SELECT * FROM Address a JOIN Author au ON a.id = au.addressId WHERE au.firstname = 'John';`                                                   | Rechercher les adresses des auteurs ayant 'John' comme prénom.        |                                         |
| `SELECT * FROM Book WHERE EXISTS (SELECT 1 FROM Author WHERE id = Book.authorId AND lastname = 'Doe');`                                         | Rechercher les livres d’un auteur nommé 'Doe'.                        |                                         |
| `SELECT COUNT(*) FROM Review r WHERE r.bookId = 1;`                                                                                            | Compter le nombre de critiques d’un livre donné.                      |                                         |
| `SELECT * FROM Book WHERE title = 'War and Peace' ORDER BY pages DESC;`                                                                        | Rechercher les livres ayant un titre spécifique, triés par nombre de pages. |                                         |

---



### Critères de notation :

- **Total de 40 points**, avec **2 points** pour chaque question.
- Les méthodes doivent suivre la convention de nommage de **Spring Data JPA** et utiliser les bons opérateurs.
- Une des méthodes doit être implémentée avec une requête JPQL. Vous devez la deviner et l’implémenter correctement.
