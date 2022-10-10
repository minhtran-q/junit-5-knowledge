# Junit 5 Knowledge
## Architecture
<details>
  <summary>Overview</summary>
  <br/>
  
  ![](images/detailed_JUnit_5_architecture.png)
  
  Ref: https://nipafx.dev/junit-5-architecture-jupiter/
  
</details>

### Terminologies
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
  
  Ref: 
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
  <summary>What is a "Stub"?</summary>
  <br/>
  
  Stub objects provide canned responses (and can be autogenerated by helper libraries), but typically do not directly cause the unit test to fail.
  
  ```
  @Test
  public void whenUseSpyAnnotation_thenSpyIsInjectedCorrectly() {
      spiedList.add("one");
      spiedList.add("two");

      Mockito.verify(spiedList).add("one");
      Mockito.verify(spiedList).add("two");

      assertEquals(2, spiedList.size());

      Mockito.doReturn(100).when(spiedList).size(); \\stub
      assertEquals(100, spiedList.size());
  }
  ```
  
  Ref: https://stackoverflow.com/questions/463278/what-is-a-stub
</details>

## Annotation
## In Spring Boot

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

## Mockito
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
   
  + Ref: https://www.baeldung.com/mockito-annotations
  + Ref: https://medium.com/javarevisited/argument-capturing-a-must-know-unit-testing-technique-e88b3a6a6af1
  + Ref: https://stackoverflow.com/questions/16467685/difference-between-mock-and-injectmocks
  
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
  
  + Ref: https://dzone.com/articles/mockito-mock-vs-spy-in-spring-boot-tests#:~:text=A%20Mockito%20spy%20is%20a,therefore%20the%20term%20partial%20mock.
  + Ref: https://stackoverflow.com/questions/28295625/mockito-spy-vs-mock#:~:text=The%20difference%20is%20that%20in,call%20the%20real%20method%20behavior.
  
</details>

Ref: https://www.javadoc.io/doc/org.mockito/mockito-core/2.23.4/org/mockito/Mockito.html#3
