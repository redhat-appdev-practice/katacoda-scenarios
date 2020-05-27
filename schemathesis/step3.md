## Run the tests
1. Ensure that the application is running (the tests will be run against the running application): `mvn spring-boot:run`
2. In our project we are using an OAS that is in a remote repo, Scemathesis allows you to run tests against both local
remote schemas:
    - For local: `schemathesis run todo.yaml --base-url http://localhost:8080`{{execute}}
    - For remote: `schemathesis run https://raw.githubusercontent.com/redhat-appdev-practice/schemathesis-lab/master/todo.yaml --base-url http://localhost:8080`{{execute}}

        <sub>Note: there should be failures for both of these runs</sub>
