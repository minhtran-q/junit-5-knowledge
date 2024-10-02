# Unit Test Knowledge
## Architecture
<details>
  <summary>Overview</summary>
  <br/>
  
  ![](images/detailed_JUnit_5_architecture.png)
  
  Ref: https://nipafx.dev/junit-5-architecture-jupiter/
  
</details>

### Terminology
<details>
  <summary>What exactly is a "unit" in unit testing?</summary>
  <br/>
  
   A unit is "the smallest piece of the code that can be usefully tested".
  
</details>
<details>
  <summary>Unit Test vs Integration Test</summary>
  <br/>
  
  **Unit Test**
  
  A unit test covers a single “**unit**”, where a unit commonly is a single class.
  
  **Integration Test**
  
  An integration test can be any of the following:
  
  + A test that covers multiple “units”. It tests the interaction between two or more classes
  + A test that covers multiple layers, might cover the interaction between a business service and the persistence layer, for instance.
  + A test that covers the whole path through the application. We send a request to the application and check that it responds correctly and has changed the database state according to our expectations.
  
</details>
<details>
  <summary>@SpringBootTest vs Mockito</summary>
  <br/>
  
  In my opinion, even we're using a mocked bean, but we're still running within spring context and for me this is an **integration test**(a unit test doesn't need any spring context to run within).
  
  With unit testing  just use **Mockito** or another framework that doesn’t need spring context(`@SpringBootTest`). When writing a test for a service class to test some calculation logic, we don’t need spring context and this is a **PURE** unit test.
  
  When running a test in spring context, this is considered an integration test even if you're using `@MockBean`.
  
  Ref: https://stackoverflow.com/questions/54658563/unit-test-or-integration-test-in-spring-boot
</details>
<details>
  <summary>JUnit 5 vs Mockito</summary>
  <br/>

  JUnit 5 focuses on writing and running tests, while Mockito focuses on creating and managing mock objects.

  **JUnit 5**
  + Uses annotations like `@Test`, `@BeforeEach`, `@AfterEach` to define test methods and lifecycle methods.
  + Provides methods to assert conditions in your tests.

  **Mockito**
  + Allows creating mock objects to mimic the behavior of real objects.
  + Defines the behavior of mock objects.
  
</details>

### Annotation

## Mockito
### Terminology
<details>
  <summary>What is Stub?</summary>
  <br/>
</details>

<details>
  <summary>Strict stubbing</summary>
  <br/>
</details>

<details>
  <summary>Stubbing vs Stub</summary>
  <br/>

  **Stub:**
  + Stub: A stub is a mock object that has been configured to return specific values or perform specific actions when certain methods are called.
  
  ```
  @Test
  void getUser_success() {
    // Create a stub for the UserDAO
    UserDao userDao = Mockito.mock(UserDao.class);
    ...
  }
  ```

  **Stubbing:**
  + Stubbing is the process of defining the behavior of a mock object’s method. When you stub a method, you specify what it should return when called with certain arguments.
  + The act of using fake objects.

  **Example:**
  ```
  when(mockObject.someMethod()).thenReturn(someValue);
  ```
</details>

### Annotation
<details>
  <summary>Popular annotation</summary>
  <br/>
  
  Annotation | Description |
  --- | --- |
  @Mock | Use to create and inject mocked instances without having to call `Mockito.mock` manually. |
  @Spy | Part of the object will be mocked and part will use real method invocations. |
  @Captor | To capture **arguments** that are passed to the methods of mocked objects.  |
  @InjectMocks | Creates an instance of the class and injects the mocks that are created with the `@Mock` (or `@Spy`). |

  
</details>
<details>
  <summary>@Mock vs @MockBean</summary>
  <br/>
  
  **@Mock**
  
  This annotation is a shorthand for the `Mockito.mock()` method. The `Mockito.mock()` method allows us to create a mock object of a class or an interface. 
  
  **@MockBean**
  
  Use the `@MockBean` to add mock objects to the _Spring application context_.
   
  Ref: https://www.baeldung.com/java-spring-mockito-mock-mockbean
  
</details>
<details>
  <summary>@Mock vs @Spy</summary>
  <br/>
  
  Mock| Spy |
  --- | --- |
  A mock in mockito is a normal mock | A spy in mockito is a partial mock | A spy in mockito is a partial mock
  allows you to stub invocations; that is, return specific values out of method calls | part of the object will be mocked and part will use real method invocations
  
  _Example:_
  ```
    @Mock
    private List<String> mockList;
 
    @Spy
    private List<String> spyList = new ArrayList();
 
    @Test
    void testMockList() {
        //by default, calling the methods of mock object will do nothing
        mockList.add("test");

        Mockito.verify(mockList).add("test");
        assertEquals(0, mockList.size());
        assertNull(mockList.get(0));
    }
 
    @Test
    void testSpyList() {
        //spy object will call the real method when not stub
        spyList.add("test");

        Mockito.verify(spyList).add("test");
        assertEquals(1, spyList.size());
        assertEquals("test", spyList.get(0));
    }
  ```
</details>
<details>
  <summary>How @Captor work?</summary>
  <br/>
  
</details>
<details>
  <summary>@InjectMocks vs @Mock</summary>
  <br/>
  
</details>
<details>
  <summary>Explain @ExtendWith(MockitoExtension.class)</summary>
  <br/>
  
</details>
<details>
  <summary>Explain @RunWith(MockitoJUnitRunner.class)</summary>
  <br/>
  
</details>
<details>
  <summary>Explain @Timeout</summary>
  <br/>
  
</details>

### Mocking Static Methods
<details>
  <summary>Example Mocking Static method</summary>
  <br/>
  
</details>

## Spring Boot Test

<details>
  <summary>@SpringBootTest</summary>
  <br/>
  
  Spring Boot provides the `@SpringBootTest` annotation which we can use to create an application context containing all the objects we need for all of the test types.
  
  The @SpringBootTest annotation loads the complete Spring application context.
  
  _However, that overusing `@SpringBootTest` might lead to very long-running test suites._
  
  Ref: https://reflectoring.io/spring-boot-test/
  
</details>
<details>
  <summary>@WebMvcTest</summary>
  <br/>
  
</details>
<details>
  <summary>@DataJpaTest</summary>
  <br/>
  
</details>
<details>
  <summary>@DataJdbcTest</summary>
  <br/>
  
</details>
<details>
  <summary>@WebFluxTest</summary>
  <br/>
  
</details>

