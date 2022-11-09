# Overview

- https://github.com/FasterXML/jackson
    + https://stackoverflow.com/questions/6846244/jackson-and-generic-type-reference
- https://www.baeldung.com/jackson
    + https://www.baeldung.com/jackson-map
- Jackson is a suite of data-processing tools for Java (and the JVM
  platform)
    + Jackson has been known as "the Java JSON library"
- Under Jackson project
    + 3 core packages: streaming, databind, annotations
    + data format libraries
    + data type libraries

# ObjectMapper

## Java Object to JSON

```java
ObjectMapper objMapper = new ObjectMapper();
Car car = new Car("yellow", "Acura");
objMapper.writeValue(new File("target/car.json"), car);
```

## JSON to Java Object

```java
String json = "...";
Car car = objMapper.readValue(json, Car.class);

// an URL

Car car = objMapper.readValue(new URL("..."), Car.class);
```

# Java8 Modules

- You need to register some Jackson modules to support Java8
- https://github.com/FasterXML/jackson-modules-java8
- https://stackoverflow.com/questions/27952472/serialize-deserialize-java-8-java-time-with-jackson-json-mapper

```java
// Up to Jackson 2.9: (but not with 3.0)
ObjectMapper mapper = new ObjectMapper()
   .registerModule(new ParameterNamesModule())
   .registerModule(new Jdk8Module())
   .registerModule(new JavaTimeModule()); // new module, NOT JSR310Module

// with 3.0 (or with 2.10 as alternative)
ObjectMapper mapper = JsonMapper.builder() // or different mapper for other format
   .addModule(new ParameterNamesModule())
   .addModule(new Jdk8Module())
   .addModule(new JavaTimeModule())
   // and possibly other configuration, modules, then:
   .build();

// Alternatively, you can also auto-discover these modules
ObjectMapper mapper = new ObjectMapper();
mapper.findAndRegisterModules();
```
