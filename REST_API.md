# REST API
### REST API
An uniformed, resource-based API which uses HTTP to identify the operations and resources.

- Producer
    - Should define RequestMapping, HTTP method, URI, Request and Response Body, Parameters, Validation, Errors, Authorization
- Consumer
    - Any HTTP client could be a consumer of REST api. RestTemplate class in Spring.
    - HttpClient, OkHTTP, Ajax...
- Verbs
    - GET, POST, PUT, DELETE, PATCH, OPTIONS
    - For crud operations using GET POST PUT DELETE
    - Partially update: PATCH
    - CORS check: OPTIONS(automatically done by the browsers)
- URI
    - The resource identifier. Should be a noun. Should be pointing to "something" instead of "procedure". Example: "/apple"(good) vs "/getApple"(bad). | what resource
    - URL The resource locator | locate the resource on the server
- Payload
    - JSON and XML are the most commonly used formats, especially JSON.
    - <u>Jackson</u> and Jax-B are the two frameworks used internally by Spring to convert between Java Object to <u>JSON(Jackson)</u> and XML(Jax-B)
- Header
    - Declare the meta-data about the request. eg. Content-Type, Content-Length. Declare the security data like Authorization, api-key, cors
    - Declare data that is additional to the body and url parameters
- Security
    - HTTPS to ensure data security in transit. Token based Authentication/Authorization.
### SOAP
Simple Object Access Protocol(SOAP) is a XML based information exchange web service.
#### SOAP vs REST api
- [TBD](https://smartbear.com/blog/soap-vs-rest-whats-the-difference/)
    - 
