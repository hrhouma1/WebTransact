# Tutoriel : Explication de la question la plus difficile du quiz

Bonjour à tous,

Je tiens à vous féliciter pour vos efforts dans ce quiz. Je sais que certaines questions étaient plus complexes que d’autres, et je souhaite aujourd’hui vous présenter celle qui a été classée comme la **plus difficile**. Cette question portait sur le calcul de la **moyenne des numéros de siège**, une question qui peut paraître simple à première vue, mais qui cache une réelle complexité liée à la nature des données.

## La question

Voici la question que vous avez rencontrée :

```sql
SELECT AVG(seatNumber) FROM Passenger WHERE flightId = 1;
```

### Le contexte :
Le champ `seatNumber` dans la base de données contient des chaînes de caractères comme `'12A'`, `'14B'`, etc., où les numéros de sièges ne sont pas simplement des entiers, mais des combinaisons de chiffres et de lettres.

### Le problème :
La question semble demander de calculer une moyenne sur le champ `seatNumber`, mais **le problème réside dans le fait que ces données sont de type chaîne (`String`)**, et non pas des entiers. Calculer une moyenne directement sur ce type de données n’est pas possible sans prétraiter les données.

## La solution

Pour résoudre cette question, il fallait comprendre qu’avant de calculer la moyenne, il est nécessaire de **prétraiter les données** et d'extraire la partie **numérique** des numéros de siège.

### Étapes à suivre :

1. **Extraire la partie numérique des chaînes** :
   - Pour cela, on utilise une méthode qui supprime les caractères non numériques d'une chaîne (par exemple `'12A'` devient `'12'`).
   
2. **Convertir la chaîne en entier** :
   - Une fois la partie numérique extraite, on peut la convertir en entier (par exemple `'12'` devient `12`).

3. **Calculer la moyenne** :
   - Une fois les données converties en entiers, il est possible de calculer la moyenne.

### Exemple de code en Java (Spring Boot)

Voici comment cela pourrait être implémenté en Java dans une application Spring Boot :

#### Récupération des données (JPQL) :
On commence par récupérer les numéros de siège pour un vol spécifique en utilisant une requête JPQL dans le repository :

```java
@Query("SELECT p.seatNumber FROM Passenger p WHERE p.flight.flightId = :flightId")
List<String> findSeatNumbersByFlightId(@Param("flightId") Long flightId);
```

#### Calcul de la moyenne après extraction des parties numériques :
Dans le service, on transforme les données pour extraire la partie numérique et calculer la moyenne :

```java
public double calculateAverageSeatNumber(Long flightId) {
    List<String> seatNumbers = passengerRepository.findSeatNumbersByFlightId(flightId);
    List<Integer> numericSeatNumbers = seatNumbers.stream()
        .map(seat -> {
            // Extraction des parties numériques des numéros de siège
            String numericPart = seat.replaceAll("[^0-9]", "");
            return Integer.parseInt(numericPart);
        })
        .collect(Collectors.toList());

    // Calcul de la moyenne des numéros de siège
    return numericSeatNumbers.stream()
        .mapToInt(Integer::intValue)
        .average()
        .orElse(0); // Si aucun résultat, retourne 0
}
```

### Explication technique :

1. **Extraction des parties numériques** :
   - La méthode `replaceAll("[^0-9]", "")` permet de supprimer tous les caractères non numériques d'une chaîne, ne conservant que les chiffres.
   
2. **Conversion en entier** :
   - Après avoir extrait les chiffres, nous utilisons `Integer.parseInt()` pour convertir la chaîne en entier.
   
3. **Calcul de la moyenne** :
   - Avec la méthode `stream()` en Java, nous appliquons `mapToInt()` pour convertir les entiers en un flux sur lequel nous pouvons ensuite calculer la moyenne avec `average()`.

### Conclusion :

Cette question est classée comme **difficile** car elle nécessite de comprendre comment manipuler des données alphanumériques avant de les utiliser dans des calculs. En réalité, il s'agit d'un problème classique que l'on rencontre souvent en traitement de données : les données brutes doivent être prétraitées pour pouvoir être exploitées correctement. Cela montre l'importance de savoir comment manipuler les chaînes de caractères et appliquer des transformations avant de faire des calculs.

Je suis sûr que vous comprenez maintenant pourquoi cette question demandait un peu plus de réflexion. Bravo à tous pour vos efforts !

Cordialement,  
**Haythem Rehouma**
