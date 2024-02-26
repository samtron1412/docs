# Overview

- https://site.mockito.org/
- https://github.com/mockito/mockito
- https://www.vogella.com/tutorials/Mockito/article.html
- https://www.baeldung.com/mockito-series
    + https://www.baeldung.com/mockito-exceptions
- https://www.arhohuttunen.com/junit-5-mockito/

# Mockito 3.x

- Documentation
    + https://javadoc.io/doc/org.mockito/mockito-core/3.12.4/org/mockito/Mockito.html

## Mocking UUID or Clock

- https://rieckpil.de/mocking-static-methods-with-mockito-java-kotlin/

## Mocking static methods

- https://www.baeldung.com/mockito-mock-static-methods
- https://wttech.blog/blog/2020/mocking-static-methods-made-possible-in-mockito-3.4.0/

```java
@Test
void givenStaticMethodWithArgs_whenMocked_thenReturnsMockSuccessfully() {
    assertThat(StaticUtils.range(2, 6)).containsExactly(2, 3, 4, 5);

    try (MockedStatic<StaticUtils> utilities = Mockito.mockStatic(StaticUtils.class)) {
        utilities.when(() -> StaticUtils.range(2, 6))
          .thenReturn(Arrays.asList(10, 11, 12));

        assertThat(StaticUtils.range(2, 6)).containsExactly(10, 11, 12);
    }

    assertThat(StaticUtils.range(2, 6)).containsExactly(2, 3, 4, 5);
}
```

## Mocking an enum

- https://stackoverflow.com/a/70593736
- Reload enum when it is needed to prevent failures from other tests
    + https://stackoverflow.com/questions/21941777/reload-java-enum
    + Failure: https://github.com/mockito/mockito/issues/2183

```java
@Test
void testGetConsumableQuantity_UnknownLocation_Exception() {
    // Mock the InventoryLocation enum and an unsupported inventory location for the exception case.
    // Currently, InventoryLocation enum has two values: PRIME and RESERVE, mocked value UNSUPPORTED is added for testing.
    try (MockedStatic<InventoryLocation> mockedStaticInventoryLocation = mockStatic(InventoryLocation.class)) {
        final InventoryLocation UNSUPPORTED = mock(InventoryLocation.class);
        doReturn(2).when(UNSUPPORTED).ordinal();
        mockedStaticInventoryLocation.when(InventoryLocation::values).thenReturn(new InventoryLocation[]{InventoryLocation.PRIME, InventoryLocation.RESERVE, UNSUPPORTED});

        final InventoryContainer container = new InventoryContainer(ID, CONTAINER_TYPE, EACHES_QUANTITY, UNSUPPORTED, PARENT,
                TRANSFER_COST, EACHES_TRANSFER_COST, SPLIT_COST_PER_UNIT, SUBCONTAINERS);

        final Exception exception = assertThrows(IllegalStateException.class, () -> container.getConsumableQuantity());
        assertTrue(exception.getMessage().contains("Unknown inventory location"));
    }
}
```

# Spy

- https://stackoverflow.com/questions/11620103/mockito-trying-to-spy-on-method-is-calling-the-original-method
    + Using `doReturn(obj).when(spy).method(params)` rather than
      `when(spy.method(params)).thenReturn(obj)`

# Tips and Tricks

## Mockito and JUnit5 (extension and annotations)

- https://www.arhohuttunen.com/junit-5-mockito/
- 3 ways to initialize and create mocks
    + Manual initialization
        * `Mockito.mock()`
        * Pros: most control
        * Cons: verbose, Does not validate framework usage or detect incorrect stubbing
    + Annotation Based Initialization
        * annotations (`@Mock`, `@InjectMocks`, etc.) and `MockitoAnnotations.openMocks()`
        * Pros: easy to create mocks, readable
    + Mockito JUnit 5 Extension: mockito-junit-jupiter
        * `@ExtendWith(MockitoExtension.class)` and annotations
        * No need for `openMocks()`
        * Strict stubbing

## Fake vs. Spy vs. Mock vs. Stub

- https://stackoverflow.com/questions/28295625/mockito-spy-vs-mock
- Fake
    + A lightweight/modified version of the real implementation.
    + Subclass and override methods ??
    + Similar to partial mocking ??
- Spy
    + Wrap around the real object and will call the underlined real
      methods
    + We can mock some of the Spy's methods but keep other methods as
      is.
- Mock
    + A fake object and does not call the underlined real methods
    + All invocations to all methods return null if we don't have define
      return values for mock methods.
        * Many people make mistake with not mocking all methods.
- Stub
    + No logic, always return a fixed value when it is invoked.

### Partial mocking

- https://web.archive.org/web/20090820023945/https://monkeyisland.pl/2009/01/13/subclass-and-override-vs-partial-mocking-vs-refactoring
- https://stackoverflow.com/questions/31413337/mockito-when-then-not-returning-expected-value
- Spy the whole object and then mock some methods in it.

## Bypassing strict stubbing

- https://www.baeldung.com/mockito-unnecessary-stubbing-exception
- https://stackoverflow.com/questions/42947613/how-to-resolve-unneccessary-stubbing-exception

- Case by case

```
Mockito.lenient().when(mockedService.getUserById(any())).thenReturn(new User());
```

- Bypass for every cases

```java
// junit5
@ExtendWith(MockitoExtension.class)
@MockitoSettings(strictness = Strictness.LENIENT)
class JUnit5MockitoTest {
}

// junit4
@RunWith(MockitoJUnitRunner.Silent.class)
```

## Mockito Annotations

- @Mock, @Spy, @Captor, @InjectMocks
    + https://howtodoinjava.com/mockito/mockito-annotations/
    + https://www.baeldung.com/mockito-annotations
- It will create a new object for each `@Test` to isolate tests.
