
- View the `api/TodosApis.java`
      - The interface created from the *paths* inside of your OAS file.
      - Contains all of your path's Swagger annotations
      - There is also a basic implementation of each of your path methods returning a 503<sub>Not Implemented</sub>. You may have noticed this if you attempted this in the previous step
- View the `api/TodoApiController.java`
      - Currently there is very little besides the RequestMapping annotation inside of this controller
      - This will be where we implement the methods inside of the TodoApi
- View `model/Todo.java`
      - The pojo object represented by the *schema* section of your OAS file
