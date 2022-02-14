# Overview

- https://github.com/FasterXML/jackson
- https://www.baeldung.com/jackson
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
