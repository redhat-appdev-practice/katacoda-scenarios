
- Add the following plugin to your 'pom.xml'
   ```xml
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>build-helper-maven-plugin</artifactId>
      <version>3.1.0</version>
      <executions>
        <execution>
          <phase>generate-sources</phase>
          <goals>
            <goal>add-source</goal>
          </goals>
          <configuration>
            <sources>src/main/gen</sources>
          </configuration>
        </execution>
      </executions>
    </plugin>
   ```{{copy}}

- Validate you can run the application
  - Run `mvn spring-boot:run`{{execute}}
  - Navigate to the Swagger UI tab, a refresh may be necessary 
