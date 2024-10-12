# 03 Mise en place des tests automatises

Contenu de la leçon 03-Mise-en-place-des-tests-automatises.


```java
package com.dyma.tennis;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest
class TennisApplicationTests {

    // Injection automatique du contrôleur HealthCheck dans la classe de test
    @Autowired
    private HealthCheckController healthCheckController;

    // Injection automatique du service HealthCheck dans la classe de test
    @Autowired
    private HealthCheckService healthCheckService;

    // Injection automatique du repository HealthCheck dans la classe de test
    @Autowired
    private HealthCheckRepository healthCheckRepository;

    // Test de base qui vérifie que le contexte Spring se charge correctement
    @Test
    void contextLoads() {
        // Vérifie que le contrôleur HealthCheck n'est pas null
        assertThat(healthCheckController).isNotNull();
        
        // Vérifie que le service HealthCheck n'est pas null
        assertThat(healthCheckService).isNotNull();
        
        // Vérifie que le repository HealthCheck n'est pas null
        assertThat(healthCheckRepository).isNotNull();
    }
}
```

### Explication des commentaires :
- **Injection automatique (@Autowired)** : L'annotation `@Autowired` permet à Spring d'injecter automatiquement des instances de ces objets dans la classe de test. Cela signifie que lorsque vous exécutez le test, Spring Boot va s'assurer que les composants comme le contrôleur, le service, et le repository sont instanciés et prêts à être utilisés.
  
- **Méthode `contextLoads()`** : Ce test vérifie simplement que l'application peut démarrer correctement. Il s'assure que toutes les dépendances critiques (contrôleur, service, repository) sont bien injectées et ne sont pas nulles. C'est une bonne pratique de vérifier que le contexte Spring se charge sans erreurs.

