# **Examen Partie 2 : Compléter les annotations et les appels API**


- L'objectif de cet exercice est de compléter les annotations et les appels API dans un contrôleur REST pour la gestion des médicaments dans une pharmacie. 
- Plusieurs possibilités sont offertes pour chaque annotation ainsi que pour les appels API. 
- Vous devez choisir celles qui vous semblent les plus appropriées.

---

# 1. Compléter les annotations manquantes pour que cette classe puisse répondre aux requêtes HTTP

# 📢

```java
// Compléter les annotations manquantes pour que cette classe gère les médicaments via des requêtes HTTP

____(1)____

public class MedicamentController {

    // Gérer les requêtes GET pour lister tous les médicaments disponibles
    ____(2)____

    public List<Medicament> getAllMedicaments() {
        return Arrays.asList(
            new Medicament(1, "Paracétamol", "Analgésique"),
            new Medicament(2, "Ibuprofène", "Anti-inflammatoire")
        );
    }

    // Gérer les requêtes POST pour ajouter un nouveau médicament
    ____(3)____

    public Medicament addMedicament(____(4)____) {
        return medicament;
    }

    // Gérer les requêtes GET pour récupérer un médicament par son ID
    ____(5)____

    public Medicament getMedicamentById(____(6)____) {
        return new Medicament(medicamentId, "Médicament Existant", "Catégorie Inconnue");
    }
}
```

# Explications :
- **(1)** : Cette annotation doit indiquer que la classe `MedicamentController` est un contrôleur REST. Cela signifie que cette classe va gérer des requêtes HTTP pour interagir avec les ressources liées aux médicaments.
  
- **(2)** : Ici, il faut ajouter une annotation pour indiquer que cette méthode `getAllMedicaments()` doit répondre aux requêtes **GET** sur l'URL `/medicaments`, permettant de récupérer la liste de tous les médicaments disponibles.

- **(3)** : Cette annotation doit indiquer que la méthode `addMedicament()` va traiter des requêtes **POST** pour permettre l'ajout d'un nouveau médicament. L'URL doit refléter cette action.

- **(4)** : Il faut spécifier que l'objet médicament sera passé dans le **corps** de la requête HTTP. Cette annotation permet de lier le contenu du corps de la requête à l'objet `Medicament` qui est manipulé dans la méthode.

- **(5)** : La méthode `getMedicamentById()` doit être configurée pour répondre aux requêtes **GET** lorsqu'un médicament est récupéré via son **ID**. L'URL doit contenir l'ID du médicament à récupérer.

- **(6)** : Vous devez indiquer que l'ID du médicament sera transmis dans l'URL de la requête. Cette annotation permet de lier l'ID dans l'URL au paramètre `medicamentId` dans la méthode.

---

# 2. Compléter les appels API pour chaque méthode

# 📢

#### **Récupérer tous les médicaments**

Cet appel doit pointer sur la méthode `getAllMedicaments()`, qui renvoie la liste de tous les médicaments disponibles.

```http
### Possibilité 1
____(7)____ http://localhost:8080/medicaments
Accept: application/json
```

- **Explication** : Cet appel permet d'envoyer une requête pour récupérer la liste des médicaments. Vous devez indiquer ici quel type de méthode HTTP est utilisé et quel format de réponse est attendu, tel que JSON.

```http
### Possibilité 2
____(8)____ http://localhost:8080/medicaments
Accept: application/xml
```

- **Explication** : Cet appel est similaire au précédent mais spécifie que la réponse doit être au format XML. Choisissez le bon type de méthode HTTP et format.

#### **Ajouter un nouveau médicament**

Cet appel doit pointer sur la méthode `addMedicament()`, qui permet d'ajouter un nouveau médicament.

```http
### Possibilité 1
____(9)____ http://localhost:8080/medicaments/ajouter
Content-Type: application/json

{
  "id": 3,
  "nom": "Aspirine",
  "categorie": "Analgésique"
}
```

- **Explication** : Cet appel permet d'envoyer une requête pour ajouter un médicament. Vous devez choisir le type de méthode HTTP approprié pour l'ajout, et spécifier que les données du médicament seront envoyées dans le corps de la requête, au format JSON.

#### **Récupérer un médicament par son ID**

Cet appel doit pointer sur la méthode `getMedicamentById()`, qui permet de récupérer un médicament spécifique en fonction de son ID.

```http
### Possibilité 1
____(10)____ http://localhost:8080/medicaments/id/1
Accept: application/json
```

- **Explication** : Cet appel permet de récupérer un médicament spécifique en fournissant son ID dans l'URL. Vous devez indiquer le type de méthode HTTP à utiliser et choisir une URL qui contient un paramètre d'ID.




# **Annexe - Modèle de la classe Medicament**

```java
public class Medicament {

    private int id;  // ID unique pour chaque médicament
    private String nom;  // Nom du médicament
    private String categorie;  // Catégorie ou type de médicament

    // Constructeur par défaut
    public Medicament() {
    }

    // Constructeur avec paramètres
    public Medicament(int id, String nom, String categorie) {
        this.id = id;
        this.nom = nom;
        this.categorie = categorie;
    }

    // Getters et Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNom() {
        return nom;
    }

    public void setNom(String nom) {
        this.nom = nom;
    }

    public String getCategorie() {
        return categorie;
    }

    public void setCategorie(String categorie) {
        this.categorie = categorie;
    }

    @Override
    public String toString() {
        return "Medicament{" +
                "id=" + id +
                ", nom='" + nom + '\'' +
                ", categorie='" + categorie + '\'' +
                '}';
    }
}
```

---

### **Explication des éléments du modèle :**

- **Attributs :**
  - `id` : Identifiant unique pour chaque médicament.
  - `nom` : Le nom du médicament (ex. Paracétamol, Ibuprofène).
  - `categorie` : La catégorie à laquelle appartient le médicament (ex. Analgésique, Anti-inflammatoire).

- **Constructeur** :
  - Le constructeur permet de créer des instances de la classe `Medicament` avec un ID, un nom et une catégorie.

- **Getters et Setters** :
  - Ces méthodes permettent d'accéder aux attributs et de les modifier.

- **Méthode `toString()`** :
  - Elle est utilisée pour obtenir une représentation sous forme de chaîne de caractères de l'objet `Medicament`.


