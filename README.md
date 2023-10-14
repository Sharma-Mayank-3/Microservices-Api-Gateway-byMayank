# Microservices-Api-Gateway-byMayank

# Steps to implement Api-Gateway

1. Add cloud bootstrap dependency.
2. Add Gateway dependency 
3. lombok
4. webflux
5. eureka discovery client.


# Add api-gateway to service registry service.

1. add configuration to application.properties file.
```yaml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
    fetch-registry: 'true'
    register-with-eureka: 'true'
  instance:
    preferIpAddress: 'true'
spring:
  application:
    name: API-GATEWAY-SERVICE
server:
  port: '8084'

```

2. Add Annotation to the main class.

       @EnableDiscoveryClient


# Add Gateway configuration in the application.yml file.

```yaml
  cloud:
    gateway:
      routes:
        - id: HOTEL-SERVICE
          uri: http://localhost:8082
          predicates:
            - Path=/microservices/hotel/**

        - id: USER-SERVICE
          uri: http://localhost:8080
          predicates:
            - Path=/microservices/user/**

        - id: RATING-SERVICE
          uri: http://localhost:8083
          predicates:
            - Path=/microservices/rating/**

```

# NOTE : If you don't want to add url and take it directly from service registry.
```yaml
cloud:
    gateway:
      routes:
        - id: HOTEL-SERVICE
          uri: lb://HOTEL-SERVICE
          predicates:
            - Path=/microservices/hotel/**
```


# NOTE : If you don't want to add other url present in service.
```yaml
cloud:
    gateway:
      routes:
        - id: HOTEL-SERVICE
          uri: lb://HOTEL-SERVICE
          predicates:
            - Path=/microservices/hotel/**, /yyy/**
```