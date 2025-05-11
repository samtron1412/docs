# Overview

- https://en.wikipedia.org/wiki/Aspect-oriented_programming
- https://aravindvasu.dev/2019/introduction-to-aop/

# AspectJ

- AspectJ (Java implementation)
    + https://en.wikipedia.org/wiki/AspectJ
    + https://eclipse.dev/aspectj/doc/released/devguide/index.html
    + https://docs.spring.io/spring-framework/reference/core/aop/ataspectj/advice.html
    + Jars: https://mvnrepository.com/artifact/org.aspectj
        * `aspectjtools`: compiler (ajc), compile-time weaving
        * `aspectjweaver`: load time weaving
        * `aspectrt`: runtime library that is need to run Java programs
          enhanced by AspectJ
- Joinpoint vs. ProceedingJoinPoint
    + https://www.baeldung.com/aspectj-joinpoint-proceedingjoinpoint

## Examples

```java
 @Aspect
 public class GuiceInterceptor implements Interceptor {

     private static final Logger LOGGER = LogManager.getLogger(GuiceInterceptor.class);
     private static final Map<Class, Class> BINDING_REPLACEMENT_MAP = new ImmutableMap.Builder<Class, Class>()
             .put(RedisCache.class, NoCache.class)
             .build();

     @Override
     // The + sign mean that this will intercept `.to(Class)` calls
     // in any subclass of `ScopedBindingBuilder`
     @Around("call(* com.google.inject.binder.ScopedBindingBuilder+.to(java.lang.Class))")
     public Object intercept(ProceedingJoinPoint joinPoint) throws Throwable {
         final Class oldClass = (Class) joinPoint.getArgs()[0];
         final Class newClass = BINDING_REPLACEMENT_MAP.get(oldClass);

         if (newClass != null) {
             LOGGER.info("Replacing Guice binding to {} with {}", oldClass, newClass);
             return joinPoint.proceed(new Object[] {newClass});
         }
         return joinPoint.proceed();
     }
 }
```
