# api-gateway
  This ms is act as gateway to [address-ms2](https://github.com/tsmahur/address-ms1), [user-ms2](https://github.com/tsmahur/user-ms2). This is a part of [ms-eureka-gateway-hysrtix-cloud-config](https://github.com/tsmahur/ms-eureka-gateway-hysrtix-cloud-config) Project.

  It also implements the following:
  - implementing circuit breaker in the artchitecture 
  - identify the service that is not running
  - run the fallback method available (FallbackController.java)
  - notify the user about the status not running
  - hystrix library and dashboard so that first hystrix in api-gateway then fallback method and configurations for each service
  
##
### Dependency
    eureka discover client, gateway, spring boot actuator, spring-cloud-starter-netflix-hystrix
   ***using older sprng boot version and dependencies - latest are having some problem with circuit breaker for fallback config (-filters) and also no need of config:import: optional:configserver:http://localhost:8094 in old version***

### application.yml
    port, app name, gateway-routes, predicates, filters (for fallback), hystrix config,
    management (management/hystrix.stream so that can acess from hystrix), eureka client(same in all MS)

### main application class
    @EnableEurekaClient, @EnableHystrix

### EndPoints (through gateway) 
    
    GET http://localhost:8092/address/1
    POST http://localhost:8092/address
    {
        "city": "Noida",
        "state": "Up",
        "pinCode": 1233456
    }

    GET http://localhost:8092/users/1
    POST http://localhost:8092/users
    {
        "firstName":"Ravi",
        "lastName": "Verma",
        "email": "ac@abc.com",
        "addressId": 1
    }
