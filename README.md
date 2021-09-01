# dio-santander-java-product-catalog

Building a project with microservices architecture using Spring Cloud



> Aprenda na prática como funciona uma arquitetura de software baseada em microsserviços, 
> os seus benefícios e desafios. by: [@Oswaldo Neto](https://github.com/oswaldoneto)

## Preparing the Development environment

Workspace uses:

- Docker 19.3.15
- Docker compose 1.29.2
- Java OpenJDK 16
- Gradle
- Spring Boot 2.5.2

### Install Docker Compose




```bash
~$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```




## Running the application

#### Product-catalog application

Let's start by running the Spring application using your favourite IDE.



Two lines that interest us:

- Tomcat started on port(s): 8080
- Exposing 1 endpoint(s) beneath base path '/actuator'

After started, we should be able to reach the following url:

```bash
~$  curl http://localhost:8080/actuator | json_pp
```

and see the endpoints returned:


```bash
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                               Dload  Upload   Total   Spent    Left  Speed
100   243    0   243    0     0  13453      0 --:--:-- --:--:-- --:--:-- 14294
{
   "_links" : {
      "self" : {
         "templated" : false,
         "href" : "http://localhost:8080/actuator"
      },
      "health" : {
         "href" : "http://localhost:8080/actuator/health",
         "templated" : false
      },
      "health-path" : {
         "href" : "http://localhost:8080/actuator/health/{*path}",
         "templated" : true
      }
   }
}
```

#### Running Elasticsearch and redis

Inside the `docker-services` folder we have a file the can start two important services for our application:

```yml
version: '2'

services:

    elasticsearch:
        container_name: 'elasticsearch'
        image: elasticsearch:6.6.2
        ports:
            - 9200:9200
            - 9300:9300
        environment:
            - discovery.type=single-node

    redis:
        container_name: "redis"
        image: redis:3.0.1
        ports:
            - 6379:6379
```

You can start them by running `docker-compose up -d` inside the folder, so it will run the file automatically.

More about how to use [Docker compose][1]

To check the services health, go to `http://localhost:8080/actuator/health` and see the output:

```json
{ "status" : "UP" }
```

