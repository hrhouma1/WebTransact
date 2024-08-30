# ANNEXE 2 - Journalisation Spécifique (com.example)
- Comme pour la journalisation globale, chaque niveau de journalisation pour `com.example` est de plus en plus restrictif, en capturant moins d'événements à mesure que l'on passe de DEBUG à ERROR.

# **Fichier de configuration** : 

```properties
     # Niveau de journalisation global
     logging.level.root=INFO
     # Configuration spécifique à une classe ou un package
     logging.level.com.example=DEBUG
     # Emplacement du fichier de journal
     logging.file=myapp.log
```

# La signification de logging.level.com.example=DEBUG


#### 1. Niveau `DEBUG`
```
Journalisation Spécifique (com.example)
├── Niveau DEBUG
│   ├── Capture tout, même les détails mineurs
│   │   ├── DEBUG (détails supplémentaires)
│   │   ├── INFO (informations utiles)
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ne laisse rien passer
```
- **DEBUG** capture absolument tout ce qui se passe dans `com.example`, depuis les petits détails (DEBUG) jusqu'aux erreurs graves (ERROR).

#### 2. Niveau `INFO`
```
Journalisation Spécifique (com.example)
├── Niveau INFO
│   ├── Capture les événements importants
│   │   ├── INFO (informations utiles)
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ignore les événements moins importants
│       └── DEBUG (détails supplémentaires)
```
- **INFO** capture les informations utiles et les événements plus graves dans `com.example`, mais ignore les détails superflus (DEBUG).

#### 3. Niveau `WARN`
```
Journalisation Spécifique (com.example)
├── Niveau WARN
│   ├── Capture les avertissements et les erreurs graves
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ignore les événements moins graves
│       ├── INFO (informations utiles)
│       └── DEBUG (détails supplémentaires)
```
- **WARN** capture seulement ce qui pourrait poser problème (WARN) ou ce qui est déjà un problème (ERROR) dans `com.example`. Les informations utiles (INFO) et les détails mineurs (DEBUG) sont ignorés.

#### 4. Niveau `ERROR`
```
Journalisation Spécifique (com.example)
├── Niveau ERROR
│   ├── Capture uniquement les erreurs critiques
│   │   └── ERROR (erreurs graves qui nécessitent une attention immédiate)
│   └── Ignore tout le reste
│       ├── WARN (avertissements)
│       ├── INFO (informations utiles)
│       └── DEBUG (détails supplémentaires)
```
- **ERROR** est très strict. Il n'enregistre que les erreurs graves (ERROR) dans `com.example`, tout le reste est ignoré.

### Résumé Comparatif pour `com.example` :

- **DEBUG** : Capture tout dans `com.example`, depuis les détails les plus petits jusqu'aux erreurs graves.
- **INFO** : Capture les informations utiles et tous les événements plus graves dans `com.example`.
- **WARN** : Capture uniquement les avertissements et les erreurs graves dans `com.example`.
- **ERROR** : Capture uniquement les erreurs les plus critiques dans `com.example`.

