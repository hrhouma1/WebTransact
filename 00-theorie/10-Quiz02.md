# 📚 **Quiz Spring Boot**

### **Aperçu**

Testez vos connaissances sur les annotations essentielles de Spring Boot avec ce quiz de 50 questions. Chaque question est accompagnée de plusieurs choix, mais une seule réponse est correcte. Bonne chance ! 🚀

---

### **Quiz**

1. **Quelle annotation est utilisée pour marquer une classe comme un contrôleur REST dans Spring Boot ?**  
   - `@Service`  
   - `@RestController`  
   - `@Repository`  
   - `@Autowired`

2. **Quelle annotation permet de mapper les requêtes HTTP aux méthodes d'un contrôleur ?**  
   - `@GetMapping`  
   - `@PostMapping`  
   - `@RequestMapping`  
   - `@Query`

3. **Quelle annotation est utilisée pour injecter automatiquement les dépendances dans Spring Boot ?**  
   - `@Inject`  
   - `@Autowired`  
   - `@Resource`  
   - `@Provide`

4. **Quelle annotation marque une classe comme un service dans Spring Boot ?**  
   - `@Controller`  
   - `@Entity`  
   - `@Service`  
   - `@Component`

5. **Pour mapper les variables de chemin d'une URL, quelle annotation est utilisée ?**  
   - `@RequestParam`  
   - `@PathVariable`  
   - `@RequestBody`  
   - `@RequestHeader`

6. **Quelle annotation est utilisée pour gérer les transactions de base de données dans Spring Boot ?**  
   - `@Transactional`  
   - `@PersistenceContext`  
   - `@Entity`  
   - `@Query`

7. **Quelle annotation permet de spécifier un bean à injecter lorsqu'il existe plusieurs beans du même type ?**  
   - `@Primary`  
   - `@Autowired`  
   - `@Qualifier`  
   - `@Inject`

8. **Pour planifier l'exécution de méthodes à des intervalles réguliers, quelle annotation est utilisée ?**  
   - `@Scheduled`  
   - `@Async`  
   - `@EnableScheduling`  
   - `@Cron`

9. **Quelle annotation est utilisée pour activer la mise en cache dans une application Spring ?**  
   - `@Cacheable`  
   - `@EnableCaching`  
   - `@CacheEvict`  
   - `@CachePut`

10. **Pour valider les données saisies par l'utilisateur avant de les traiter, quelle annotation est utilisée ?**  
    - `@Valid`  
    - `@Validation`  
    - `@Validated`  
    - `@Check`

11. **Quelle annotation est utilisée pour définir des tâches à exécuter de manière asynchrone dans Spring Boot ?**  
    - `@Async`  
    - `@Scheduled`  
    - `@EnableAsync`  
    - `@Task`

12. **Quelle annotation permet de lier une propriété de fichier de configuration à un champ dans une classe Spring Boot ?**  
    - `@Value`  
    - `@PropertySource`  
    - `@Configuration`  
    - `@Environment`

13. **Pour mapper une méthode de contrôleur à une requête HTTP GET, quelle annotation est utilisée ?**  
    - `@PostMapping`  
    - `@GetMapping`  
    - `@RequestMapping`  
    - `@PutMapping`

14. **Quelle annotation est utilisée pour marquer une classe comme un composant, permettant à Spring de détecter automatiquement et de gérer le bean ?**  
    - `@Bean`  
    - `@Component`  
    - `@Service`  
    - `@Entity`

15. **Quelle annotation est utilisée dans Spring Boot pour mapper une méthode de contrôleur à une requête HTTP POST ?**  
    - `@GetMapping`  
    - `@PostMapping`  
    - `@RequestMapping(method = RequestMethod.POST)`  
    - `@SubmitMapping`

16. **Pour extraire les en-têtes d'une requête HTTP, quelle annotation est utilisée ?**  
    - `@RequestHeader`  
    - `@Header`  
    - `@HttpHeader`  
    - `@RequestLine`

17. **Quelle annotation est utilisée pour récupérer le corps d'une requête HTTP sous forme d'objet Java ?**  
    - `@RequestBody`  
    - `@RequestPayload`  
    - `@InputBody`  
    - `@PostBody`

18. **Pour spécifier le code de statut HTTP d'une réponse, quelle annotation est utilisée ?**  
    - `@ResponseStatus`  
    - `@HttpCode`  
    - `@StatusCode`  
    - `@ResponseCode`

19. **Quelle annotation est utilisée pour gérer les exceptions spécifiques dans les contrôleurs de Spring Boot ?**  
    - `@ErrorHandler`  
    - `@ExceptionCatcher`  
    - `@ExceptionHandler`  
    - `@Catch`

