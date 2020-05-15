
- Add the following maven plugin to your 'pom.xml'
     ```xml
     <plugin>
        <groupId>org.openapitools</groupId>
        <artifactId>openapi-generator-maven-plugin</artifactId>
        <version>4.3.1</version>
        <executions>
            <execution>
                <phase>generate-sources</phase>
                <goals>
                    <goal>generate</goal>
                </goals>
                <configuration>
                    <generatorName>spring</generatorName>
                    <inputSpec>https://raw.githubusercontent.com/jland-redhat/rhc_openapi_todo/todo_enhanced/todo.yaml</inputSpec>
                    <library>spring-boot</library>
                    <output>${project.basedir}</output>
                    <configOptions>
                        <serializableModel>true</serializableModel>
                        <artifactId>${project.artifactId}</artifactId>
                        <groupId>${project.groupId}</groupId>
                        <version>${project.version}</version>
                        <dateLibrary>java8</dateLibrary>
                        <sourceFolder>src/main/gen</sourceFolder>
                        <basePackage>com.redhat.todo</basePackage>
                        <invokerPackage>com.redhat.todo</invokerPackage>
                        <configPackage>com.redhat.todo.config</configPackage>
                        <modelPackage>com.redhat.todo.model</modelPackage>
                        <apiPackage>com.redhat.todo.api</apiPackage>
                    </configOptions>
                </configuration>
            </execution>
        </executions>
     </plugin>
     ```{{copy}}
<sub>Warning: If you did not add pom.xml to your .openapi-generate-ignore file the next build will override your pom.xml and you will need to add back the previous plugin</sub>
     
- Explore the new OAS file being pulled from github
  - Note the new `user` schema as well as the new paths associated with the new user object
- Validate that `TodoApisController.java` has been deleted from your gen folder and regenerate your files with `mvn generate-sources`{{execute}}
- Validate `api/UsersApi.java` and `model/User.java` are generated and the Controller.java are not being generated
