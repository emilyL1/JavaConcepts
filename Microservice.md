# Microservice

### monolithic
All components are bound together.

### SOA
- Service-Oriented Architecture
- Focusing on interaction and integration between independent services, usually using a service bus, SOAP or messaging system.

## Microservices
Microservices is a synonym for Service Oriented Architectural (SOA) style of constructing aggregation of many small loosely coupled services.

Split the application into tiny little services and then link them together using distributed communication, like http, service discovery, load balancing and api gateway.

### advantage
- scalability
    - increase/decrease on demand
- flexibility
    - Each service could be developed, tested, deployed separately
- resilient
    - Elastically adding/removing nodes for each service won't cause issues to the overall application. Network failures can be recovered by using retry circuit breakers.

### disadvantage
- There is a higher chance of failure during communication between different services.
- Difficult to manage a large number of services.
- The developer needs to solve the problem, such as network latency and load balancing.

### Framework
- Service Discovery
    - Eureka
    ```yml
    eureka: # Configure this Discovery Server
        instance:
          hostname: localhost
        client: 
            registerWithEureka: false
            fetchRegistry: false
    server: # HTTP (Tomcat) port
        port: 9000     
    ```
    ```java
        @SpringBootApplication
    @EnableEurekaServer
    public class DiscoveryServerApplication {
        public static void main(String[] args) {
      SpringApplication.run(DiscoveryServerApplication.class, args);
        }
    }
    ```
    Consumer Service
    ```yml
    spring: # Service registers under this name
        application:
            name: consumer-service
    eureka: # Discovery Server Access
        client:
            serviceUrl:
                defaultZone: http://localhost:9000/eureka/
    server: # HTTP Server (Tomcat) Port
        port: 8081

    ```
    include RemoteRepository bean and RestTemplate bean in main application, so that this microservice can consume other microservices.
    ```java
        @SpringBootApplication
    @EnableDiscoveryClient
    public class ConsumerServiceApplication {
     
        public static final String AUTHENTICATION_SERVICE_URL = "http://AUTHENTICATION-SERVICE";
     
        public static void main(String[] args) {
            SpringApplication.run(ConsumerServiceApplication.class, args);
        }
     
        @Bean
        @LoadBalanced
        public RestTemplate restTemplate() {
            return new RestTemplate();
        }
     
        @Bean
        public AuthenticationRepository authenticationRepository(){
            return new RemoteAuthenticationRepository(AUTHENTICATION_SERVICE_URL);
        }
    }
    ```
    - Consul
- LoadBalancer
    - Ribbon + RestTemplate
- Log Tracing
    - Sleuth
        - manage traceID, spanID
    - Zipkin
        - put traceID together
        - splunk/ elastic search
- Config Server
    - Spring Config Server can be used for centralizing all the configuration files for each service
- Fault Tolerance
    - [Resilience4j](https://resilience4j.readme.io/docs/)
        - CircuitBreaker
        - Bulkhead
        - RateLimiter
        - Retry

### Demo: 
- [MyIOT](https://github.com/AntraJava/MyIOT)
- [twosum](https://github.com/AntraJava/twosum)
