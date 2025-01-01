# How a new request is handled

- DispatcherServlet - is the front controller which takes all the requests and
  sends it to the appropriate handler
- Controller (user) - controller will handle the request and return a value
- JacksonHttpMessageConverters - return value will be converted to json
- ErrorMvcAutoConfiguration - handles the errors