20. **Quelle annotation est utilisée pour marquer une méthode qui doit être exécutée avant chaque test unitaire dans un contexte Spring Boot ?**  
    - `@BeforeTest`  
    - `@PreTest`  
    - `@BeforeEach`  
    - `@Before`

21. **Quelle annotation Spring Boot est utilisée pour déclarer qu'une méthode doit être exécutée après chaque test unitaire ?**  
    - `@AfterEach`  
    - `@PostTest`  
    - `@AfterTest`  
    - `@Cleanup`

22. **Quelle annotation permet d'activer la découverte de composants dans les packages spécifiés ?**  
    - `@ComponentScan`  
    - `@EnableAutoConfiguration`  
    - `@ScanComponents`  
    - `@Discover`

23. **Pour spécifier des profils Spring actifs dans un test, quelle annotation est utilisée ?**  
    - `@ActiveProfiles`  
    - `@Profile`  
    - `@UseProfiles`  
    - `@Profiles`

24. **Quelle annotation est utilisée pour marquer une méthode de configuration qui retourne un bean Spring ?**  
    - `@Bean`  
    - `@Provide`  
    - `@CreateBean`  
    - `@NewBean`

25. **Pour tester les contrôleurs Spring MVC sans démarrer le serveur, quelle annotation est utilisée ?**  
    - `@WebMvcTest`  
    - `@ControllerTest`  
    - `@MvcTest`  
    - `@SpringMvcTest`

26. **Quelle annotation est utilisée pour injecter une valeur de propriété dans un champ ?**  
    - `@Value`  
    - `@Property`  
    - `@InjectValue`  
    - `@ConfigValue`

27. **Quelle annotation permet de marquer une interface comme un repository Spring Data ?**  
    - `@Repository`  
    - `@DataRepository`  
    - `@EntityRepository`  
    - `@InterfaceRepository`

28. **Pour exécuter une méthode de manière asynchrone dans une application Spring, quelle annotation est utilisée ?**  
    - `@Async`  
    - `@Asynchronous`  
    - `@RunAsync`  
    - `@ExecuteAsync`

29. **Quelle annotation est utilisée pour définir qu'une classe est une entité JPA ?**  
    - `@Entity`  
    - `@JpaEntity`  
    - `@DbEntity`  
    - `@Persistable`

30. **Pour autoriser les requêtes cross-origin sur un contrôleur ou une méthode de contrôleur, quelle annotation est utilisée ?**  
    - `@CrossOrigin`  
    - `@AllowCrossOrigin`  
    - `@EnableCors`  
    - `@Cors`

31. **Qu'est-ce que ResponseEntity dans Spring Boot et à quoi sert-il ?**  
    - Un objet qui représente la réponse HTTP, y compris le statut, les headers, et le corps.  
    - Une entité JPA pour mapper les tables de base de données.  
    - Un composant pour injecter des dépendances.  
    - Un outil pour configurer la sécurité de l'application.

32. **Comment retourner une réponse HTTP 404 NOT FOUND en utilisant ResponseEntity ?**  
    - `return new ResponseEntity<>(HttpStatus.NOT_FOUND);`  
    - `return ResponseEntity.notFound().build();`  
    - `return ResponseEntity.status(200).body();`  
    - `return ResponseEntity.ok();`

33. **Quelle est l'utilité de la pagination dans les APIs REST et comment Spring Data JPA la supporte ?**  
    - Pour limiter le nombre de requêtes à la base de données, en utilisant l'annotation `@Limit`.  
    - Pour augmenter la sécurité des données, par l'emploi de `@SecurePage`.  
    - Pour améliorer la performance et l'expérience utilisateur, en retournant les données en petites portions via `Pageable`.  
    - Pour compresser les données envoyées au client, grâce à `@Compress`.

34. **Dans un repository JPA, quelle interface permet d'implémenter la pagination ?**  
    - `CrudRepository`  
    - `JpaRepository`  
    - `PagingAndSortingRepository`  
    - `SimpleJpaRepository`

35. **Comment spécifier une requête JPQL pour chercher des entités tout en supportant la pagination ?**  
    - En utilisant `@Query` au-dessus d'une méthode de repository et en passant `Pageable` comme paramètre.  
    -

 En déclarant une méthode dans le repository avec un retour de type `List` et en ajoutant manuellement des paramètres de pagination.  
    - En utilisant `@Pagination` sur les entités JPA.  
    - Par l'annotation `@EnableJpqlPagination` au niveau de la classe d'application principale.

36. **Quelle méthode ResponseEntity permet de personnaliser entièrement la réponse, y compris le statut, les headers, et le corps ?**  
    - `ResponseEntity.ok()`  
    - `ResponseEntity.status(HttpStatus.OK)`  
    - `ResponseEntity.headers()`  
    - `ResponseEntity.body()`

