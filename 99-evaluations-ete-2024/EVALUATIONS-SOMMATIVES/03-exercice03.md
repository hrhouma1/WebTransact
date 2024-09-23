# **Examen Partie 3 : Implémenter un contrôleur REST pour la gestion des étudiants**

- L'objectif est de créer un projet Spring Boot en utilisant Spring Initializr. 
- Une fois le projet généré, vous devez implémenter un contrôleur REST pour la gestion des étudiants dans une base de données.
- **Vous n'êtes pas tenus d'implémenter une base de données, cela peut être réalisé en mémoire en utilisant une liste d'étudiants.**

---

# Instructions

1. **Générer le projet Spring Boot**  
Utilisez Spring Initializr pour générer votre projet Spring Boot. Téléchargez le projet sous forme de fichier ZIP.

2. **Implémenter la classe `Student`**  
Créez la classe `Student` avec les champs suivants :
   - `id` (int) : identifiant unique de l'étudiant.
   - `name` (String) : nom de l'étudiant.
   - `email` (String) : adresse e-mail de l'étudiant.
   - `enrollmentYear` (int) : année d'inscription de l'étudiant.

3. **Créer et tester le contrôleur `StudentController`**  
   - Implémentez les méthodes pour ajouter, récupérer, modifier et supprimer des étudiants (CRUD).
   - **Utilisez une simple liste en mémoire** pour stocker les étudiants (pas besoin d'une base de données).
   - Testez les appels API via les méthodes HTTP appropriées.

---

# Ce que vous devez me fournir :

1. Le fichier ZIP contenant le projet Spring Boot complet.
2. Des captures d'écran montrant vos tests de l'API avec Postman ou un fichier `.http`.
