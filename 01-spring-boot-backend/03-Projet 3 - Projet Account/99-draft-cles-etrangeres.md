# Définir la relation `OneToMany` et `ManyToOne` entre les classes `Customer` et `Accounts`. 

# Code mis-à-jour

### 1. `Accounts.java`
```java
package com.eazybytes.accounts.model;

import java.time.LocalDate;
import jakarta.persistence.*;

import lombok.Data;

@Entity
@Table(name = "Accounts")
@Data
public class Accounts {

    @Id
    @Column(name = "account_number")
    private long accountNumber;

    @Column(name = "account_type")
    private String accountType;

    @Column(name = "branch_address")
    private String branchAddress;

    @Column(name = "create_dt")
    private LocalDate createDt;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "customer_id", nullable = false)
    private Customer customer;
}
```

### 2. `Customer.java`
```java
package com.eazybytes.accounts.model;

import java.time.LocalDate;
import java.util.List;
import jakarta.persistence.*;

import lombok.Data;

@Entity
@Table(name = "Customer")
@Data
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "customer_id")
    private int customerId;

    private String name;
    private String email;

    @Column(name = "mobile_number")
    private String mobileNumber;

    @Column(name = "create_dt")
    private LocalDate createDt;

    @OneToMany(mappedBy = "customer", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Accounts> accounts;
}
```

### Explications :

- **Customer.java** : La classe `Customer` contient une liste de comptes (`List<Accounts> accounts`) avec l'annotation `@OneToMany`. La relation est mappée par l'attribut `customer` dans la classe `Accounts`.

- **Accounts.java** : La classe `Accounts` contient une référence à un `Customer` avec l'annotation `@ManyToOne`. La clé étrangère `customer_id` est utilisée pour lier les comptes à un client spécifique.

Avec ces modifications, la relation `OneToMany` entre `Customer` et `Accounts` est maintenant correctement définie. Vous pouvez maintenant utiliser ces entités dans vos contrôleurs et services avec la relation appropriée en place.

--------

#  Diagramme représentant la relation entre les classes `Customer` et `Accounts` :

```
+----------------+         1     +----------------+
|   Customer     |----------------|    Accounts    |
|----------------|   (OneToMany)  |----------------|
| - customerId   |                | - accountNumber|
| - name         |                | - accountType  |
| - email        |                | - branchAddress|
| - mobileNumber |                | - createDt     |
| - createDt     |                |----------------|
|----------------|                | - customerId   |
| + accounts     |<---------------|                |
| (List<Accounts>)|  (ManyToOne)   |                |
+----------------+                +----------------+
```

### Explications du diagramme :

- **Customer** est lié à **Accounts** par une relation OneToMany (1 -> \*).
- **Accounts** est lié à **Customer** par une relation ManyToOne (\* -> 1).
- L'attribut `customerId` dans **Accounts** est une clé étrangère qui fait référence à l'entité **Customer**.
- L'attribut `accounts` dans **Customer** représente la liste de comptes associés à ce client.

Ce diagramme montre clairement les relations et les dépendances entre les deux classes.








### `customers-controller`
| HTTP Method | Endpoint                | Description                       |
|-------------|-------------------------|-----------------------------------|
| PUT         | `/updateCustomer/{id}`   | Update customer by ID             |
| POST        | `/newCustomer`           | Create a new customer             |
| GET         | `/customers`             | Get all customers                 |
| GET         | `/customerExist/{id}`    | Check if a customer exists by ID  |
| GET         | `/customer/{id}`         | Get a customer by ID              |
| DELETE      | `/deleteCustomer/{id}`   | Delete customer by ID             |

### `accounts-controller`
| HTTP Method | Endpoint                | Description                                |
|-------------|-------------------------|--------------------------------------------|
| PUT         | `/updateAccounts`        | Update multiple accounts                   |
| PUT         | `/update/{id}`           | Update an account by ID                    |
| POST        | `/newAccounts`           | Create multiple accounts                   |
| POST        | `/newAccount`            | Create a new account                       |
| POST        | `/findAccounts`          | Find accounts by IDs                       |
| GET         | `/myAccount/{id}`        | Get an account by ID                       |
| GET         | `/accounts`              | Get all accounts                           |
| DELETE      | `/deleteAllAccounts`     | Delete all accounts                        |
| DELETE      | `/deleteAccounts`        | Delete multiple accounts by IDs            |
| DELETE      | `/deleteAccount/{id}`    | Delete an account by ID                    |


