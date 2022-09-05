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

# Tips and Tricks

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

## Spy vs. Mock

- https://stackoverflow.com/questions/28295625/mockito-spy-vs-mock
- Spy
    + Wrap around the real object and will call the underlined real
      methods
- Mock
    + A fake object and does not call the underlined real methods

## Mockito Annotations

- @Mock, @Spy, @Captor, @InjectMocks
    + https://howtodoinjava.com/mockito/mockito-annotations/
    + https://www.baeldung.com/mockito-annotations
- It will create a new object for each `@Test` to isolate tests.
