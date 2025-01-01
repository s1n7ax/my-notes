# Path Parameters

- Here, name of the path variable `{id}` should match to the parameter
  `@PathVariable long id`

```java
record EmployeeRecord(long id, String name, int age) {
}

@RestController
public class Employee {

 @GetMapping("/employee/{id}")
 public EmployeeRecord test(@PathVariable long id) {
  return new EmployeeRecord(id, "s1n7ax", 30);
 }
}
```

- If the name of the parameter is different, name of the relavent path
  parameter can be added to `@PathVariable` annotation

```java
// even though the names a different, path `id` will be mapped to `uuid`
// because the relationship is
// mentioned in the @PathVariable("id") annotation
@GetMapping("/employee/{id}")
public EmployeeRecord test(@PathVariable("id") long uuid)
```
