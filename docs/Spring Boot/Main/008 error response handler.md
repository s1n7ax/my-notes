# Error response handler

`ResponseEntityExceptionHandler` handles the response when there is an error.
This can be customized by extending the class

```java
@ControllerAdvice
class ErrorResponseHandler extends ResponseEntityExceptionHandler {

 @ExceptionHandler(RuntimeException.class)
 public final ResponseEntity<ErrorRecord> handleExceptionResponse(Exception ex, WebRequest request) throws Exception {
  var error = new ErrorRecord(ex.getMessage(), request.getDescription(false));
  return new ResponseEntity<ErrorRecord>(error, HttpStatus.SERVICE_UNAVAILABLE);
 }

 @ExceptionHandler(UserNotFoundException.class)
 public final ResponseEntity<ErrorRecord> handleUserNotFoundExceptionResponse(UserNotFoundException ex,
   WebRequest request) throws Exception {
  var error = new ErrorRecord(ex.getMessage(), request.getDescription(false));
  return new ResponseEntity<ErrorRecord>(error, HttpStatus.NOT_FOUND);
 }
}
```
