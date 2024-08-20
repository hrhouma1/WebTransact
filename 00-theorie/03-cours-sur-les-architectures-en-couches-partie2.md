# Architecture et le flux de données dans notre application Spring Boot.


```plaintext
   +----------------------------+
   |      AccountsApplication    |
   |        (Main Class)         |
   +----------------------------+
             |
             v
   +----------------------------+       +----------------------------+       +----------------------------+
   |     AccountsController      |<------|      AccountsService       |<------|    AccountsRepository      |
   |        (Controller)         |       |         (Service)          |       |       (Repository)          |
   +----------------------------+       +----------------------------+       +----------------------------+
             |                                      |                                      |
             |                                      |                                      |
             v                                      v                                      v
   +----------------------------+       +----------------------------+       +----------------------------+
   |        @GetMapping          |       |  Logic for business rules  |       |   Extends CrudRepository    |
   |    @PostMapping methods     |       |   like CRUD operations     |       |                            |
   |   Interacts with Service    |       |   Interacts with Repo      |       |    Interacts with Database  |
   +----------------------------+       +----------------------------+       +----------------------------+
             |
             v
   +----------------------------+
   |        Accounts.java        |
   |          (Model)            |
   +----------------------------+
             |
             v
   +----------------------------+
   |       Database (H2)         |
   |  Stores account information |
   +----------------------------+
```

# Explication des Flèches et du Flux de Données :

1. **Architecture een couche** :
   - **Controller → Service** : Le **Controller** fait appel au **Service** pour exécuter la logique métier.
   - **Service → Repository** : Le **Service** utilise le **Repository** pour interagir avec la base de données.
 

3. **Flux de Données** :
   - **Controller** reçoit une demande du client et la transmet au **Service**.
   - **Service** applique la logique métier et interagit avec le **Repository** pour accéder à la base de données.
   - **Repository** communique avec la base de données et renvoie les résultats au **Service**, qui les transmet ensuite au **Controller**.

4. **Injection de Dépendances avec `@Autowired`** :
   - **Controller** dépend du **Service** et **Service** dépend du **Repository**. Ces dépendances sont injectées par Spring via l'annotation `@Autowired`.



# Évaluation Formative:

1. Existe-t-il d'autres mécanismes pour l'injection de dépendances en Spring ? Si oui, décrivez et comparez-les avec l'annotation `@Autowired`.
2. En quoi ces mécanismes diffèrent-ils en termes de performance et de flexibilité ?
3. Dans quels cas spécifiques serait-il préférable d'utiliser un mécanisme plutôt que l'autre ?
