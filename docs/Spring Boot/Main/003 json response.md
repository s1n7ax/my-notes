# Json Response

When an object is returned, spring boot will parse it to a json.

```java
record HelloWorldRecord(String greeting) {
}

@RestController
public class HelloWorld {

 @GetMapping("/hello-world")
 public HelloWorldRecord greet() {
  return new HelloWorldRecord("Hello World");
 }
}
```
