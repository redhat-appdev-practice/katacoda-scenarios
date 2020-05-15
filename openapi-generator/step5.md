
1. Generate Spring Boot Application:
   - Run the command below, note replace todo.yaml with a path to your file.  
   ```sh
   openapi-generator generate \
        -g spring \
        --library spring-boot \
        -i todo.yaml \
        -o ${PWD} \
        -p groupId=com.redhat \
        -p artifactId=todo \
        -p artifactVersion=1.0.0-SNAPSHOT \
        \
        -p basePackage=com.redhat.todo \
        -p configPackage=com.redhat.todo.config \
        -p apiPackage=com.redhat.todo.api \
        -p modelPackage=com.redhat.todo.model \
        \
        -p sourceFolder=src/main/gen \
        \
        -p dateLibrary=java8 \
        -p java8=true
   ```{{execute}}
   
   <sub>Note: that we are pointing our "sourceFolder" to "src/main/gen". Anything inside the gen folder should be treated as immutable</sub>
   
   - Open the IDE and take some time to look around the code. Take note that we are currently generating all the files related to the application inside of the "src/main/gen" folder
