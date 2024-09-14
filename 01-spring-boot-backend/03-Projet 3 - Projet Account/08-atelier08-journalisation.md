# LOGGING (JOURNALISATION)

----
----

- Si vous n'avez pas réussi à compléter **l'étape 8**, vous pouvez cloner le dépôt du projet avec la commande suivante :

```bash
git clone https://github.com/hrhouma1/accounts-v2.git
```

- Cela vous fournira le code nécessaire pour continuer.

----
# PARTIE 1 - Théorie
----

Le logging dans une application Spring Boot fait référence à la pratique de l'enregistrement des messages, des événements, et des informations de débogage qui se produisent pendant l'exécution de l'application. C'est un aspect essentiel du développement et du débogage, car il permet aux développeurs de suivre ce qui se passe dans le code, d'identifier les erreurs, de diagnostiquer les problèmes et de surveiller la santé de l'application en temps réel.

Spring Boot utilise généralement le système de journalisation SLF4J (Simple Logging Facade for Java) comme façade de journalisation. Vous pouvez choisir une implémentation de SLF4J, telle que Logback ou Log4j2, pour gérer la sortie réelle des journaux. Vous pouvez également configurer différents niveaux de journalisation (par exemple, DEBUG, INFO, WARN, ERROR) pour contrôler la quantité d'informations journalisées en fonction de vos besoins.

### Configuration de la Journalisation

1. **Fichier de configuration** : 
   - Vous pouvez configurer la journalisation en créant un fichier de configuration, généralement appelé `application.properties` ou `application.yml`. 
   - Exemple :
     ```properties
     # Niveau de journalisation global
     logging.level.root=INFO
     # Configuration spécifique à une classe ou un package
     logging.level.com.example=DEBUG
     # Emplacement du fichier de journal
     logging.file=myapp.log
     ```



2. **Programmation** :
   - Vous pouvez également journaliser de manière programmatique dans votre code Java en utilisant des bibliothèques de journalisation comme SLF4J. 
   - Exemple :
     ```java
     import org.slf4j.Logger;
     import org.slf4j.LoggerFactory;

     public class MyService {
         private static final Logger logger = LoggerFactory.getLogger(MyService.class);

         public void doSomething() {
             logger.info("Exécution de doSomething()");
             // Autres opérations
         }
     }
     ```

En résumé, la journalisation dans une application Spring Boot est un élément crucial pour le développement, la maintenance, et le débogage. Elle permet de capturer des informations sur le comportement de l'application, de les stocker dans des fichiers journaux, et de les rendre disponibles pour l'analyse et la résolution de problèmes.

----
----
----
----
# PARTIE 2 - Pratique 1 et Implémentation 1 (Basique)
----

# Étapes pour Implémenter le Logging dans Spring Boot :

# 2.1. **Dépendances Maven** :
   - Assurez-vous d'avoir les dépendances appropriées dans votre fichier `pom.xml`.
   - Spring Boot inclut déjà `spring-boot-starter-logging` qui apporte des bibliothèques comme Logback, SLF4J, et Log4J2.

# 2.2. **Configuration du Logging** :
   
   - Vous pouvez configurer le logging en modifiant le fichier `application.properties` ou `application.yml`.
   - Exemple :
     
     ```properties
     logging.level.root=WARN
     logging.level.com.eazybytes=DEBUG
     logging.file.name=app.log
     logging.file.path=/logs
     logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n
     ```
     
----
###### ❗❗❗❗ Signification de logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n  ➡️➡️➡️ REGARDEZ Annexe 01 ❗❗❗❗
----


