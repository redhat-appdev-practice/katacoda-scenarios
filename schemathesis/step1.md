## Intro
In this lab we are going to look at testing our application using test cases that are generated using the
OAS(OpenAPI Spec). To accomplish this task we will be using a tool called Schemathesis.

Schemathesis is a tool for testing your web applications built with an Open API specifications.
It reads the application schema and generates test cases which will ensure that your application is compliant with its
 schema.
The nice thing about Schemathesis is that The application being test could be written in any language, the only thing
you need is a valid API schema in a supported format. For more information on Schemathesis, you can check out the
project page [here](https://github.com/kiwicom/schemathesis).