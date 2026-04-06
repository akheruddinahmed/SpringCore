# 1. Introduction to Spring Framework

Spring is a lightweight, open-source Java framework used to build enterprise-level applications. It simplifies development by providing built-in support for:

- Dependency management
- Web development
- Database access
- Security

The main goal of Spring is to make applications:

- Loosely coupled
- Easy to test
- Easy to maintain

## 2. Inversion of Control (IoC)

### Concept

In traditional Java, developers create objects using `new`.  
In Spring, the container creates and manages objects.

This is called **Inversion of Control (IoC)**.

### Why IoC?

- Reduces tight coupling
- Improves flexibility
- Makes unit testing easier

### Example

**Without Spring:**

```java
class Car {
    Engine engine = new Engine();
}
```

**With Spring:**

```java
class Car {
    Engine engine;

    Car(Engine engine) {
        this.engine = engine;
    }
}
```

Spring injects the dependency instead of creating it.

## 3. Dependency Injection (DI)

### Concept

Dependency Injection means providing required dependencies to a class from outside.

### Types of DI

#### 1) Constructor Injection (Recommended)

```java
@Component
class Car {
    private Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

✔ Ensures dependency is always available.

#### 2) Setter Injection

```java
@Component
class Car {
    private Engine engine;

    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```

✔ Useful for optional dependencies.

## 4. Spring Container

The Spring Container is the core component responsible for managing application objects.

### Responsibilities

- Creates beans
- Injects dependencies
- Manages lifecycle

### Types

- `BeanFactory` → basic container (lazy loading)
- `ApplicationContext` → advanced (eager loading, widely used)

## 5. Beans in Spring

A Bean is any object managed by the Spring container.

### Ways to Define Beans

#### Using `@Component`

```java
@Component
class Engine {}
```

#### Using `@Bean`

```java
@Configuration
class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine();
    }
}
```

### Bean Scopes

| Scope     | Description                               |
|-----------|-------------------------------------------|
| Singleton | One instance per container (default)      |
| Prototype | New instance every time                   |
| Request   | One per HTTP request                      |
| Session   | One per user session                      |

## 6. Stereotype Annotations

These annotations mark classes as Spring-managed beans.

### `@Component`

A generic annotation used to declare a class as a Spring bean.  
Spring automatically detects it during component scanning and creates an object.

Used when the class does not belong to a specific layer.

```java
@Component
class Engine {}
```

### `@Service`

Used in the business logic layer.  
It indicates that the class contains application logic and processing rules.

Improves readability and follows layered architecture.

```java
@Service
class UserService {
    public void process() {}
}
```

### `@Repository`

Used in the data access layer.  
It interacts with the database and also provides exception translation.

Converts database exceptions into Spring exceptions.

```java
@Repository
class UserRepository {
}
```

### `@Controller`

Used in Spring MVC to handle web requests and return views (HTML pages).

```java
@Controller
class HomeController {

    @RequestMapping("/home")
    public String home() {
        return "home";
    }
}
```

### `@RestController`

Used for REST APIs.  
It returns data (JSON/XML) instead of views.

Combination of `@Controller` + `@ResponseBody`.

```java
@RestController
class ApiController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello World";
    }
}
```

## 7. Dependency Injection Annotations

### `@Autowired`

Used to automatically inject dependencies.  
Spring finds the matching bean and injects it.

Can be used on fields, constructors, or setters.

```java
@Autowired
Engine engine;
```

### `@Qualifier`

Used when multiple beans of the same type exist.  
It specifies which bean should be injected.

```java
@Autowired
@Qualifier("dieselEngine")
Engine engine;
```

### `@Primary`

Marks a bean as the default choice when multiple beans exist.

```java
@Bean
@Primary
public Engine petrolEngine() {
    return new Engine();
}
```

## 8. Configuration Annotations

### `@Configuration`

Marks a class as a configuration class that defines beans.

```java
@Configuration
class AppConfig {}
```

### `@Bean`

Used to manually create and configure a bean.

Useful for third-party classes or custom configurations.

```java
@Bean
public Engine engine() {
    return new Engine();
}
```

### `@ComponentScan`

Tells Spring where to scan for components.

```java
@ComponentScan("com.app")
```
