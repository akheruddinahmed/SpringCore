1. Introduction to Spring Framework

Spring is a lightweight, open-source Java framework used to build enterprise-level applications. It simplifies development by providing built-in support for:

Dependency management
Web development
Database access
Security

 The main goal of Spring is to make applications:

Loosely coupled
Easy to test
Easy to maintain
2. Inversion of Control (IoC)
Concept

In traditional Java, developers create objects using new.
In Spring, the container creates and manages objects.

 This is called Inversion of Control (IoC).

Why IoC?
Reduces tight coupling
Improves flexibility
Makes unit testing easier
Example

Without Spring:

class Car {
    Engine engine = new Engine();
}

With Spring:

class Car {
    Engine engine;

    Car(Engine engine) {
        this.engine = engine;
    }
}

 Spring injects the dependency instead of creating it.

3. Dependency Injection (DI)
Concept

Dependency Injection means:
 Providing required dependencies to a class from outside.

Types of DI
1. Constructor Injection (Recommended)
@Component
class Car {
    private Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}

✔ Ensures dependency is always available

2. Setter Injection
@Component
class Car {
    private Engine engine;

    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}

✔ Useful for optional dependencies

4. Spring Container

The Spring Container is the core component responsible for managing application objects.

Responsibilities
Creates beans
Injects dependencies
Manages lifecycle
Types
BeanFactory → basic container (lazy loading)
ApplicationContext → advanced (eager loading, widely used)
5. Beans in Spring

A Bean is any object managed by the Spring container.

Ways to Define Beans
Using @Component
@Component
class Engine {}
Using @Bean
@Configuration
class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine();
    }
}
Bean Scopes
Scope	Description
Singleton	One instance per container (default)
Prototype	New instance every time
Request	One per HTTP request
Session	One per user session
6. STEREOTYPE ANNOTATIONS

These annotations mark classes as Spring-managed beans.

@Component

A generic annotation used to declare a class as a Spring bean.
Spring automatically detects it during component scanning and creates an object.

 Used when the class does not belong to a specific layer.

@Component
class Engine {}
@Service

Used in the business logic layer.
It indicates that the class contains application logic and processing rules.

 Improves readability and follows layered architecture.

@Service
class UserService {
    public void process() {}
}
@Repository

Used in the data access layer.
It interacts with the database and also provides exception translation.

 Converts database exceptions into Spring exceptions.

@Repository
class UserRepository {
}
@Controller

Used in Spring MVC to handle web requests and return views (HTML pages).

@Controller
class HomeController {

    @RequestMapping("/home")
    public String home() {
        return "home";
    }
}
@RestController

Used for REST APIs.
It returns data (JSON/XML) instead of views.

 Combination of @Controller + @ResponseBody.

@RestController
class ApiController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello World";
    }
}
7. DEPENDENCY INJECTION ANNOTATIONS
@Autowired

Used to automatically inject dependencies.
Spring finds the matching bean and injects it.

 Can be used on fields, constructors, or setters.

@Autowired
Engine engine;

@Qualifier

Used when multiple beans of the same type exist.
It specifies which bean should be injected.

@Autowired
@Qualifier("dieselEngine")
Engine engine;
@Primary

Marks a bean as the default choice when multiple beans exist.

@Bean
@Primary
public Engine petrolEngine() {
    return new Engine();
}
8. CONFIGURATION ANNOTATIONS
@Configuration
+
Marks a class as a configuration class that defines beans.

@Configuration
class AppConfig {}
@Bean

Used to manually create and configure a bean.

 Useful for third-party classes or custom configurations.

@Bean
public Engine engine() {
    return new Engine();
}
@ComponentScan

Tells Spring where to scan for components.

@ComponentScan("com.app")
