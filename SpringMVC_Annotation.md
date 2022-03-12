# SpringMVC Annotation
- @Controller, @RestController
    - Spring 4.0 introduced the @RestController annotation in order to simplify the creation of RESTful web services.  It's a convenient annotation that **<u>combines</u>** `@Controller` and `@ResponseBody`,
    - `@Controller` is simply a specialization of the @Component class, which allows us to auto-detect implementation classes through the classpath scanning.
    - We annotated the request handling method with `@ResponseBody`. This annotation enables automatic serialization of the return object into the HttpResponse.
    - `@Controller` can return pages
- @RequestMapping(URL,Method) -> method
    - is used to map web requests to Spring Controller methods.
    - With the *headers* Attribute
        - produces and consumes. the old type of mapping with the headers attribute will automatically be converted to the new produces mechanism starting with Spring 3.1
            - behave differently from most other annotations: When specified at the type level, the method-level annotations do not complement but override the type-level information. 
    - Spring Framework 4.3 introduced @GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping
        - improve the readability and reduce the verbosity of the code. 
    - input @PathVarible @RequestParam @RequestHeader @RequestBody
        - `@PathVarible`
            - Parts of the mapping URI can be bound to variables via the @PathVariable annotation. /{id}
            - If the name of the method parameter <u>matches</u> the name of the path variable exactly, then this can be <u>simplified by using @PathVariable with no value</u>
        - `@RequestParam `
            - @RequestMapping allows easy mapping of URL parameters with the @RequestParam annotation. ?id
            - `@RequestMapping(value = "/ex/bars", params = "id", method = GET)` narrowing the request mapping
        -  the `@RequestBody` annotation maps the HttpRequest body to a transfer or domain object, enabling automatic deserialization of the inbound HttpRequest body onto a Java object.
    - output @ResponseBody - Json/xml -> Jackson and Jax-b
        - The `@ResponseBody` annotation tells a controller that the object returned is automatically serialized into JSON and passed back into the HttpResponse object.
    - We simply need a `@Configuration` class to enable the full MVC support and <u>configure classpath scanning</u> for the controller:
- @Validated bean validation
    - Java Bean Validation Basics
        - standard framework — JSR 380, also known as Bean Validation 2.0. 
        - This ensures that <u>the properties of a bean meet specific criteria</u>, using annotations such as @NotNull, @Min, and @Max.
        - return ConstraintViolation
    -  JSR-330‘s @Size, Hibernate‘s @Length and JPA @Column(length=value)
    - @Validated vs @ Valid
        - `@Valid` annotation for <u>method level</u> validation. We also use it to <u>mark a member attribute</u> for validation. 
        - for <u>group-level</u>, we have to use Spring's `@Validated` partial validation
            - `@NotNull(groups = BasicInfo.class)`
            - `@Validated(BasicInfo.class) `
- ExceptionHandling
    - Before Spring 3.2, HandlerExceptionResolver or the `@ExceptionHandler`. Since 3.2, we've had the `@ControllerAdvice`
    - @ExceptionHandler -> Exception
        - works at the @Controller level
        - drawback: The @ExceptionHandler annotated method is only active for that particular Controller
    - HandlerExceptionResolver
        - ExceptionHandlerExceptionResolver
            - is enabled by default in the DispatcherServlet. This is actually the core component of how the @ExceptionHandler mechanism presented earlier works.
        - DefaultHandlerExceptionResolver
            -  resolve standard Spring exceptions to their corresponding [HTTP Status Codes](https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/mvc.html#mvc-ann-rest-spring-mvc-exceptions)  
            -  one limitation is that it doesn't set anything to the body of the Response.  
        - limitations: It's interacting with the low-level HtttpServletResponse and fits into the old MVC model that uses ModelAndView,   
    - @ControllerAdvice -> class -> @ExceptionHandler -> global exception handler
        - Spring 3.2 brings support for a global @ExceptionHandler with the @ControllerAdvice annotation.
    - ResponseStatusException (Spring5)
        - implement a @ControllerAdvice globally but also ResponseStatusExceptions locally.
        - This reduces tight coupling compared to the @ExceptionHandler. 
    - Handle the Access Denied 
        - custom handler
            - ``` java
               @Autowired
                private CustomAccessDeniedHandler accessDeniedHandler;
                
                @Override
                protected void configure(HttpSecurity http) throws Exception {
                    http.authorizeRequests()
                        .antMatchers("/admin/*").hasAnyRole("ROLE_ADMIN")
                        ...
                        .and()
                        .exceptionHandling().accessDeniedHandler(accessDeniedHandler)
                }
              ```
        - [method-level security](https://www.baeldung.com/spring-security-method-security) @PreAuthorize, @PostAuthorize, and @Secure  

### Others
- [@Profile](https://www.baeldung.com/spring-profiles)
- [@Qualifier](https://www.baeldung.com/spring-qualifier-annotation)
- [@PostConstruct](https://www.baeldung.com/spring-postconstruct-predestroy)
- [@Refresh](https://www.baeldung.com/spring-reloading-properties)
- [@Component](https://www.baeldung.com/spring-component-annotation)