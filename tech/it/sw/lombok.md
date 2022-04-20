# Overview

- https://projectlombok.org/
- Using annotations to simplify code by generating boiler-plate code
  automatically

# val

- local final variables (not on fields)

# var

- local non-final variables (not on fields)
- NOTE: SHOULD USE JAVA 10 `VAR` INSTEAD !!!
    + https://openjdk.java.net/projects/amber/guides/lvti-faq

# @NonNull

- `Use on fields`: Lombok will generate null checks if Lombok generates an
  entire method or constructor for you, e.g., via `@Data`
- `Use for parameters of a method or constructor`: Lombok will generate a
  null check at the top of that method.

# @Getter, @Setter

- Use on fields: to generate getters and setters for those fields

# @ToString

- Use on class definition: to generate `toString()` method

# @EqualsAndHashCode

- Use on class definition to generate `equals(Object other)` and
  `hashCode()` methods

# @NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor

- Generates constructors that take no arguments, one argument per
  final/non-nullfield, or one argumetn for eveyr field.

# @Data

- A shortcut for `@ToString`, `@EqualsAndHashCode`, `@Getter` on all
  non-final fields, `@Setter` on all fields, and
  `@RequiredArgsConstructor`

# @Value

- In practice, `@Value` is shorthand for:
    + `final @ToString @EqualsAndHashCode @AllArgsConstructor @FieldDefaults(makeFinal = true, level = AccessLevel.PRIVATE) @Getter`
    +  except that explicitly including an implementation of any of the
      relevant methods simply means that part won't be generated and no
      warning will be emitted.

# @Builder
