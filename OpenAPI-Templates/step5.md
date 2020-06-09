## Update `pojo.mustache` to include custom annotations
  - Inorder to use custom properties inside of templates are stored in 'vendorExtensions' and should begin with `x-`. You can read more about that [here](https://swagger.io/docs/specification/openapi-extensions/)
   - Add class annotations
      - Add the following directly above `@ApiModel` annotation (~line 4)
        ```mustache
        {{#vendorExtensions.x-java-class-annotation}}
        {{{.}}}
        {{/vendorExtensions.x-java-class-annotation}}
        {{^vendorExtensions.x-java-class-annotation}}
        //TODO: x-java-class-annotation required
        {{/vendorExtensions.x-java-class-annotation}}

        ```{{copy}}
        
       - `#` specifies the start of an array and `/` is the end so the above code will loop through our `x-java-class-annotation` and print the content of of each
       - `^` specifies inverted section. meaning the TODO message will be printed if the `x-java-class-annotation` is empty or non-existing
       - {{{.}}} prints the value of each of the items inside the array. Note the triple bracket was used over the double one. This prevents mustache from attempting to url encoding of the values
   - Add field annotations
      - Add the following directly above `@JsonProperty("{{baseName}}"){{#withXml}}` (~line 29)
        ```mustache
          {{#vendorExtensions.x-java-field-annotation}}
          {{{.}}}
          {{/vendorExtensions.x-java-field-annotation}}
        ```{{copy}}
   - Regnerate source and validate our TODO is showing up
      - `mvn generate-sources`{{execute}}
