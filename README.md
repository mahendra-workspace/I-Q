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
       Author author1 = session.get(Author.class, 1L);
       
       ```
   - **Second-Level Cache**
     - The second-level cache is associated with the Hibernate ```SessionFactory```. It allows entities, collections, or queries to be cached across sessions.
     - It is shared across multiple sessions and can store data beyond the lifecycle of a single session.
     - When enabled, Hibernate checks the second-level cache for the required data before querying the database. If the data is present in the cache, it is retrieved directly.
     - For enabling it we need to add Maven Dependency (e.g., EhCache or Caffeine) and need configuration in properties file and also need to write ```@cache(usage = CacheConcurrencyStrategy.READ_WRITE)``` in entity.
     - ```
       hibernate.cache.use_second_level_cache=true
       hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory
       hibernate.cache.use_query_cache=true
       ```
      - ```
        @Entity
        @Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
        public class Author {
        }
        ```
   - **Common Caching Providers**
     - EhCache: Popular and widely used caching provider for Hibernate.
     - Caffeine: A high-performance caching library.
     - Infinispan: Advanced distributed caching solution.
     - Redis: In-memory data structure store, commonly used for distributed caching.   

 9. **BeanFactory and ApplicationContext**
     - BeanFactory and ApplicationContext are two core interfaces in the Spring framework for managing beans. Both are part of the Spring IoC (Inversion of Control) container
     - **BeanFactory**
       - The BeanFactory is the basic and simplest container in Spring. It provides the foundational functionality for managing and instantiating beans.
       - Lazy Initialization: Beans are created only when they are requested (on-demand).
       - Provides basic features like instantiating and wiring beans.
       - Does not provide advanced features such as event publishing, internationalization, or annotation-based configuration.
       - **ApplicationContext**
         - The ApplicationContext is a more advanced container that extends the BeanFactory and adds extra features for enterprise-level applications.
         - Eager Initialization: By default, it instantiates all singleton beans during startup for better performance in the long run.         
         - Internationalization: Supports i18n (messages and resources in different languages). 
         - Annotation Processing: Fully supports annotations like @Autowired, @Component, @Value, etc.        

 10. **ClassLoader and Its types**
     - In Java, a ClassLoader is a part of the Java Runtime Environment (JRE) responsible for dynamically loading Java classes into the Java Virtual Machine (JVM). ClassLoaders handle the task of locating, loading, and linking class files (.class) during runtime. Without class loaders, the JVM cannot execute Java applications.
     - **Responsibity**
       - Locating and reading the bytecode of a class (from files or other sources) and converting it into a Class object.
       - Allocates memory for class variables and initializes them to default values.
       - Executes the static initializers and static blocks in the class.
     - **Bootstrap ClassLoader:**
       - Parent of all ClassLoaders.
       - It is written in native code and part of the JVM itself.
       - Loads the core Java classes (e.g., classes from java.lang and java.util packages).
     - **Extension ClassLoader (Platform ClassLoader from Java 9)**
       - Loads classes from the Java extensions directory ($JAVA_HOME/lib/ext).
       - It is implemented in Java and delegates to the Bootstrap ClassLoader.  
     - ** System ClassLoader (Application ClassLoader)**
       - Loads classes from the application's classpath (e.g., the CLASSPATH environment variable or JAR files specified at runtime).
       - Delegates to the Extension ClassLoader.
       - This is the default class loader for most user-defined classes.
     - **Custom ClassLoaders**
       - Developers can define their own class loaders by extending the ```ClassLoader```
       - Useful for Dynamically loading classes from non-standard sources (e.g., network, database).
