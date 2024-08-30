# ANNEXE 1 - Journalisation : 

- Comparons les différents niveaux de journalisation pour la **Journalisation Globale (root)** en utilisant une arborescence. 
- Cette comparaison vous aidera à comprendre ce que chaque niveau capture ou ignore.


# **Fichier de configuration** : 


```properties
     # Niveau de journalisation global
     logging.level.root=INFO
     # Configuration spécifique à une classe ou un package
     logging.level.com.example=DEBUG
     # Emplacement du fichier de journal
     logging.file=myapp.log
```
# La signification de logging.level.root=INFO 

### Journalisation Globale (root)
#### 1. Niveau `INFO`
```
Journalisation Globale (root)
├── Niveau INFO
│   ├── Capture les événements importants
│   │   ├── INFO (informations utiles)
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ignore les événements moins importants
│       └── DEBUG (détails supplémentaires)
```
- **INFO** est le niveau où l'on commence à capturer ce qui est important, mais on ignore les détails superflus (DEBUG).
  
#### 2. Niveau `WARN`
```
Journalisation Globale (root)
├── Niveau WARN
│   ├── Capture les avertissements et les erreurs graves
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ignore les événements moins graves
│       ├── INFO (informations utiles)
│       └── DEBUG (détails supplémentaires)
```
- **WARN** capture seulement ce qui pourrait poser problème (avertissements) ou ce qui est déjà un problème (erreurs critiques). Les informations utiles et les détails mineurs sont ignorés.

#### 3. Niveau `ERROR`
```
Journalisation Globale (root)
├── Niveau ERROR
│   ├── Capture uniquement les erreurs critiques
│   │   └── ERROR (erreurs graves qui nécessitent une attention immédiate)
│   └── Ignore tout le reste
│       ├── WARN (avertissements)
│       ├── INFO (informations utiles)
│       └── DEBUG (détails supplémentaires)
```
- **ERROR** est très strict. Il n'enregistre que les erreurs graves, tout le reste est ignoré.

#### 4. Niveau `DEBUG`
```
Journalisation Globale (root)
├── Niveau DEBUG
│   ├── Capture tout, même les détails mineurs
│   │   ├── DEBUG (détails supplémentaires)
│   │   ├── INFO (informations utiles)
│   │   ├── WARN (avertissements)
│   │   └── ERROR (erreurs critiques)
│   └── Ne laisse rien passer
```
- **DEBUG** capture absolument tout, depuis les petites informations jusqu'aux erreurs critiques.

### Résumé Comparatif :

- **DEBUG** : Capture tout, même les détails les plus petits.
- **INFO** : Capture les informations utiles et tous les événements plus graves (WARN et ERROR).
- **WARN** : Capture uniquement les avertissements et les erreurs graves.
- **ERROR** : Capture uniquement les erreurs les plus critiques.

Chaque niveau de journalisation est de plus en plus restrictif, en capturant moins d'événements à mesure que l'on passe de DEBUG à ERROR.
