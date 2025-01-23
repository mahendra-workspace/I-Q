# JAVA

1. **What is the use of TRANSIENT keyword?**
   - The ```transient``` keyword is used in the context of serialization in Java. A transient variable is a variable that will not be serialized when an object is converted into a byte stream.
   - Typically applied to variables holding sensitive data, such as passwords, or data that can be derived/calculated at runtime and does not need to be persisted.
2. **What is the use of VOLATILE Keyword ?**
   - The volatile keyword is used in the context of multithreading in Java. A volatile variable is one whose value is always read from the main memory rather than from a thread's local cache.
   - Guarantees that updates to the variable by one thread are immediately visible to all other threads.
   - Used for variables that are shared across multiple threads, especially for flags or signals.

3. **What is covarient overriding ?**
   - In covarient overriding return type of an overriding method can be a subclass of the return type declared in the parent class. This is known as a covariant return type.
   - In method overriding, the overridden method in the child class can have a return type that is more specific (a subclass) than the return type of the method in the parent class.
   - The overriding method must follow all the rules of method overriding, Same name, Same parameter list, Return type must be either the same or covariant (a subclass of the parent return type).
  
4. **how to create your own bean life cycle?**
   - Using Core Java: Managing your own lifecycle without relying on a framework.
   - You can create and manage your own bean lifecycle by defining lifecycle methods like ```initialize``` and ```destroy```
   - Using ```@PostConstruct``` and ```@PreDestroy``` Annotations. These annotations are part of Jakarta EE (formerly Java EE) and are recognized by the Spring framework.
   - Implementing ```InitializingBean``` and ```DisposableBean``` Interfaces.

5. **what is differece between filter and intercepter?**
   - In Spring Boot, both filters and interceptors are mechanisms to process requests and responses.
   - Filters are part of the Servlet API and are used to process requests and responses at a low level, often for tasks like security, logging, or modifying the request/response.
   - Filters are invoked before the request reaches the controller and after the response leaves the controller.
   - Use Case of filters are authentication and authorization, Modifying request/response headers or payload.
   - Filter can create by implementing the ```javax.servlet.Filter``` interface or using ```@Component```.
   - Interceptors are part of Spring's HandlerInterceptor API and are used to perform operations before and after the execution of a controller handler method.
   - Interceptors operate at the Spring MVC level and can access handler objects and model attributes.
   - Interceptors are invoked after filters but before the controller method and can be used to preprocess and postprocess controller logic.
   - Use Case of Interceptor are validating user input, handling cross-cutting concerns like logging, session tracking, or security at the Spring MVC level.
   - Interceptors can be created by implementing the ```HandlerInterceptor``` interface or extending ```HandlerInterceptorAdapter```.

    
