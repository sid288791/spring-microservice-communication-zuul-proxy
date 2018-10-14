# Spring Microservices Communication Using Gatway Zuul Proxy
Steps which needs to be followed are as :-

## Create Eureka Server
- > Create maven project and add the required dependencies such as spring-cloud-starter-netflix-eureka-server and spring-boot-starter-test
- > Create application.properties and add server.port="give any value default 8761",eureka.client.register-with-eureka=false,eureka.client.fetch-registry=false
- > Add EnableEurekaServer annotation in your Application class.
- > Finally run the application class and hit the url http://localhost:8761


## Create Hello Client
- > Create maven project and add the required dependencies such as spring-cloud-starter-netflix-eureka-client,spring-cloud-starter-sleuth,spring-boot-starter-web and spring-cloud-starter-feign
- > Create application.properties and add server.port="give any value default (we are using 8072)", 
spring.application.name=hello-client, 
eureka.client.register-with-eureka=true, 
eureka.client.fetch-registry=true, 
eureka.client.serviceUrl.defaultZone:http://localhost:8761/eureka/, 
eureka.instance.hostname:localhost
- > Add EnableDiscoveryClient and EnableFeignClients annotation in your Application class.
- > Add interface and annotated it with FeignClient annotation.
- > Add Rest Controller and call hello service using feign client interface.
- > Add required logs
- > Finally run the application and hit the url http://localhost:8072/rest/hello/client


## Create Hello Service
- > Create maven project and add the required dependencies such as spring-cloud-starter-netflix-eureka-client,spring-boot-starter-web,spring-cloud-starter-sleuth
- > Create application.properties and add server.port="give any value default (we are using 8071)", 
spring.application.name=hello-service, 
eureka.client.register-with-eureka=true, 
eureka.client.fetch-registry=true, 
eureka.client.serviceUrl.defaultZone:http://localhost:8761/eureka/, 
eureka.instance.hostname:localhost
- > Add EnableDiscoveryClient annotation in your Application class.
- > Add Rest Controller and create method and return any String.
- > Add required logs
- > Finally run the application and if want to check your application hit the url http://localhost:8071/rest/hello/server

## Create Zuul Service
- > Create maven project and add the required dependencies such as spring-cloud-starter-netflix-eureka-client and spring-cloud-starter-netflix-zuul
- > Create application.properties and add server.port="give any value default (we are using 8073)",
spring.application.name=" ",
eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
eureka.client.serviceUrl.defaultZone:http://localhost:8761/eureka/
eureka.instance.hostname:localhost,
zuul.prefix=/api
zuul.routes.hello-service.path=/service/**
#zuul.routes.hello-service.serviceId=HELLO-SERVICE
#mention url when you don't want to go through eureka service or url
zuul.routes.hello-service.url=http://localhost:8071
zuul.routes.hello-client.path=/client/**
zuul.routes.hello-service.serviceId=HELLO-CLIENT
- > Add EnableDiscoveryClient and EnableZuulProxy annotation in your Application class.	
- > Finally run the application and if want to check your application hit the url http://localhost:8073/api/client/rest/hello/client or http://localhost:8073/api/service/rest/hello/server


file:///D:/backup/Siddharth/test/Microservice/Micorservice_Communiation.jpg
