Chers étudiant.e.s,

Bravo à tous pour vos efforts et votre participation au questionnaire. Comme promis, voici le **solutionnaire** complet pour vous aider à comprendre les méthodes JPA à dériver des requêtes SQL.

---

### Solutionnaire complet

| **Niveau**   | **Requête SQL**                                                                                                                               | **Indice**                                                          | **Nom de la méthode JPA**                           |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------|
| **Facile**   | `SELECT * FROM Airport;`                                                                                                                       | Récupérer tous les aéroports.                                         | `findAll()`                                         |
| **Facile**   | `SELECT * FROM Flight;`                                                                                                                        | Récupérer tous les vols.                                              | `findAll()`                                         |
| **Facile**   | `SELECT * FROM Passenger;`                                                                                                                     | Récupérer tous les passagers.                                         | `findAll()`                                         |
| **Facile**   | `SELECT * FROM Airport WHERE airportId = 1;`                                                                                                   | Récupérer un aéroport par son ID.                                     | `findByAirportId(Long airportId)`                   |
| **Facile**   | `SELECT * FROM Flight WHERE flightId = 2;`                                                                                                     | Récupérer un vol par son ID.                                          | `findByFlightId(Long flightId)`                     |
| **Facile**   | `SELECT * FROM Passenger WHERE passengerId = 3;`                                                                                               | Récupérer un passager par son ID.                                     | `findByPassengerId(Long passengerId)`               |
| **Facile**   | `SELECT * FROM Flight WHERE destination = 'Paris';`                                                                                            | Récupérer les vols vers Paris.                                        | `findByDestination(String destination)`             |
| **Facile**   | `SELECT * FROM Passenger WHERE seatNumber = '12A';`                                                                                            | Récupérer les passagers ayant le siège '12A'.                         | `findBySeatNumber(String seatNumber)`               |
| **Facile**   | `SELECT * FROM Flight WHERE departureTime > '2024-01-01';`                                                                                     | Rechercher les vols après une date donnée.                            | `findByDepartureTimeAfter(LocalDate departureTime)` |
| **Facile**   | `SELECT * FROM Passenger WHERE passengerName = 'John';`                                                                                        | Rechercher un passager par son nom.                                   | `findByPassengerName(String passengerName)`         |
| **Moyen**    | `SELECT * FROM Flight WHERE destination LIKE 'P%';`                                                                                            | Rechercher les vols vers une destination commençant par 'P'.          | `findByDestinationStartingWith(String prefix)`      |
| **Moyen**    | `SELECT * FROM Passenger WHERE seatNumber = '12A' AND flightId = 1;`                                                                           | Rechercher les passagers avec un siège spécifique sur un vol donné.   | `findBySeatNumberAndFlightId(String seatNumber, Long flightId)` |
| **Moyen**    | `SELECT COUNT(*) FROM Flight WHERE destination = 'New York';`                                                                                  | Compter les vols vers New York.                                       | `countByDestination(String destination)`            |
| **Moyen**    | `SELECT AVG(seatNumber) FROM Passenger WHERE flightId = 1;`                                                                                    | Calculer la moyenne des numéros de siège d'un vol spécifique.         | **Calcul personnalisé nécessaire (voir ci-dessous)** |
| **Moyen**    | `SELECT * FROM Flight WHERE departureTime BETWEEN '2024-01-01' AND '2024-12-31';`                                                              | Rechercher les vols entre deux dates.                                 | `findByDepartureTimeBetween(LocalDate start, LocalDate end)` |
| **Difficile**| `SELECT * FROM Passenger p JOIN Flight f ON p.flightId = f.flightId WHERE f.destination = 'Paris';`                                              | Rechercher les passagers des vols à destination de Paris.             | `findByFlightDestination(String destination)`      |
| **Difficile**| `SELECT * FROM Airport a JOIN Flight f ON a.airportId = f.airportId WHERE f.destination = 'Tokyo';`                                             | Rechercher les aéroports avec des vols à destination de Tokyo.        | `findByFlightsDestination(String destination)`     |
| **Difficile**| `SELECT * FROM Passenger WHERE EXISTS (SELECT 1 FROM Flight WHERE flightId = Passenger.flightId AND destination = 'London');`                   | Rechercher les passagers avec un vol à destination de Londres.        | `findByFlightDestination(String destination)`      |
| **Difficile**| `SELECT COUNT(*) FROM Passenger p WHERE p.flightId = 1;`                                                                                       | Compter le nombre de passagers sur un vol spécifique.                 | `countByFlightId(Long flightId)`                    |
| **Difficile**| `SELECT * FROM Flight WHERE destination = 'Paris' ORDER BY departureTime DESC;`                                                                | Rechercher les vols vers Paris, triés par ordre décroissant de départ.| `findByDestinationOrderByDepartureTimeDesc(String destination)` |
| **Difficile**| `SELECT SUM(seatNumber) FROM Passenger WHERE flightId = 1;`                                                                                    | Calculer la somme des numéros de siège d'un vol donné.                | **Calcul personnalisé nécessaire (voir ci-dessous)** |

---

### Explications pour les requêtes complexes

#### 1. Moyenne des numéros de siège (`AVG(seatNumber)`)

La requête suivante posait des questions, et voici pourquoi elle était considérée comme difficile :
```sql
SELECT AVG(seatNumber) FROM Passenger WHERE flightId = 1;
```
**Problème :** Le champ `seatNumber` contient des chaînes de caractères (comme `'12A'`), ce qui signifie que la moyenne ne peut pas être calculée directement sur ce type de données.

**Solution :** Il est nécessaire de **prétraiter les données** pour extraire la partie numérique des chaînes avant de faire la moyenne.

**Code en Java pour traiter cela** :
```java
public double calculateAverageSeatNumber(Long flightId) {
    List<String> seatNumbers = passengerRepository.findSeatNumbersByFlightId(flightId);
    List<Integer> numericSeatNumbers = seatNumbers.stream()
        .map(seat -> Integer.parseInt(seat.replaceAll("[^0-9]", "")))
        .collect(Collectors.toList());

    return numericSeatNumbers.stream()
        .mapToInt(Integer::intValue)
        .average()
        .orElse(0); // Si aucun résultat, retourne 0
}
```

#### 2. Somme des numéros de siège (`SUM(seatNumber)`)

De manière similaire à la moyenne, la somme nécessite aussi l'extraction des parties numériques avant de pouvoir être calculée.

---

### Conclusion

Ces méthodes JPA dérivées des requêtes SQL montrent comment manipuler les données dans un projet Spring Boot. Certaines questions impliquaient une logique plus complexe et des manipulations dans le code Java, comme pour la moyenne et la somme des numéros de siège.

N'oubliez pas que ces défis font partie de votre apprentissage pour devenir des experts dans la manipulation des bases de données et des frameworks comme **Spring Boot**.

Si vous avez des questions ou avez besoin d'éclaircissements supplémentaires, n'hésitez pas à me contacter.

Bonne continuation dans vos études ! 👨‍🎓👩‍🎓

Cordialement,  
**Haythem Rehouma**