37. **Comment effectuer une pagination dans une requête SQL native avec Spring Data JPA ?**  
    - En utilisant `@Query(nativeQuery = true)` avec un paramètre `Pageable`.  
    - En ajoutant des clauses `LIMIT` et `OFFSET` directement dans la requête SQL.  
    - Il n'est pas possible d'utiliser la pagination avec des requêtes SQL natives.  
    - En utilisant `@NativePagination`.

38. **Quelle est la différence principale entre `Page<T>` et `Slice<T>` dans Spring Data ?**  
    - `Page<T>` contient des informations sur le nombre total de pages, tandis que `Slice<T>` ne fournit que les données de la page courante sans calculer le total.  
    - `Slice<T>` est utilisé exclusivement pour les données JSON, tandis que `Page<T>` est pour les données XML.  
    - `Page<T>` est obsolète et `Slice<T>` est la nouvelle API.  
    - Aucune différence; `Page<T>` et `Slice<T>` sont interchangeables.

39. **Quel est le rôle principal de ResponseEntity dans un contrôleur Spring Boot ?**  
    - Exécuter des requêtes de base de données  
    - Injecter des dépendances dans les beans  
    - Gérer la pagination des données  
    - Personnaliser les réponses HTTP

40. **Comment retourner une réponse HTTP 404 NOT FOUND en utilisant ResponseEntity ?**  
    - `return new ResponseEntity<>(HttpStatus.NOT_FOUND);`  
    - `return ResponseEntity.notFound().build();`  
    - `return ResponseEntity.ok().body("Not Found");`  
    - `return ResponseEntity.status(HttpStatus.OK);`

41. **Pour implémenter une pagination dans Spring Data JPA, quelle interface est principalement utilisée ?**  
    - `CrudRepository`  
    - `JpaRepository`  
    - `PagingAndSortingRepository`  
    - `PageableRepository`

42. **Quelle méthode de l'interface `Pageable` est utilisée pour créer un objet `PageRequest` avec tri pour la pagination ?**  
    - `PageRequest.of(page, size, Sort.by("property"));`  
    - `Pageable.newRequest(page, size);`  
    - `Pageable.request(page, size, direction, "property");`  
    - `PageRequest.create(page, size, "property");`

43. **Dans JPQL, comment spécifier une clause de pagination pour limiter les résultats d'une requête ?**  
    - Ajout de `LIMIT` et `OFFSET` à la fin de la requête JPQL  
    - Utilisation des méthodes `setFirstResult()` et `setMaxResults()` sur la `Query`  
    - JPQL supporte directement les mots-clés `PAGE` et `SIZE`  
    - La pagination n'est pas supportée en JPQL

44. **Quel est l'avantage d'utiliser `Page` de Spring Data pour les résultats de pagination ?**  
    - Il permet un accès direct à la base de données.  
    - Il offre des méthodes supplémentaires pour la manipulation des données.  
    - Il fournit des informations détaillées sur l'état de la pagination, comme le nombre total de pages.  
    - Il augmente la vitesse de la requête.

45. **Quand utiliser `ResponseEntity<T>` par rapport à un type de retour simple comme `T` dans un contrôleur Spring Boot ?**  
    - Quand il n'y a pas besoin de personnaliser la réponse HTTP  
    - Quand vous avez besoin de retourner uniquement le corps de la réponse sans en-têtes ou statut HTTP  
    - Quand vous devez personnaliser la réponse HTTP, y compris le statut, les en-têtes ou le corps  
    - `ResponseEntity<T>` et `T` sont interchangeables et peuvent être utilisés dans toutes les situations

46. **Quelle annotation est utilisée pour marquer une classe Java comme entité JPA ?**  
    - `@EntityModel`  
    - `@Entity`  
    - `@TableEntity`  
    - `@JPAEntity`

47. **Quelle annotation permet de spécifier la table de base de données associée à une entité JPA ?**  
    - `@Table(name = "nom_de_la_table")`  
    - `@EntityTable(name = "nom_de_la_table")`  
    - `@DatabaseTable(name = "nom_de_la_table")`  
    - `@DbTable(name = "nom_de_la_table")`

48. **Pour insérer automatiquement la valeur de la clé primaire lors de la persistance d'une entité, quelle annotation utilise-t-on sur le champ id ?**  
    - `@GeneratedValue(strategy = GenerationType.AUTO)`  
    - `@AutoGenerate`  
    - `@PrimaryKey`  
    - `@IdAuto`

49. **Quelle annotation Spring Data est utilisée pour créer automatiquement un bean repository qui interagit avec l'entité spécifiée ?**  
    - `@EntityRepository`  
    - `@TableRepository`  
    - `@Repository`  
    - `@DataRepository`

50. **Quelle annotation est utilisée pour marquer un champ ou une propriété comme la clé primaire d'une entité ?**  
    - `@PrimaryKey`  
    - `@Id`  
    - `@Key`  
    - `@EntityId`