---
### ➡️➡️➡️ Résultat 1:
----
![image](https://github.com/user-attachments/assets/87cb0432-cd8b-4c0c-b57f-af1e89a0d8ae)



```
🎉 Yay ! Ça fonctionne ! 🎉 On voit app.log 🎉🎉🎉
❗❗❗❗❗❗❗ Mais attention, le dossier `logs` n'a pas été créé automatiquement. 😕😕😕😕😕
🤔 Hmmm... Pourquoi le dossier `logs` n'a-t-il pas été créé automatiquement ? 🤔
🧐 Peut-être un problème de permissions ou de configuration ?
❓ Avons-nous vérifié les chemins et les droits d'écriture ?
```




#### ➡️➡️➡️ ☠️ WARNING #1 ! 🧐
- Il se peut que tu aies un conflit entre `logging.file.name` et `logging.file.path`. Dans ce cas, nous pouvons garder uniquement "logging.file.name=.."

```
🚫 À éviter : Utiliser à la fois `logging.file.name` et `logging.file.path` (cela crée des conflits).
✅ À garder : Utiliser uniquement `logging.file.name` avec un chemin absolu vers le fichier log.
```



#### ➡️➡️➡️ ☠️ WARNING #2 ! 🧐
- Vérifie les permissions du dossier `logs`, l'application pourrait ne pas avoir les droits d'écriture. Il faut le créer dans ce cas (Ce n'est pas vraiment obligatoire dans windows).


```
🚫 À éviter : Oublier de vérifier les permissions d'écriture sur le dossier `logs`.
✅ À garder : Assure-toi que ton application a les droits d'écriture sur le répertoire `logs`.
```

#### ➡️➡️➡️ ☠️ WARNING #3 ! 🧐
- Dans *Windows*, le chemin utilisé doit être absolu, évite les chemins relatifs comme `/logs` sous Windows.

```
🚫 À éviter : Spécifier un chemin relatif comme `/logs` sous Windows.
✅ À garder : Utiliser un chemin absolu comme `C:/Users/Haythem/Desktop/accounts-v1/logs`.
```


#### ➡️➡️➡️ ☠️ WARNING #4 ! 🧐
- Assure-toi que les barres obliques sont correctement utilisées dans les chemins, sinon cela peut provoquer des erreurs.

```
🚫 À éviter : Utiliser un chemin comme `C:\Users\Haythem\Desktop\accounts-v1\log` sous Windows.
✅ À garder : Utiliser un chemin absolu comme `C:/Users/Haythem/Desktop/accounts-v1/logs`.
✅ À garder : Utiliser un chemin absolu comme `C:\\Users\\Haythem\\Desktop\\accounts-v1\\log`.
```


#### ➡️➡️➡️ ☠️ WARNING #5 ! 🧐
- Redémarre toujours ton application après avoir modifié le fichier `application.properties` pour que les changements soient pris en compte.


```
🚫 À éviter : Ne pas redémarrer l'application après modification du fichier `application.properties`.
✅ À garder : Redémarrer l'application pour appliquer les changements de configuration.
```

```properties
     logging.level.root=WARN
     logging.level.com.eazybytes=DEBUG
     logging.file.name=app.log
     logging.file.name=C:/Users/Haythem/Desktop/accounts-v1/logs/app.log
     logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n
```

---
### ➡️➡️➡️ Résultat 2:
----
![image](https://github.com/user-attachments/assets/a49e167b-670b-4926-9e2e-e1409e775d34)


```
🎉 Yay ! Ça fonctionne ! 🎉
✅ Les logs sont bien créés dans le bon répertoire.
✅ La configuration de `logging.file.name` est correcte.
✅ Plus de conflit entre `logging.file.name` et `logging.file.path`.
🚀 Tout roule parfaitement !
```


--------------------
# Résumons 📝
--------------------

#### 1 -  Utiliser uniquement `logging.file.name` avec un chemin absolu vers le fichier log. ✅✅✅
#### 2 -  Assure-toi que ton application a les droits d'écriture sur le répertoire `logs`. ✅✅✅
#### 3 -  Utiliser un chemin absolu comme `C:/Users/Haythem/Desktop/accounts-v1/logs`. ✅✅✅
#### 4 -  Utiliser un chemin absolu comme `C:\\Users\\Haythem\\Desktop\\accounts-v1\\log`. ✅✅✅
#### 5 - Redémarrer l'application pour appliquer les changements de configuration. ✅✅✅




# 2.3. **Utilisation de Logger dans le Code** :
   - Utilisez le Logger de SLF4J dans vos classes, par exemple dans `AccountsService` :
     ```java
     import org.slf4j.Logger;
     import org.slf4j.LoggerFactory;

     @Service
     public class AccountsService {

         private static final Logger logger = LoggerFactory.getLogger(AccountsService.class);

         public String save(Accounts accounts) {
             logger.debug("Saving account: {}", accounts);
             // Logique de sauvegarde...
         }
     }
     ```

### Test de l'Implémentation Basique

Pour tester l'implémentation du logging dans `AccountsService`, suivez ces étapes :

1. **Insertion d'un Compte** :
   - Créez un compte en utilisant l'endpoint POST `/newAccount`.
   - Exemple de JSON pour créer un compte :
     ```json
     {
       "accountNumber": 1,
       "customerId": 1,
       "accountType": "Checking",
       "branchAddress": "123 Main St",
       "createDt": "2023-01-02"
     }
     ```

2. **Observation des Logs** :
   - Après avoir créé le compte, vérifiez les logs générés dans la console ou dans le fichier `app.log` (selon votre configuration) pour voir les messages correspondants au niveau DEBUG, tels que :
     ```
     [2023-01-02 12:34:56] - AccountsService - DEBUG - Saving account: Accounts{accountNumber=1, customerId=1, ...}
     ```

----
###### ❗❗❗❗ Signification de logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n  ➡️➡️➡️ REGARDEZ Annexe 01 ❗❗❗❗
----

----
----
----

# PARTIE 3 - Pratique 2 et Implémentation 2 (Intermédiaire)
----

### Ajout de Logging dans `AccountsService` :

# 3.1. **Ajouter le Logger** :
   - Assurez-vous d'avoir un logger dans votre classe `AccountsService` :
     ```java
     import org.slf4j.Logger;
     import org.slf4j.LoggerFactory;

     @Service
     public class AccountsService {

         private static final Logger logger = LoggerFactory.getLogger(AccountsService.class);

         // Votre code...
     }
     ```

# 3.2. **Utilisation du Logger dans les Méthodes** :
   - Ajoutez des logs à différents niveaux dans vos méthodes :

```java
public List<Accounts> getAllAccounts() {
    // 🟢 Ajoutez cette ligne ici pour informer les utilisateurs du début de la récupération de tous les comptes
    logger.info("Fetching all accounts");
    
    List<Accounts> allAccounts = new ArrayList<>();
    accountsRepository.findAll().forEach(allAccounts::add);
    
    // 🔵 Ajoutez cette ligne ici pour informer les utilisateurs du nombre de comptes récupérés
    logger.debug("Number of accounts fetched: {}", allAccounts.size());
    
    return allAccounts;
}

public String save(Accounts accounts) {
    // 🔵 Ajoutez cette ligne ici pour déboguer la tentative de sauvegarde d'un compte
    logger.debug("Tentative de sauvegarde du compte : {}", accounts);
    
    int id = accounts.getCustomerId();
    if (customerRepository.existsById(id)) {
        accounts.setCreateDt(LocalDate.now());
        accountsRepository.save(accounts);
        
        // 🟢 Ajoutez cette ligne ici pour informer les utilisateurs que le compte a été sauvegardé avec succès
        logger.info("Account saved successfully");
        
        return "saved";
    } else {
        // 🟠 Ajoutez cette ligne ici pour avertir les utilisateurs que la sauvegarde a échoué car le client n'a pas été trouvé
        logger.warn("Failed to save account, customer not found: {}", id);
        
        // 🔴 Ajoutez cette ligne ici pour signaler une erreur critique : impossible de sauvegarder car le client n'existe pas
        logger.error("Critical error: unable to save account, customer ID not found: {}", id);
        
        return "failed, customer not found!";
    }
}
```

### Code couleur :
- 🟢 **Info** (niveau moins important) : Informer les utilisateurs d'une action réussie ou d'un processus normal, comme le début de la récupération des comptes.
- 🔵 **Debug** (niveau technique) : Fournir des informations pour les développeurs sur des détails techniques comme le nombre de comptes récupérés ou une tentative de sauvegarde.
- 🟠 **Warning** (niveau modéré) : Avertir d'un problème potentiel, comme l'absence d'un client.
- 🔴 **Error** (niveau critique) : Signaler une erreur grave qui doit être corrigée, comme l'impossibilité de sauvegarder un compte à cause d'une erreur critique.



# Résumé 
- Je vous propose une table qui indique quand les logs sont invoqués, les points de terminaison, les méthodes correspondantes et les logs appelés avec leurs codes couleur associés :

| **Point de terminaison**        | **Méthode**            | **Logs appelés**                                                                 | **Code couleur**                  |
|----------------------------------|------------------------|----------------------------------------------------------------------------------|-----------------------------------|
| `/accounts` (GET)                | `getAllAccounts()`     | `logger.info("Fetching all accounts");`                                           | 🟢 **Info** (début de la récupération des comptes) |
|                                  |                        | `logger.debug("Number of accounts fetched: {}", allAccounts.size());`             | 🔵 **Debug** (nombre de comptes récupérés) |
| `/accounts/save` (POST)          | `save(Accounts)`       | `logger.debug("Tentative de sauvegarde du compte : {}", accounts);`               | 🔵 **Debug** (tentative de sauvegarde d'un compte) |
|                                  |                        | `logger.info("Account saved successfully");`                                      | 🟢 **Info** (compte sauvegardé avec succès) |
|                                  |                        | `logger.warn("Failed to save account, customer not found: {}", id);`              | 🟠 **Warning** (client non trouvé) |
|                                  |                        | `logger.error("Critical error: unable to save account, customer ID not found: {}", id);` | 🔴 **Error** (erreur critique, sauvegarde échouée) |




# 3.3. Test de l'Implémentation Intermédiaire

Pour tester l'ajout de logging à différents niveaux, suivez ces étapes :

1. **Insertion d'un Compte avec un Client Valide** :
   - Utilisez l'endpoint POST `/newAccount` pour créer un compte avec un `customerId` valide.
   - Vérifiez que les logs INFO sont générés, indiquant que le compte a été sauvegardé avec succès.

2. **Insertion d'un Compte avec un Client Invalide** :
   - Utilisez l'endpoint POST `/newAccount` avec un `customerId` qui n'existe pas.
   - Vérifiez que les logs WARN sont générés, indiquant l'échec de la sauvegarde du compte.

3. **Récupération de Tous les Comptes** :
   - Utilisez l'endpoint GET `/accounts` pour récupérer la liste des comptes.
   - Vérifiez les logs INFO et DEBUG pour les messages correspondants à cette opération.

----
----
----

# PARTIE 4 - Pratique 3 et Implémentation 3 - Personnaliser les Logs (Avancée)
----


----
# Énoncé de l'Exercice : Configuration Avancée de Logging
----

**Objectif** : Configurer la gestion de logs personnalisée dans une application Spring Boot en séparant les logs selon leur niveau de sévérité.

**Instructions** :
1. **Configurer les Appenders** :
   - Créez un fichier `logback-spring.xml` et configurez trois appenders : un pour WARN, un pour ERROR, et un pour les autres niveaux de logs (INFO, DEBUG, TRACE).

2. **Configurer les Filtres de Niveau** :
   - Utilisez des `LevelFilter` pour vous assurer que seuls les logs correspondants aux niveaux sont écrits dans les fichiers respectifs.

3. **Configurer le Logger ROOT** :
   - Assurez-vous que le logger ROOT utilise les trois appenders configurés.

4. **Tester la Configuration** :
   - Écrivez des exemples de logs à différents niveaux et vérifiez si les logs sont correctement écrits dans les fichiers respectifs.

### Critères de Réussite :
- Les logs de niveau WARN apparaissent uniquement dans `app.warn.log`.
- Les logs de niveau ERROR apparaissent uniquement dans `app.error.log`.
- Les logs des autres niveaux apparaissent dans `app.general.log`.



----
# Correction : Configuration Avancée de Logback pour Séparation des Logs par Niveau de Sévérité :
----

1. **Créer un Fichier de Configuration Logback** :
   - Créez un fichier `logback-spring.xml` dans `src/main/resources`.
2. **Changez votre applications.properties en commentant les lignes de logging** :
   - J'ai commenté tous ce qui est en dessous de #Partie1 (qui fait référence à l'ancienne configuration de Logging).
#### ➡️➡️➡️ ☠️  🧐 Il faut garder uniquement le Niveau global de journalisation et le Niveau de journalisation pour un package spécifique

   ```properties             
            # Niveau global de journalisation
            logging.level.root=INFO
            # Niveau de journalisation pour un package spécifique
            logging.level.com.eazybytes=DEBUG   
   ```

 - Exemple :
   
   ```properties
            spring.datasource.driverClassName=org.postgresql.Driver
            spring.datasource.url=jdbc:postgresql://localhost:5432/microDemo1
            spring.datasource.username=hrgres
            spring.datasource.password=hrgres
            spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
            spring.jpa.hibernate.ddl-auto=update
            spring.jpa.show-sql=true
            server.port=8081
             
            # Niveau global de journalisation
            logging.level.root=INFO
            # Niveau de journalisation pour un package spécifique
            logging.level.com.eazybytes=DEBUG
            
            
            # *********************************
            # Partie 1
            # *********************************
            # logging.level.root=WARN
            # logging.level.com.eazybytes=DEBUG
            # chemin relatif à partir du pom.xml
            # logging.file.name=./logs/app.log 
            #logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n
            
            
            # *********************************
            # ERREURS
            # *********************************
            # logging.file.path=/logs - a causé une erreure
   ```
3. **Configurer les Appenders** :
   - Définissez des appenders distincts pour les niveaux WARN et ERROR.
   - Exemple :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <!-- Encoder pour formater les logs -->
    <encoder>
        <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>

    <!-- Appender pour les logs généraux (INFO et DEBUG) -->
    <appender name="GENERAL_LOG_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- Chemin relatif avec ./ pour spécifier le répertoire courant -->
        <file>./logs/app.general.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>./logs/app.general.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!-- Appender pour les logs WARN -->
    <appender name="WARN_LOG_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>./logs/app.warn.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>./logs/app.warn.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!-- Appender pour les logs ERROR -->
    <appender name="ERROR_LOG_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>./logs/app.error.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>./logs/app.error.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!-- Configuration du Root Logger -->
    <root level="INFO">
        <appender-ref ref="GENERAL_LOG_FILE" />
        <appender-ref ref="WARN_LOG_FILE" />
        <appender-ref ref="ERROR_LOG_FILE" />
    </root>

</configuration>
```




4. **Test de l'Implémentation**

- Après avoir mis à jour le fichier `logback-spring.xml`, redémarrez votre application pour appliquer la nouvelle configuration.
- Pour tester la séparation des logs par niveau de sévérité, suivez ces étapes :

4.1. **Génération de Logs WARN et ERROR** :
   - Utilisez l'endpoint POST `/newAccount` avec un `customerId` qui n'existe pas pour générer un log WARN.
   - Vérifiez que le log apparaît uniquement dans le fichier `app.warn.log`.
   - Vérifiez que le log ERROR apparaît uniquement dans le fichier `app.error.log`.

4.2. **Génération de Logs INFO et DEBUG** :
   - Utilisez les endpoints GET pour récupérer des données et vérifiez que les logs INFO et DEBUG apparaissent dans le fichier `app.general.log`.


# Conclusion: 
- Nous avons généré des logs à différents niveaux (DEBUG, INFO, WARN, ERROR) et nous avons vérifié qu'ils sont correctement répartis dans les fichiers configurés (`app.general.log`, `app.warn.log`, `app.error.log`).




---
---
---
---
# 01 - Annexe 01: signification de logging.pattern.console
----

Le format spécifié par `logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n` est une configuration utilisée dans les fichiers de propriétés ou de configuration pour déterminer comment les messages de log sont formatés lorsqu'ils sont affichés dans la console. Décomposons chaque partie de ce format pour comprendre en détail ce qu'elle signifie.

### 1. `%d{yyyy-MM-dd HH:mm:ss}`
- **%d** : Ceci est un spécificateur pour la date et l'heure du log. Il formate le timestamp du message de log.
- **{yyyy-MM-dd HH:mm:ss}** : Le format dans lequel la date et l'heure seront affichées.
  - `yyyy` : L'année sur quatre chiffres (ex : 2024).
  - `MM` : Le mois sur deux chiffres (01 pour janvier, 12 pour décembre).
  - `dd` : Le jour du mois sur deux chiffres.
  - `HH` : L'heure sur deux chiffres, au format 24 heures (00 à 23).
  - `mm` : Les minutes sur deux chiffres.
  - `ss` : Les secondes sur deux chiffres.
  
  **Exemple** : Si un message de log est généré le 30 août 2024 à 14:35:26, la sortie serait `2024-08-30 14:35:26`.

### 2. `- %logger{35}`
- **%logger** : Ceci est un spécificateur qui représente le nom du logger. En général, cela correspond au nom de la classe Java d'où le log a été généré.
- **{35}** : Ce nombre limite la longueur du nom du logger à 35 caractères. Si le nom du logger dépasse cette longueur, il sera tronqué au début pour ne garder que les 35 derniers caractères. Cela permet de rendre le log plus lisible en évitant que les noms de logger trop longs n'encombrent la sortie.
  
  **Exemple** : Si le nom du logger est `com.example.project.module.ClassName`, il sera affiché en entier si sa longueur est de 35 caractères ou moins. Sinon, seuls les 35 derniers caractères seront affichés.

### 3. `- %level`
- **%level** : Ceci affiche le niveau de log du message, comme `DEBUG`, `INFO`, `WARN`, `ERROR`, etc. Ce niveau indique la gravité ou la priorité du message.
  
  **Exemple** : Si le message de log est de niveau `INFO`, il sera affiché comme `INFO`.

### 4. `- %msg`
- **%msg** : Ceci affiche le message de log réel qui a été enregistré. C'est le contenu principal du log qui décrit l'événement ou l'action qui a eu lieu.
  
  **Exemple** : Si le message de log est `"Saving account: Accounts{accountNumber=1}"`, il sera affiché comme `Saving account: Accounts{accountNumber=1}`.

### 5. `%n`
- **%n** : Ceci représente un saut de ligne (newline). Cela garantit que chaque message de log est affiché sur une nouvelle ligne dans la console.
  
  **Exemple** : Après chaque log, le curseur passe à la ligne suivante, ce qui permet de séparer clairement les différents messages de log.

### Exemple global
Lorsque ce format est appliqué, voici à quoi pourrait ressembler un message de log dans la console :

```
2024-08-30 14:35:26 - com.example.project.module.ClassName - INFO - Saving account: Accounts{accountNumber=1}
```

### Conclusion
Ce format fournit une structure claire et lisible pour afficher les logs, en incluant des informations essentielles comme la date, le nom du logger, le niveau de log, et le message. Le fait de formater les logs de manière cohérente aide les développeurs à comprendre rapidement ce qui se passe dans l'application et à identifier les problèmes en un coup d'œil.
