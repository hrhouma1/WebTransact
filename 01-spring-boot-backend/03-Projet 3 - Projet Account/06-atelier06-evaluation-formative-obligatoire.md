### 1. `Accounts.java`
```java
package com.eazybytes.accounts.model;

import java.time.LocalDate;
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.Column;
import jakarta.persistence.Id;

import lombok.Data;

@Entity
@Table(name = "Accounts")
@Data
public class Accounts {

    @Id
    @Column(name = "account_number")
    private long accountNumber;

    @Column(name = "customer_id")
    private int customerId;

    @Column(name = "account_type")
    private String accountType;

    @Column(name = "branch_address")
    private String branchAddress;

    @Column(name = "create_dt")
    private LocalDate createDt;

}
```

### 2. `Customer.java`
```java
package com.eazybytes.accounts.model;

import java.time.LocalDate;

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
}
```

### 3. `AccountsController.java`
```java
package com.eazybytes.accounts.controller;

import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.service.AccountsService;
import io.swagger.v3.oas.annotations.Operation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
public class AccountsController {

    @Autowired
    private AccountsService accountsService;

    // Anciennes Méthodes

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

    @Operation(summary = "Update an account by ID")
    @PutMapping("/update/{id}")
    public String updateAccount(@PathVariable("id") Long id, @RequestBody Accounts updateAccounts) {
        return accountsService.updateAccount(id, updateAccounts);
    }

    @Operation(summary = "Delete an account by ID")
    @DeleteMapping("/deleteAccount/{id}")
    public String deleteAccount(@PathVariable("id") Long id) {
        return accountsService.deleteAccount(id);
    }

    // Nouvelles Méthodes

    @Operation(summary = "Create multiple accounts")
    @PostMapping("/newAccounts")
    public List<String> newAccounts(@RequestBody List<Accounts> accountsList) {
        return accountsService.saveAll(accountsList);
    }

    @Operation(summary = "Delete all accounts")
    @DeleteMapping("/deleteAllAccounts")
    public String deleteAllAccounts() {
        return accountsService.deleteAllAccounts();
    }

    @Operation(summary = "Delete multiple accounts by IDs")
    @DeleteMapping("/deleteAccounts")
    public String deleteAccounts(@RequestBody List<Long> accountIds) {
        return accountsService.deleteAllByIds(accountIds);
    }

    @Operation(summary = "Update multiple accounts")
    @PutMapping("/updateAccounts")
    public String updateAccounts(@RequestBody List<Accounts> accountsList) {
        return accountsService.updateAccounts(accountsList);
    }

    @Operation(summary = "Find accounts by IDs")
    @PostMapping("/findAccounts")
    public List<Accounts> findAccounts(@RequestBody List<Long> accountIds) {
        return accountsService.findAllByIds(accountIds);
    }
}
```

### 4. `CustomerController.java`
```java
package com.eazybytes.accounts.controller;

import com.eazybytes.accounts.model.Customer;
import com.eazybytes.accounts.service.CustomerService;
import io.swagger.v3.oas.annotations.Operation;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDate;
import java.util.List;

@RestController
public class CustomersController {

    @Autowired
    CustomerService customerService;

    @Operation(summary = "Get all customers")
    @GetMapping("/customers")
    public List<Customer> getAllCustomers(){
        return customerService.getAllCustomer();
    }

    @Operation(summary = "Get customer by ID")
    @GetMapping("/customer/{id}")
    public Customer getCustomerById(@PathVariable int id){
        return customerService.getCustomerById(id);
    }

    @Operation(summary = "Create new customer")
    @PostMapping("/newCustomer")
    public void newCustomer(@RequestBody Customer newCustomer){
        newCustomer.setCreateDt(LocalDate.now());
        customerService.save(newCustomer);
    }

    @Operation(summary = "Update customer by ID")
    @PutMapping("/updateCustomer/{id}")
    public String updateCustomer(@PathVariable("id") int id, @RequestBody Customer updateCustomer){
        return customerService.update(id, updateCustomer);
    }

    @Operation(summary = "Delete customer by ID")
    @DeleteMapping("/deleteCustomer/{id}")
    public String deleteCustomer(@PathVariable("id") int id){
        return customerService.deleteCustomer(id);
    }

    @Operation(summary = "Check if customer exists by ID")
    @GetMapping("/customerExist/{id}")
    public boolean customerExist(@PathVariable("id") int id){
        return customerService.customerExist(id);
    }
}
```

### 5. `AccountsRepository.java`
```java
package com.eazybytes.accounts.repository;

import com.eazybytes.accounts.model.Accounts;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

import java.time.LocalDate;
import java.util.List;

@Repository
public interface AccountsRepository extends CrudRepository<Accounts, Long> {

    // Anciennes Méthodes

    List<Accounts> findByCreateDtAfter(LocalDate date);

    @Query("SELECT a FROM Accounts a WHERE a.accountNumber BETWEEN :startId AND :endId")
    List<Accounts> findAccountsInRange(long startId, long endId);

    @Query("SELECT COUNT(a) FROM Accounts a WHERE a.accountType = :accountType")
    long countByAccountType(String accountType);

    // Nouvelles Méthodes

    List<Accounts> findAllByAccountNumberIn(List<Long> ids);

    void deleteAllByAccountNumberIn(List<Long> accountNumbers);

    List<Accounts> findByCustomerId(int customerId);
}
```

### 6. `CustomerRepository.java`
```java
package com.eazybytes.accounts.repository;

import com.eazybytes.accounts.model.Customer;
import org.springframework.data.jpa.repository.JpaRepository;

public interface CustomerRepository extends JpaRepository<Customer, Integer> {
}
```

