
```plaintext
+------------+           +------------+
|            |           |            |
|   Client   |1 -------->|    Card    |
|            |           |            |
+------------+           +------------+
     |                         |
     |                         |
     +-- client_id (PK)         +-- card_id (PK)
     |                         |
     +-- name                   +-- card_number
     |                         |
     +-- email                  +-- expiry_date
     |                         |
     +-- mobile_number          +-- client_id (FK)
     |                         |
     +-- address                +-- card_type
     |                         |
+------------+           +------------+
```

### Légende :
- `Client`: Table représentant les clients.
- `Card`: Table représentant les cartes.
- `1 -------->` : Représente une relation un-à-plusieurs (1 client peut avoir plusieurs cartes).
- `(PK)` : Clé primaire.
- `(FK)` : Clé étrangère reliant la `Card` à un `Client`.

### Explications :
- Chaque `Client` peut avoir plusieurs `Cards` associées.
- La clé étrangère `client_id` dans la table `Card` référence la clé primaire `client_id` dans la table `Client`.

















```ssh

<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <include resource="org/springframework/boot/logging/logback/base.xml"/>
    
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.general.log</file>
        <encoder>
            <pattern>%date %level [%thread] %logger{10} [%file:%line] %msg%n</pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.general.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
    </appender>

    <appender name="WARN_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.warn.log</file>
        <encoder>
            <pattern>%date %level [%thread] %logger{10} [%file:%line] %msg%n</pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.warn.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <appender name="ERROR_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.error.log</file>
        <encoder>
            <pattern>%date %level [%thread] %logger{10} [%file:%line] %msg%n</pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>C:/Users/YourUsername/Desktop/accounts-v1/logs/app.error.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <root level="INFO">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
        <appender-ref ref="WARN_FILE" />
        <appender-ref ref="ERROR_FILE" />
    </root>

    <logger name="com.eazybytes" level="DEBUG" additivity="false">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
        <appender-ref ref="WARN_FILE" />
        <appender-ref ref="ERROR_FILE" />
    </logger>
</configuration>

```


```ssh
logging.level.root=WARN
logging.level.com.eazybytes=DEBUG
logging.file.name=C:/Users/YourUsername/Desktop/accounts-v1/logs/app.log
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %logger{35} - %level - %msg%n

```
