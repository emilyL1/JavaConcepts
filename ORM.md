# ORM

### JDBC
- middleware to manipulate database
- Driver, Connection, Statement, PrepareStatement, ResultSet
- jdbc handle commit automatically | conn.setAutoCommit(false)
- statement
    - Useful when you are using **static** SQL statements at runtime. 
    - `stmt = conn.createStatement( );`
    - `ResultSet executeQuery (String SQL)`
- PreparedStatement
    - gives you the flexibility of supplying arguments dynamically.
    - `String SQL = "Update Employees SET age = ? WHERE id = ?";
    PreparedStatement stmt = conn.prepareStatement(SQL);
         stmt.setInt(1, 35); ` 
- CallableStatement  
    - execute a call to a database stored procedure
    - `String SQL = "{call getEmpName (?, ?)}";
   cstmt = conn.prepareCall (SQL);` 
    - `// Because second parameter is OUT so register it
         stmt.registerOutParameter(2, java.sql.Types.VARCHAR);` 
 -  [Batch Processing](baeldung.com/jdbc-batch-processing)
     -  all statement into 1 batch         
### ORM
- Object-Relational Mapping (ORM) is a technique that lets you query and manipulate data from a database using an object-oriented paradigm. 

### JDBC vs ORM
- jdbc advantage: usually have clean SQL processing, good performance even with large data.
- jdbc disadvatage
    - become complex if it is used in large projects. We get a large programming overhead, no encapsulation. 
    - Implementation of the MVC concept becomes harder. 
    - One more disadvantage of JDBC is that SQL queries are DBMS specific. 
- ORM advatage:
    - it is designed to let the business code access objects rather than DB tables. 
    - we hide details of SQL queries from object-oriented logic
    -  With ORM we get all the transaction management and automatic key generation.
    -  ORMs improve portability because generate database-specific SQL for you
    -  entities are more based on business concepts rather than a database structure.
- ORM disadvatages:
    - They have slow performance in case of large batch updates. 

### JPA
- The Java Persistence API (JPA) is a <u>**specification**</u> that defines how to persist data in Java applications. It declares a way for JavaEE applications to implement ORM to any relational databases.
- EntityManager
    - Entity
        - An entity represents a table stored in a database. define an entity(`@Entity`) so that JPA is aware of it
        - We must also ensure that the entity has a no-arg constructor and a primary key(`@Id`)
            - We can generate the identifiers in different ways, which are specified by the `@GeneratedValue` annotation.
            - the value can be AUTO, TABLE, SEQUENCE, or IDENTITY:
        - the name of the table in the database and the name of the entity won't be the same.(`@Table(name="STUDENT")`)
        - make a field non-persistent. We can use the `@Transient annotation`
        - We can use the `@Enumerated` annotation to specify whether the enum should be persisted by name or by ordinal (default):
    - **persistence context** sits between client code and data store. It's a staging area where persistent data is converted to entities, ready to be read and altered by client code. 
        - an implementation of **the Unit of Work** pattern.
            - A Unit of Work keeps keeps track of all loaded data, tracks changes of that data, and is responsible to eventually synchronize any changes back to the database at the end of the business transaction.
        - JPA EntityManager and Hibernate's Session are an implementation of the persistence context concept.
    
- Query
- Criteria API
- Cascade
    - By default, JPA doesn't give any cascade. It needs to be manually turn on : example: @OneToMany(Cascade=Persist);
- Fetch/Load Type
    - eager loading: all associate data will be loaded at once
    - lazy loading: load data when needed

### Hibernate
- Hibernate is a standard **<u>implementation</u>** of the JPA specification
- Session
    - start our unit of work by obtaining a Session(to encapsulate the business transaction of our unit of work)
        - `Session session = sessionFactory.openSession();`
        - ```java
            Transaction transaction = session.getTransaction();
            transaction.begin();
            
            FootballPlayer gigiBuffon = players.stream()
              .filter(p -> p.getId() == 3)
              .findFirst()
              .get();
            
            gigiBuffon.setName("Gianluigi Buffon");
            transaction.commit();
          ```
    - Notice that we didn't need to call any method to notify Session that we changed something in our entity – since it's a managed entity, all changes are propagated to the database automatically. 
- Cache
    - First level is session level
    - Second level is sessionFactory level

### Spring Data JPA
- <u>Spring Data JPA</u> is not a JPA provider. It is a library/framework that <u>adds an extra layer of abstraction</u> on the top of our JPA provider (like Hibernate).

