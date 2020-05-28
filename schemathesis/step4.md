## Fix the tests
1. In order to fix the failing tests we need to stub out each of the endpoints that are declared in our OAS
2. Add the following to the TodosApiController:
    ```java

    @Override
    public ResponseEntity<Void> createTodo( Todo todo, Boolean completed) {
        return new ResponseEntity<>(HttpStatus.valueOf(200);

    }

    @Override
    public ResponseEntity<Void> deleteTodo(String todoId) {
        return new ResponseEntity<>(HttpStatus.valueOf(200);

    }

    @Override
    public ResponseEntity<List<Todo>> getTodos( Boolean completed) {

        return new ResponseEntity<>(HttpStatus.valueOf(200);

    }

    @Override
    public ResponseEntity<Void> updateTodo(String todoId, Todo todo) {
        return new ResponseEntity<>(HttpStatus.valueOf(200);

    }
    ```{{copy}}
3. Stop the running Todo API instance with `CTRL + C`
3. Start the service again to pick up the changes: `mvn spring-boot:run`{{execute}}
3. Rerun the tests: `schemathesis run todo.yaml --base-url http://localhost:8080`{{execute}}
4. By default Schemathesis only tests that the response code is less than 500, but there are more options for test cases.  
   Run `schemthesis run --help` to see more testing options, specifically the --checks option.
5. Rerun the tests using all available checks: `schemathesis run todo.yaml --checks all --base-url http://localhost:8080`{{execute}}
6. Update the TodosApiController methods to conform to the OAS:
   ```java
   
    @Override
    public ResponseEntity<Void> createTodo(@Valid Todo todo, @Valid Boolean completed) {
        return new ResponseEntity<>(HttpStatus.valueOf(201));
    }

    @Override
    public ResponseEntity<Void> deleteTodo(String todoId) {
        return new ResponseEntity<>(HttpStatus.valueOf(204));
    }

    @Override
    public ResponseEntity<List<Todo>> getTodos(@Valid Boolean completed) {
        return ResponseEntity.status(200).body(new ArrayList<Todo>() );
    }

    @Override
    public ResponseEntity<Void> updateTodo(String todoId, Todo todo) {
        return new ResponseEntity<>(HttpStatus.valueOf(202));
    }
    ```{{copy}}
7. Stop the running Todo API instance with `CTRL + C`
7. Start the service again to pick up the changes: `mvn spring-boot:run`{{execute}}
7. Run the tests one final time: `schemathesis run todo.yaml --checks all --base-url http://localhost:8080`{{execute}}
