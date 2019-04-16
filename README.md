# microservices-spring-boot
Forex Service (FS) is the Service Provider (spring-boot-microservice-forex-service). It provides currency exchange values for various currency. Here is the sample request call for this service : http://localhost:8000/currency-exchange/from/EUR/to/INR

Currency Conversion Service (CCS) can convert a bucket of currencies into another currency (spring-boot-microservice-currency-conversion). It uses the Forex Service to get current currency exchange values. CCS is the Service Consumer. Here is the same request for this service : 
http://localhost:8100/currency-converter/from/EUR/to/INR/quantity/10000

Based on the load, we can have multiple instances of the Currency Conversion Service and the Forex Service running. 

We will use Ribbon for Load Balancing and Eureka Naming server for registering all microservices. The Eureka service is accessible at http://localhost:8761/ 

All instances of the components (CCS and FS) register with the Eureka Naming Server. When FS needs to call the CCS, it will ask Eureka Naming Server for the active instances. We will use Ribbon to do Client Side Load Balancing between the different instances of FS.

Here are the things which we have done for these microservices to interact with each other and scale.

1. Creating a Forex Microservice - We will create a simple rest service based on Spring Boot Starter Web and Spring Boot Started JPA. We will use Hibernate as JPA implmentation and connect to H2 database.
2. Create the CCS - Currency Conversion Service - We will create a simple rest service using feign to invoke the Forex Microservice
3. Use Ribbon for Load Balancing
4. Implement Eureka Naming Service and connect FS and CCS through Eureka.
