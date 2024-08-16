### Classe `Customer`

```java
package com.exemple.cards.model;

import jakarta.persistence.*;
import lombok.*;

import java.util.List;

@Entity
@Table(name = "Customer")
@Data
public class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "customer_id")
    private int customerId;

    @Column(name = "name")
    private String name;

    @Column(name = "email")
    private String email;

    @Column(name = "mobile_number")
    private String mobileNumber;

    @Column(name = "address")
    private String address;

    @OneToMany(mappedBy = "customerId", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Cards> cards;
}
```

### Classe `Cards`

```java
package com.exemple.cards.model;

import java.time.LocalDate;

import jakarta.persistence.*;

import lombok.*;

@Entity
@Table(name = "Cards")
@Data
public class Cards {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "card_id")
    private int cardId;

    @ManyToOne
    @JoinColumn(name = "customer_id", nullable = false)
    private Customer customer;

    @Column(name = "card_number")
    private String cardNumber;

    @Column(name = "card_type")
    private String cardType;

    @Column(name = "total_limit")
    private int totalLimit;

    @Column(name = "amount_used")
    private int amountUsed;

    @Column(name = "available_amount")
    private int availableAmount;

    @Column(name = "create_dt")
    private LocalDate createDt;
}
```

### Explications  :

- **Customer** : La classe `Customer` contient les informations sur les clients, et elle a une relation un-à-plusieurs avec la classe `Cards` via la liste `cards`.

- **Cards** : La classe `Cards` contient les informations sur les cartes et possède une relation plusieurs-à-un avec la classe `Customer`. Le champ `customer` est utilisé pour lier chaque carte à un client spécifique.

