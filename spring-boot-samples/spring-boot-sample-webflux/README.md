# spring-boot-config-example
This is a simple Spring Boot project demonstrating how Spring picks up the configurations from different locations.

# instruction
## build the source
```bash
mvn clean package
```

## Run with configurations in JAR
```
java -jar target/spring-boot-sample-webflux-2.0.0.BUILD-SNAPSHOT.jar
```

## External configurations
### Preparation
First we copy the configuration files to somewhere else
```
cp src/main/resources/*.properties /tmp/config
```

Test echo endpoint
```
curl -X POST -d "aaa" http://localhost:8080/echo
#Hello,aaa by default
```

### Using external configuration files
Let's change `echo.prefix=Hello,` to `echo.prefix=Hello World,`!
```
java -jar target/spring-boot-sample-webflux-2.0.0.BUILD-SNAPSHOT.jar --spring.config.location=/tmp/config/
```

Test echo endpoint
```
curl -X POST -d "aaa" http://localhost:8080/echo
#Hello World,aaa by default
```

### Extra profile
Now we run with profile `admin` too!
```
java -jar target/spring-boot-sample-webflux-2.0.0.BUILD-SNAPSHOT.jar --spring.config.location=/tmp/config/ --spring.profiles.active=admin
```

Test echo endpoint
```
curl -X POST -d "aaa" http://localhost:8080/echo
#Hello World,aaa by admin
```