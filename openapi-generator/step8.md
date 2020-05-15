
- Create a `src/main/java` source folder
  - This is the folder we will be putting all the code we plan on modifying
- Move `TodoApiController.java` from the `src/main/gen` folder to the same package inside the `src/main/java` folder
- Stub the getTodo by adding the following method:
     ```java
     @Override
     public ResponseEntity<Todo> getTodo(String todoId) {
         Todo response = new Todo();
         response.setName("Stubbed Todo Item");
         response.setDescription("Stubbed Todo Description");
         response.setCompleted(false);
         response.setDate(OffsetDateTime.now().plusDays(1));
         return ResponseEntity.ok(response);
     }
     ``` {{copy}}
 - Also add the following imports:
     ```java
     import com.redhat.todo.model.Todo;
     import java.time.OffsetDateTime;
     import org.springframework.http.ResponseEntity;
     ```{{copy}}
     
<sub>Note: we are returning a `200` response code. This is complient with our OAS specification. Currently we don't have any validation on which response code we are returning but it is best practice to follow what is specified by your OpenAPI Document. And in the future we will be looking at *Schemathesis* which will run test to validate that all expected response codes are returned</sub>
- Prevent the regeneration of the `TodoApisController.java`
  - In order to prevent files that you add to your `src/main/java` from being recreated in `src/main/gen` they need to be added to your `.openapi-generate-ignore` file
  - Add the following lines to prevent any 'Controller.java' files from being added, as well as preventing us from overriding our `pom.xml`
      ```regex
      **/*Controller.java
      pom.xml
      ```{{copy}}
      
- Validate Endpoint
  - Run `mvn spring-boot:run`{{execute}}
  - Navigate to the Swagger UI tab
  - Validate `GET /todos/{todoId}` returns 200 stubbed data 
- Stub out other endpoints (optional)
  - Remember response codes should match your OAS document
