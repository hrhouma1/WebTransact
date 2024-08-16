
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
