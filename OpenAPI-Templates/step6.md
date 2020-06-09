## Add our annotations to the OAS file
  - Add the following to the `todo` section inside of paths/componenets/schemas section
    ```yaml
      x-java-class-annotation:
        - "@javax.persistence.Entity"
    ```{{copy}}
  - Add the following field annotations to the the properties id section under the todo schema:
    ```yaml
      x-java-field-annotation:
        - "@javax.persistence.Id"
        - "@javax.persistence.GeneratedValue(strategy = javax.persistence.GenerationType.IDENTITY")
    ```{{copy}}
  - Validate
    - Running the following command will output the model info used by the templates to the OpenAPIModel.json file
      ```sh
        ./print-model.sh | grep -Pzo "(?s)############ Model info ############\n(\K\[.*?\} \]\n)" > OpenAPIModel.json
      ```{{copy}}
      - Note: In the print-model.sh the `-DdebugModels` is the flag that outputs the model object
    - Search through the file for "@javax.persistence" and validate the custom annotations are inside the vendor extensions at the correct level
    - Note this is the data used when building the files, meaning any existing data here can be used when modifying templates
  - Regenerate And Run
    - Run `mvn generate-sources`{{execute}}
      - Validate annotations are showing up on `Todo.java`
    - Run `mvn spring-boot:run`{{execute}}
      - Validate all endpoints work (some data should be preloaded)
