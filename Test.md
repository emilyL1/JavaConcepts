# Test
- unit test
    - Test the code piece by piece. To make sure each small part of the code is functional.
    - Junit
        - It is integrated with SpringBoot and Maven
        - mvn test
        - static import 
            - assertTrue(expected,actual) static method
        - Life cycle 
            - @BeforeAll
            - @BeforeEach| clean environment
            - @Test @AfterEach @AfterAll | close connection
    - Mockito
        - The mocking framework mainly focuses on <u>simulating the behavior of the dependencies</u>
            - It can easily mock a DB failure instead of shutting down the DB
        - @Mock
            - `List mockList = Mockito.mock(ArrayList.class);`
            - `@Mock List<String> mockedList;`
            - verify
            ```
            // selective, explicit, highly readable verification
            verify(mockedList).add("one");
            ```
            -  stub method calls
            ```
            // stubbing appears before the actual execution
            when(mockedList.get(0)).thenReturn("first");
            
            // the following prints "first"
            System.out.println(mockedList.get(0));
            ```
        - @Spy
            - partial mocking, real methods are invoked but still can be verified and stubbed
            - Stubbed the method spiedList.size() to return 100 instead of 2 using `Mockito.doReturn()`
        - @Captor 
            - verify(): to check methods were called with given arguments can use <u>flexible argument matching</u>, for example any expression via the `any()` or capture what arguments were called using @Captor instead 
            - `Mockito.verify(mockedList).add(argCaptor.capture());`
        - @InjectMocks
            - @Mock creates a mock. @InjectMocks creates an instance of the class and injects the mocks that are created with the @Mock (or @Spy) annotations into this instance. 
- [integration test](https://www.baeldung.com/integration-testing-in-spring)
    - Make sure all parts work together correctly by integrating multiple components.
    ```java
        @Test
    public void givenGreetURI_whenMockMVC_thenVerifyResponse() {
        MvcResult mvcResult = this.mockMvc.perform(get("/greet"))
          .andDo(print()).andExpect(status().isOk())
          .andExpect(jsonPath("$.message").value("Hello World!!!"))
          .andReturn();
        
        Assert.assertEquals("application/json;charset=UTF-8", 
          mvcResult.getResponse().getContentType());
    }
    ```
-  Code Coverage
    -  Percentage of the executed lines during the test.
    -  SonarQube can be used to collect test coverage
- Code Review
    - pull request  
- TDD/BDD
    - Test(Behavior) Driven Development
    - Focusing on writing tests first then implementation.
    - TDD focuses on test code.
    - BDD focuses on <u>simulating user</u> operation and verifying applications' behavior.  