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
  
  Ref: https://reflectoring.io/spring-boot-test/
  
</details>

## Mockito
### Annotation
<details>
  <summary>Popular annotation</summary>
  <br/>
  
  Annotation | Description |
  --- | --- |
  @Mock | Use to create and inject mocked instances without having to call `Mockito.mock` manually. |
  @Spy | Part of the object will be mocked and part will use real method invocations |
  @Captor |  |
  @InjectMocks |  |
   
  Ref: https://www.baeldung.com/mockito-annotations
  
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
