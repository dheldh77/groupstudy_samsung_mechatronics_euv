
Application deployment script:
```shell
#!/bin/bash

REPOSITORY=/home/ec2-user/app/step1
PROJECT_NAME=springboot-webservice

cd $REPOSITORY/$PROJECT_NAME/

echo "> Git Pull"

git pull

echo "> Start building project"

./gradlew jarBoot   # --> Use jarBoot instead of build

echo "> Copying build file"

cp $REPOSITORY/$PROJECT_NAME/build/libs/*.jar $REPOSITORY/

echo "> Checking pid of current application"

CURRENT_PID=$(pgrep -f ${PROJECT_NAME}.*.jar)

if [ -z "$CURRENT_PID" ]; then
        echo "> Cannot kill process. There is no application running. "
else
        echo "> kill -15 $CURRENT_PID"
        kill -15 $CURRENT_PID
        sleep 5
fi

echo "> Deploying new application"

JAR_NAME=$(ls -tr $REPOSITORY/ | grep jar | tail -n 1)

echo "> Jar Name: $JAR_NAME"

nohup java -jar -Dspring.config.location=classpath:/application.yml,/home/ec2-user/app/application-oauth.yml $REPOSITORY/$JAR_NAME 2>&1 &
```


Used `./gradlew jarBoot` instead of `build`.
* `build` is from the [base plugin](https://docs.gradle.org/current/userguide/base_plugin.html)
    > Intended to build everything, including running all tests, producing the production artifacts and generating documentation. You will probably rarely attach concrete tasks directly to build as assemble and check are typically more appropriate.
* `jarBoot` is from the spring boot gradle plugin
    > A custom Jar task that produces a Spring Boot executable jar.


When you check nohup.out and you get the following error: `NoClassDefFoundError`, you need to define the main class in your `build.gradle` file
```groovy
jar {
    manifest {
        attributes(
                'Main-Class': 'com.example.springboot.Application'
        )
    }
}
```