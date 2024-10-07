# Diagramme de la base de données (Relation entre les entités **Airport**, **Flight**, et **Passenger**)

```
+-----------------------------+             +-----------------------------+
|           Airport            |             |           Flight            |
+-----------------------------+             +-----------------------------+
| - airportId (PK)             | <-----------| - flightId (PK)             |
| - airportName                |             | - airportId (FK)            |
| - location                   |             | - destination               |
|                               |             | - departureTime             |
+-----------------------------+             +-----------------------------+
                                             |
                                             |
                                             v
                                +-----------------------------+
                                |         Passenger            |
                                +-----------------------------+
                                | - passengerId (PK)           |
                                | - flightId (FK)              |
                                | - passengerName              |
                                | - seatNumber                 |
                                +-----------------------------+
```

### Instructions :

1. **Complétez la colonne "Nom de la méthode JPA"** en dérivant les méthodes à partir des requêtes SQL.
2. Respectez la syntaxe des méthodes JPA avec des préfixes comme `findBy`, `countBy`, `sumBy`, et utilisez les bons opérateurs (`And`, `Or`, `GreaterThan`, etc.).
3. Vous avez 20 questions valant chacune 5 points, pour un total de 100 points.
4. **Classement des questions :**
   - Niveau Facile (1 à 10) : Requêtes simples.
   - Niveau Moyen (11 à 15) : Requêtes avec conditions plus complexes.
   - Niveau Difficile (16 à 20) : Jointures et agrégations.

### Tableau des questions

| **Niveau**   | **Requête SQL**                                                                                                                               | **Indice**                                                          | **Nom de la méthode JPA**              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|-----------------------------------------|
| **Facile**   | `SELECT * FROM Airport;`                                                                                                                       | Récupérer tous les aéroports.                                         |                                         |
| **Facile**   | `SELECT * FROM Flight;`                                                                                                                        | Récupérer tous les vols.                                              |                                         |
| **Facile**   | `SELECT * FROM Passenger;`                                                                                                                     | Récupérer tous les passagers.                                         |                                         |
| **Facile**   | `SELECT * FROM Airport WHERE airportId = 1;`                                                                                                   | Récupérer un aéroport par son ID.                                     |                                         |
| **Facile**   | `SELECT * FROM Flight WHERE flightId = 2;`                                                                                                     | Récupérer un vol par son ID.                                          |                                         |
| **Facile**   | `SELECT * FROM Passenger WHERE passengerId = 3;`                                                                                               | Récupérer un passager par son ID.                                     |                                         |
| **Facile**   | `SELECT * FROM Flight WHERE destination = 'Paris';`                                                                                            | Récupérer les vols vers Paris.                                        |                                         |
| **Facile**   | `SELECT * FROM Passenger WHERE seatNumber = '12A';`                                                                                            | Récupérer les passagers ayant le siège '12A'.                         |                                         |
| **Facile**   | `SELECT * FROM Flight WHERE departureTime > '2024-01-01';`                                                                                     | Rechercher les vols après une date donnée.                            |                                         |
| **Facile**   | `SELECT * FROM Passenger WHERE passengerName = 'John';`                                                                                        | Rechercher un passager par son nom.                                   |                                         |
| **Moyen**    | `SELECT * FROM Flight WHERE destination LIKE 'P%';`                                                                                            | Rechercher les vols vers une destination commençant par 'P'.          |                                         |
| **Moyen**    | `SELECT * FROM Passenger WHERE seatNumber = '12A' AND flightId = 1;`                                                                           | Rechercher les passagers avec un siège spécifique sur un vol donné.   |                                         |
| **Moyen**    | `SELECT COUNT(*) FROM Flight WHERE destination = 'New York';`                                                                                  | Compter les vols vers New York.                                       |                                         |
| **Moyen**    | `SELECT AVG(seatNumber) FROM Passenger WHERE flightId = 1;`                                                                                    | Calculer la moyenne des numéros de siège d'un vol spécifique.         |                                         |
| **Moyen**    | `SELECT * FROM Flight WHERE departureTime BETWEEN '2024-01-01' AND '2024-12-31';`                                                              | Rechercher les vols entre deux dates.                                 |                                         |
| **Difficile**| `SELECT * FROM Passenger p JOIN Flight f ON p.flightId = f.flightId WHERE f.destination = 'Paris';`                                              | Rechercher les passagers des vols à destination de Paris.             |                                         |
| **Difficile**| `SELECT * FROM Airport a JOIN Flight f ON a.airportId = f.airportId WHERE f.destination = 'Tokyo';`                                             | Rechercher les aéroports avec des vols à destination de Tokyo.        |                                         |
| **Difficile**| `SELECT * FROM Passenger WHERE EXISTS (SELECT 1 FROM Flight WHERE flightId = Passenger.flightId AND destination = 'London');`                   | Rechercher les passagers avec un vol à destination de Londres.        |                                         |
| **Difficile**| `SELECT COUNT(*) FROM Passenger p WHERE p.flightId = 1;`                                                                                       | Compter le nombre de passagers sur un vol spécifique.                 |                                         |
| **Difficile**| `SELECT * FROM Flight WHERE destination = 'Paris' ORDER BY departureTime DESC;`                                                                | Rechercher les vols vers Paris, triés par ordre décroissant de départ.|                                         |
| **Difficile**| `SELECT SUM(seatNumber) FROM Passenger WHERE flightId = 1;`                                                                                    | Calculer la somme des numéros de siège d'un vol donné.                |                                         |

### Rappel :

- **Airport** : La classe `Airport` contient `airportId` comme clé primaire (PK).
- **Flight** : La classe `Flight` contient `flightId` comme clé primaire (PK) et `airportId` comme clé étrangère (FK).
- **Passenger** : La classe `Passenger` contient `passengerId` comme clé primaire (PK) et `flightId` comme clé étrangère (FK).

### Critères de notation :

- **Total de 100 points**, avec 5 points pour chaque question.
- Les méthodes doivent suivre la convention de nommage de **Spring Data JPA** et utiliser les bons opérateurs.
- L’évaluation inclut des requêtes SQL simples, des jointures, et des agrégations.
