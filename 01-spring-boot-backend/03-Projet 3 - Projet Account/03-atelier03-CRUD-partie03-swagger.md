# 🏁 Intégration de Swagger dans votre Projet Spring Boot

Swagger est un outil puissant pour documenter et interagir avec votre API RESTful de manière conviviale. En suivant ces étapes, vous pouvez rapidement configurer Swagger dans votre projet Spring Boot.

---

### 1️⃣ Ajout de la Dépendance Swagger dans le `pom.xml`

Pour commencer, vous devez ajouter la dépendance nécessaire dans votre fichier `pom.xml` afin de permettre l'intégration de Swagger.

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.1.0</version>
</dependency>
```

Cette dépendance permet d'intégrer automatiquement Swagger UI dans votre projet, vous offrant une interface graphique pour tester et documenter votre API.

---

### 2️⃣ Annoter les Méthodes du Contrôleur avec `@Operation`

Swagger utilise les annotations pour documenter les différents endpoints de votre API. L'annotation `@Operation` vous permet de décrire ce que fait chaque méthode du contrôleur.

#### Exemple d'annotations dans `AccountsController` :

```java
@RestController
public class AccountsController {
    
    @Autowired
    private AccountsService accountsService;

    @Operation(summary = "Get account by ID")
    @GetMapping("/myAccount/{id}")
    public Accounts getAccountDetails(@PathVariable("id") Long id) {
        return accountsService.getAccountsById(id);
    }

    @Operation(summary = "Get all accounts")
    @GetMapping("/accounts")
    public List<Accounts> getAllAccounts() {
        return accountsService.getAllAccounts();
    }

    @Operation(summary = "Create a new account")
    @PostMapping("/newAccount")
    public String newAccount(@RequestBody Accounts accounts) {
        return accountsService.save(accounts);
    }
}
```

Ces annotations permettent de générer automatiquement la documentation des méthodes HTTP dans Swagger UI.

---

### 3️⃣ Accéder à l'Interface Swagger UI

Après avoir ajouté les annotations et démarré votre application Spring Boot, vous pouvez accéder à l'interface Swagger UI via votre navigateur pour visualiser et tester les endpoints.

#### **URL pour accéder à Swagger UI :**
- **http://localhost:8080/swagger-ui/index.html**
- **ou parfois** : **http://localhost:8080/swagger-ui/**

Cette interface vous permettra de :

- Visualiser les différents endpoints de votre API.
- Tester les requêtes directement depuis l'interface.
- Comprendre les paramètres requis et les réponses attendues.

---

### 🛠️ Test et Vérification

1. **Démarrez votre application Spring Boot** : Exécutez votre application pour que Swagger UI soit disponible.
2. **Ouvrez Swagger UI** : Utilisez l'une des URLs fournies ci-dessus dans votre navigateur.
3. **Testez les Endpoints** : Utilisez l'interface Swagger pour envoyer des requêtes aux différents endpoints et vérifier les réponses.

Swagger facilite non seulement la documentation, mais permet aussi une collaboration simplifiée entre développeurs en offrant une vue d'ensemble claire de votre API.
- En suivant ce guide, vous avez maintenant intégré Swagger dans votre projet Spring Boot, documenté vos endpoints, et vous pouvez tester facilement votre API.
- Cela rendra votre application plus facile à maintenir et à utiliser pour vous-même et pour les autres développeurs.
