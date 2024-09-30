# **Examen Partie 2 : Compléter les annotations et les appels API**

- L'objectif de cet exercice est de compléter les annotations et les appels API dans un contrôleur REST pour la gestion des **véhicules** dans un **garage automobile**.
- Plusieurs possibilités sont offertes pour chaque annotation ainsi que pour les appels API.
- Vous devez choisir celles qui vous semblent les plus appropriées.

---

# 1. Compléter les annotations manquantes pour que cette classe puisse répondre aux requêtes HTTP

# 📢

```java
// Compléter les annotations manquantes pour que cette classe gère les véhicules via des requêtes HTTP

____(1)____

public class VehiculeController {

    // Gérer les requêtes GET pour lister tous les véhicules disponibles
    ____(2)____

    public List<Vehicule> getAllVehicules() {
        return Arrays.asList(
            new Vehicule(1, "Toyota", "Corolla"),
            new Vehicule(2, "Honda", "Civic")
        );
    }

    // Gérer les requêtes POST pour ajouter un nouveau véhicule
    ____(3)____

    public Vehicule addVehicule(____(4)____) {
        return vehicule;
    }

    // Gérer les requêtes GET pour récupérer un véhicule par son ID
    ____(5)____

    public Vehicule getVehiculeById(____(6)____) {
        return new Vehicule(vehiculeId, "Véhicule Existant", "Modèle Inconnu");
    }
}
```

# Explications :
- **(1)** : Cette annotation doit indiquer que la classe `VehiculeController` est un contrôleur REST. Cela signifie que cette classe va gérer des requêtes HTTP pour interagir avec les ressources liées aux **véhicules**.
  
- **(2)** : Ici, il faut ajouter une annotation pour indiquer que cette méthode `getAllVehicules()` doit répondre aux requêtes **GET** sur l'URL `/vehicules`, permettant de récupérer la liste de tous les véhicules disponibles.

- **(3)** : Cette annotation doit indiquer que la méthode `addVehicule()` va traiter des requêtes **POST** pour permettre l'ajout d'un nouveau véhicule. L'URL doit refléter cette action.

- **(4)** : Il faut spécifier que l'objet véhicule sera passé dans le **corps** de la requête HTTP. Cette annotation permet de lier le contenu du corps de la requête à l'objet `Vehicule` qui est manipulé dans la méthode.

- **(5)** : La méthode `getVehiculeById()` doit être configurée pour répondre aux requêtes **GET** lorsqu'un véhicule est récupéré via son **ID**. L'URL doit contenir l'ID du véhicule à récupérer.

- **(6)** : Vous devez indiquer que l'ID du véhicule sera transmis dans l'URL de la requête. Cette annotation permet de lier l'ID dans l'URL au paramètre `vehiculeId` dans la méthode.

---

# 2. Compléter les appels API pour chaque méthode

# 📢

#### **Récupérer tous les véhicules**

Cet appel doit pointer sur la méthode `getAllVehicules()`, qui renvoie la liste de tous les véhicules disponibles.

```http
### Possibilité 1
____(7)____ http://localhost:8080/vehicules
Accept: application/json
```

- **Explication** : Cet appel permet d'envoyer une requête pour récupérer la liste des véhicules. Vous devez indiquer ici quel type de méthode HTTP est utilisé et quel format de réponse est attendu, tel que JSON.

```http
### Possibilité 2
____(8)____ http://localhost:8080/vehicules
Accept: application/xml
```

- **Explication** : Cet appel est similaire au précédent mais spécifie que la réponse doit être au format XML. Choisissez le bon type de méthode HTTP et format.

#### **Ajouter un nouveau véhicule**

Cet appel doit pointer sur la méthode `addVehicule()`, qui permet d'ajouter un nouveau véhicule.

```http
### Possibilité 1
____(9)____ http://localhost:8080/vehicules/ajouter
Content-Type: application/json

{
  "id": 3,
  "marque": "Ford",
  "modele": "Focus"
}
```

- **Explication** : Cet appel permet d'envoyer une requête pour ajouter un véhicule. Vous devez choisir le type de méthode HTTP approprié pour l'ajout, et spécifier que les données du véhicule seront envoyées dans le corps de la requête, au format JSON.

#### **Récupérer un véhicule par son ID**

Cet appel doit pointer sur la méthode `getVehiculeById()`, qui permet de récupérer un véhicule spécifique en fonction de son ID.

```http
### Possibilité 1
____(10)____ http://localhost:8080/vehicules/id/1
Accept: application/json
```

- **Explication** : Cet appel permet de récupérer un véhicule spécifique en fournissant son ID dans l'URL. Vous devez indiquer le type de méthode HTTP à utiliser et choisir une URL qui contient un paramètre d'ID.

---

# **Annexe - Modèle de la classe Vehicule**

```java
public class Vehicule {

    private int id;  // ID unique pour chaque véhicule
    private String marque;  // Marque du véhicule
    private String modele;  // Modèle du véhicule

    // Constructeur par défaut
    public Vehicule() {
    }

    // Constructeur avec paramètres
    public Vehicule(int id, String marque, String modele) {
        this.id = id;
        this.marque = marque;
        this.modele = modele;
    }

    // Getters et Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getMarque() {
        return marque;
    }

    public void setMarque(String marque) {
        this.marque = marque;
    }

    public String getModele() {
        return modele;
    }

    public void setModele(String modele) {
        this.modele = modele;
    }

    @Override
    public String toString() {
        return "Vehicule{" +
                "id=" + id +
                ", marque='" + marque + '\'' +
                ", modele='" + modele + '\'' +
                '}';
    }
}
```

---

### **Explication des éléments du modèle :**

- **Attributs :**
  - `id` : Identifiant unique pour chaque véhicule.
  - `marque` : La marque du véhicule (ex. Toyota, Honda).
  - `modele` : Le modèle du véhicule (ex. Corolla, Civic).

- **Constructeur** :
  - Le constructeur permet de créer des instances de la classe `Vehicule` avec un ID, une marque et un modèle.

- **Getters et Setters** :
  - Ces méthodes permettent d'accéder aux attributs et de les modifier.

- **Méthode `toString()`** :
  - Elle est utilisée pour obtenir une représentation sous forme de chaîne de caractères de l'objet `Vehicule`.
