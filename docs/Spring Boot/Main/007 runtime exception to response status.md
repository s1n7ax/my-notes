# Runtime exception to response status

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
class UserNotFoundException extends RuntimeException {
 public UserNotFoundException(String message) {
  super(message);
 }
}

@RestController
public class Employee {

 @GetMapping("/employee/{id}")
 public EmployeeRecord test(@PathVariable long id) {
  if (id == 20) {
   throw new UserNotFoundException("No user found by id " + id);
  }
  return new EmployeeRecord(id, "s1n7ax", 30);
 }
```
