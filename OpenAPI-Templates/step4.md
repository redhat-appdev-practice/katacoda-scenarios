## Retrieve pojo.mustache template file
  - Go to [openapi-generator](https://github.com/OpenAPITools/openapi-generator) github
  - Navigate to the `spring` generator inside the module's resources folder
    - `modules/openapi-generator/src/main/resources/JavaSpring
  - This folder contains all of the template files used to generate the spring code from the previous application. It is worth taking some time to look at some of the different templates
    - Note the `library` folder that contains the 3 different libraries you can set. We chose spring boot when creating our application
  - Create new `templates` directory in project base. Then download and add the `pojo.mustache` from the JavaSpring templates
    
      `mkdir templates`{{execute}}
      
      `cd templates/`{{execute}}
      
      `wget https://raw.githubusercontent.com/OpenAPITools/openapi-generator/master/modules/openapi-generator/src/main/resources/JavaSpring/pojo.mustache`{{execute}}
