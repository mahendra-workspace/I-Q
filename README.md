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

6. **What is Lazy loading And Eager Loading?**
   - In Lazy loading data is fetched on-demand. Associated data is not loaded until it is explicitly accessed.
   - Accessing lazy-loaded data after the session is closed can cause LazyInitializationException in frameworks like Hibernate. Can lead to the ```N+1 Select Problem``` if not carefully managed.
   - In Eager loading data is fetched immediately, along with the main entity. All associated data is loaded in a single query. The related data is fetched using joins or separate queries during the initial load.
   - For ```@OneToMany``` and ```@ManyToMany``` associations, the default fetch type is LAZY.
   - For ```@OneToOne``` and ```@ManyToOne``` associations, the default fetch type is EAGER.
    
7. **What is N+1 select problem?**
   - The N+1 Select Problem is a common performance issue that occurs in applications (especially when using ORM frameworks like Hibernate or JPA) when data is fetched lazily for a collection or relationship.
   - The initial query retrieves the primary data (1 query).
   - For each result of the primary data, lazy loading triggers a separate query to fetch the related data (N queries).
   - Use fetch joins to avoid it when you know you’ll need related data.
   - Use lazy loading by default but optimize it with ```@BatchSize``` or ```fetch joins``` as required.
     
8. **Explain Hibernet Caching.**
   - Caching in Hibernate is a mechanism that improves application performance by reducing the number of database interactions. It stores frequently accessed data in memory, allowing Hibernate to reuse the data without hitting the database again.
   - **First-Level Cache**
     - The first-level cache is associated with the Hibernate ```Session``` object. It is enabled by default and cannot be disabled.
     - It is specific to a particular session, meaning cached data is valid only within the lifecycle of that session.
     - ```
Session session = sessionFactory.openSession();
Transaction transaction = session.beginTransaction();

       ```
