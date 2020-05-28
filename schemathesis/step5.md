1. By default Schemathesis only tests that the response code is less than 500, but there are more options for test cases.  
   Run `schemthesis run --help`{{execute}} to see more testing options, specifically the `--checks` option.
2. Rerun the tests using all available checks: `schemathesis run todo.yaml --checks all --base-url http://localhost:8080`{{execute}}
3. Update the TodosApiController methods to conform to the OAS:
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
4. Stop the running Todo API instance with `CTRL + C`
4. Start the service again to pick up the changes: `mvn spring-boot:run`{{execute}}
4. Run the tests one final time: `schemathesis run todo.yaml --checks all --base-url http://localhost:8080`{{execute}}
