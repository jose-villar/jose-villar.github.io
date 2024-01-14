# Java Spring Boot

Read more at [Learn the
path](https://www.learnthepart.com/course/cfd96af5-ca6d-4529-8fae-55f1d9186bc0/d5982d83-866c-4870-aac8-d65be576bba8)

## Definitions

- **Group ID:** Identifies the organization. Example: com.google
- **Artifact ID:** Determines the name of the application.

## Compile and Run

```sh
# Auto detect changes
gradlew -t :bootJar

# Compile and run
gradlew bootRun

```

## Packages

- **Spring Boot DevTools:** Provides fast application restarts, LiveReload, and
  configurations for enhanced development experience.

## Three layers architecture

This architecture considers:

- Presentation layer (model + view + controller)
- Business logic (service): it has all the business operations (computation and
  decision making processes)
- Data access layer (repository): it has all the CRUD operations.

![Three layers architecture](./assets/three_layers_architecture.png)

## Annotations

- `@Component` annotation is too generic. Use `@Service` for business logic
  layer and `@Repository` for the data access layer instead. They all turn a
  `class` into a `Bean`. `@Controller` also derives from `@Component`.
- `@Configuration` marks a class as a source of `Beans` definitions.
- `@Autowired` wires the class into the `Bean` that needs it.
- `@RestController` = `@Controller` + `@ResponseBody`. `@ResponseBody` converts
  the output to `JSON`.

## Best practices

### Dependency injection

- Never ever create an object inside of a class that depends on it. This is
  called tight coupling and makes unite testing impossible. Instead, use
  dependency injection.

![Dependency injection process](./assets/dependency_injection_process.png)
