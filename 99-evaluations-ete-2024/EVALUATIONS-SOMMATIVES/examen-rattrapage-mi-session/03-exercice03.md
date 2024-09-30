# **Examen Partie 3 : Implémenter un contrôleur REST pour la gestion des cartes bancaires**

- L'objectif est de créer un projet Spring Boot en utilisant Spring Initializr.
- Une fois le projet généré, vous devez implémenter un contrôleur REST pour la gestion des **cartes bancaires** (carte de crédit, carte de débit, etc.) dans une base de données.
- **Vous n'êtes pas tenus d'implémenter une base de données, cela peut être réalisé en mémoire en utilisant une liste de cartes.**

---

# Instructions

1. **Générer le projet Spring Boot**  
Utilisez [Spring Initializr](https://start.spring.io/) pour générer votre projet Spring Boot. Téléchargez le projet sous forme de fichier ZIP.

2. **Implémenter la classe `Card`**  
Créez la classe `Card` avec les champs suivants :
   - `id` (int) : identifiant unique de la carte.
   - `holderName` (String) : nom du détenteur de la carte.
   - `type` (String) : type de la carte (Crédit, Débit, etc.).
   - `cardNumber` (String) : numéro de la carte.

3. **Créer et tester le contrôleur `CardController`**  
   - Implémentez les méthodes pour ajouter, récupérer, modifier et supprimer des cartes (CRUD).
   - **Utilisez une simple liste en mémoire** pour stocker les cartes (pas besoin d'une base de données).
   - Testez les appels API via les méthodes HTTP appropriées avec des outils comme Postman ou un fichier `.http`.

---

# Méthodes à implémenter dans `CardController` :

1. **GET /cards**  
   Récupérer la liste de toutes les cartes.

2. **GET /cards/{id}**  
   Récupérer les détails d'une carte par son ID.

3. **POST /cards**  
   Ajouter une nouvelle carte. Le corps de la requête contiendra les informations de la carte.

4. **PUT /cards/{id}**  
   Modifier les informations d'une carte existante.

5. **DELETE /cards/{id}**  
   Supprimer une carte par son ID.

---

# Ce que vous devez me fournir :

1. Le fichier ZIP contenant le projet Spring Boot complet.
2. Des captures d'écran montrant vos tests de l'API avec Postman ou un fichier `.http`.

