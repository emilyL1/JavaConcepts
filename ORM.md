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
- JPA vs Hibernate
    - The Java Persistence API (JPA) is a specification that defines how to persist data in Java applications. It declares a way for JavaEE applications to implement ORM to any relational databases.
    - Hibernate is a standard implementation of the JPA specification

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
- EntityManager
- Query
- Criteria API
- Cascade
- Fetch/Load Type

### Hibernate
- Session
- Cache

