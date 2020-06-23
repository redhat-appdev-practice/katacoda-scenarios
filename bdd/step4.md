## Test a New Behavior

1. To test a new behavior, the first step will be to add the new scenario to our todo.feature file:
```gherkin
  Scenario: A Todo can be deleted using it's ID
    Given a todo object exists with an id of 1
    When I delete the todo object with an id of 1
    And I get a todo object with an id of 1
    Then I should get a response of 404
```{{copy}}

2. Rerun the tests `mvn clean test`
    - we expect this to fail
    - the output from the test command will include code snippets to implement missing steps
    
3. Implement the steps, add the following to StepDefsSpring.java:
```java
@Given("a todo object exists with an id of {int}")
    public void an_object_exists(Integer id){
        ResponseEntity<Todo> checkTodo = todoService.getTodo(id);
        Assert.assertNotNull(checkTodo.getBody());
    }

    @When("I delete the todo object with an id of {int}")
    public void delete_with_id(Integer id){
        try {
            ResponseEntity responseEntity = todoService.deleteTodo(id);
            response = responseEntity.getStatusCode().value();
        }
        catch(ResponseStatusException e){
            response = e.getStatus().value();
        }
    }

    @When("I get a todo object with an id of {int}")
    public void get_with_id(Integer id){
        try {
            ResponseEntity responseEntity = todoService.getTodo(id);
            response = responseEntity.getStatusCode().value();

        }
        catch(ResponseStatusException e){
            response = e.getStatus().value();
        }

    }
```{{copy}}
4. Run the tests one more time `mvn clean test`
