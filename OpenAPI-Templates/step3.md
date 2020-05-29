## Instructions


1a. Setup JPA <sub>Optional: If you want to skip setup JPA/Controller setup, go to step 1b</sub>
  - Add Spring Data JPA and h2 database dependencies to your pom.xml:
    ```xml
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-data-jpa</artifactId>
          <version>2.1.4.RELEASE</version>
      </dependency>
      <dependency>
          <groupId>com.h2database</groupId>
          <artifactId>h2</artifactId>
          <scope>runtime</scope>
          <version>1.4.199</version>
      </dependency>
    ```{{copy}}
  - Setup up h2 in-memory db by updating `application.properties` with the following:
    ```properties
    #InMemory DB Connection
    spring.datasource.url=jdbc:h2:mem:tododb
    spring.datasource.driverClassName=org.h2.Driver
    spring.datasource.username=sa
    spring.datasource.password=password
    spring.jpa.database-platform=org.hibernate.dialect.H2Dialect

    #H2 Console
    spring.h2.console.enabled=true
    spring.h2.console.path=/h2-console
    spring.h2.console.settings.web-allow-others=false
    ```{{copy}}
  - Create the Todo repository file in `src/main/java/com/redhat/todo/repository`
    ```java
      package com.redhat.todo.repository;

      import java.util.List;

      import com.redhat.todo.model.Todo;

      import org.springframework.data.jpa.repository.JpaRepository;
      import org.springframework.stereotype.Repository;

      @Repository
      public interface TodoRepository extends JpaRepository<Todo, Integer>{

          public List<Todo> getByCompleted(Boolean completed);

      }
    ```{{copy}}
    <sub>Spring data is automatically able to create the query based on method name, [more info](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation)</sub>
  - Add `repository` folder to scanned directories
    - Navigate to `OpenAPI2SpringBoot`
    - Add "com.redhat.todo.repository" to `@ComponentScan`'s basePackages
      ```java
      @ComponentScan(basePackages = {"com.redhat.todo", "com.redhat.todo.api" , "com.redhat.todo.config"})
      ```{{copy}}
  - Stub out all of the operation methods for TodoApiController.java example below.
    ```java
      @Override
      public ResponseEntity<Todo> getTodo(@ApiParam(value = "A unique identifier for a `todo`.",required=true) @PathVariable("todoId") Integer todoId) {
          return ResponseEntity.ok(todoRepository.findById(todoId)
              .orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND)));
      }
    ```{{copy}}
    
   <sub><span style="color:red">Important:</span> Paramter level annotations must be copied over to the stubbed method in Java in order for your paths to function correctly</sub>
  - Preload data by adding a `data.sql` file to the `resources` directory with the following:
    ```sql
    DROP TABLE IF EXISTS todo;

    CREATE TABLE todo (
      id INT IDENTITY NOT NULL  PRIMARY KEY,
      name VARCHAR(250) NOT NULL,
      description VARCHAR(250) NOT NULL,
      date DATETIME NOT NULL,
      completed Boolean DEFAULT false
    );

    INSERT INTO todo (name, description, date, completed) VALUES
      ('Apicur.io', 'Create my first OpenAPI Spec', now() - INTERVAL 2 DAY, true),
      ('OpenApi Generator', 'Generate my OpenAPI Springboot App', now() - INTERVAL 1 DAY, true),
      ('OAG Templating', 'Add DB persistance to my Springboot App', now() + INTERVAL 20 MINUTE, false)
    ```{{copy}}