### 7. `AccountsService.java`
```java
package com.eazybytes.accounts.service;

import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.repository.AccountsRepository;
import com.eazybytes.accounts.repository.CustomerRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;

@Service
public class AccountsService {

    @Autowired
    AccountsRepository accountsRepository;

    @Autowired
    CustomerRepository customerRepository;

    // Anciennes Méthodes

    public List<Accounts> getAllAccounts() {
        List<Accounts> allAccounts = new ArrayList<>();
        accountsRepository.findAll().forEach(allAccounts::add);
        return allAccounts;
    }

    public Accounts getAccountsById(long id) {
        return accountsRepository.findById(id).orElse(null);
    }

    public String save(Accounts accounts) {
        int id = accounts.getCustomerId();
        if (customerRepository.existsById(id)) {
            accounts.setCreateDt(LocalDate.now());
            accountsRepository.save(accounts);
            return "saved";
        } else {
            return "failed, customer not found!";
        }
    }

    public String deleteAccount(Long id) {
        accountsRepository.deleteById(id);
        return "deleted!";
    }

    public String updateAccount(long id, Accounts updateAccounts) {
        Accounts accountsFind = accountsRepository.findById(id).orElse(null);
        if (accountsFind != null) {
            updateAccounts.setAccountNumber(id);
            updateAccounts.setCreateDt(LocalDate.now());
            accountsRepository.save(updateAccounts);
            return "update successful!";
        } else {
            return "account not found!";
        }
    }

    // Nouvelles Méthodes

    @Transactional
    public List<String> saveAll(List<Accounts> accountsList) {
        List<String> responseList = new ArrayList<>();
        for (Accounts account : accountsList) {
            try {
                accountsRepository.save(account);
                responseList.add("Compte enregistré avec succès : " + account.getAccountNumber());
            } catch (Exception e) {
                responseList.add("Échec d'enregistrement pour le compte : " + account.getAccountNumber() + " - Erreur : " + e.getMessage());
            }
        }
        return responseList;
    }

    @Transactional
    public String deleteAllAccounts() {
        try {
            accountsRepository.deleteAll();
            return "Tous les comptes ont été supprimés avec succès";
        } catch (Exception e) {
            return "Erreur lors de la suppression des comptes : " + e.getMessage();
        }
    }

    @Transactional
    public String deleteAllByIds(List<Long> accountIds) {
        try {
            accountsRepository.deleteAllByAccountNumberIn(accountIds);
            return "Comptes supprimés avec succès";
        } catch (Exception e) {
            return "Erreur lors de la suppression des comptes : " + e.getMessage();
        }
    }

    @Transactional
    public String updateAccounts(List<Accounts> accountsList) {
        try {
            accountsList.forEach(account -> accountsRepository.save(account));
            return "Comptes mis à jour avec succès";
        } catch (Exception e) {
            return "Erreur lors de la mise à jour des comptes : " + e.getMessage();
        }
    }

    public List<Accounts> findAllByIds(List<Long> accountIds) {
        return (List<Accounts>) accountsRepository.findAllById(accountIds);
    }
}

```

### 8. `CustomerService.java`
```java
package com.eazybytes.accounts.service;

import com.eazybytes.accounts.model.Accounts;
import com.eazybytes.accounts.model.Customer;
import com.eazybytes.accounts.repository.AccountsRepository;
import com.eazybytes.accounts.repository.CustomerRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;

@Service
public class CustomerService {

    @Autowired
    CustomerRepository customerRepository;

    @Autowired
    AccountsRepository accountsRepository;

    public List<Customer> getAllCustomer() {
        List<Customer> customers = new ArrayList<>();
        customerRepository.findAll().forEach(customers::add);
        return customers;
    }

    public Customer getCustomerById(int id) {
        return customerRepository.findById(id).orElse(null);
    }

    public void save(Customer customer) {
        customer.setCreateDt(LocalDate.now());
        customerRepository.save(customer);
    }

    public String update(int id, Customer updateCustomer) {
        Customer customerFind = customerRepository.findById(id).orElse(null);
        if (customerFind != null) {
            updateCustomer.setCustomerId(id);
            updateCustomer.setCreateDt(LocalDate.now());
            customerRepository.save(updateCustomer);
            return "update successful!";
        } else {
            return "customer not found";
        }
    }

    public String deleteCustomer(int id) {
        List<Accounts> accounts = accountsRepository.findByCustomerId(id);
        if (!accounts.isEmpty()) {
            return "failed";
        } else {
            customerRepository.deleteById(id);
            return "Ok";
        }
    }

    public boolean customerExist(int id) {
        return customerRepository.existsById(id);
    }
}
```




### 8. `pom.xml`

```xml

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.0.6</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.eazybytes</groupId>
	<artifactId>accounts</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>accounts</name>
	<description>the microservice accounts</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.postgresql</groupId>
			<artifactId>postgresql</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springdoc</groupId>
			<artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
			<version>2.1.0</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.hibernate.validator/hibernate-validator -->
		<dependency>
			<groupId>org.hibernate.validator</groupId>
			<artifactId>hibernate-validator</artifactId>
			<version>8.0.0.Final</version>
		</dependency>

		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<excludes>
						<exclude>
							<groupId>org.projectlombok</groupId>
							<artifactId>lombok</artifactId>
						</exclude>
					</excludes>
				</configuration>
			</plugin>

			<!-- Plugin pour générer la Javadoc -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-javadoc-plugin</artifactId>
				<version>3.3.1</version>
				<executions>
					<execution>
						<goals>
							<goal>javadoc</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<author>true</author>
					<version>true</version>
					<windowTitle>Documentation API du Projet Accounts</windowTitle>
					<doctitle>API Documentation - Accounts Project</doctitle>
				</configuration>
			</plugin>

		</plugins>
	</build>

</project>
```
