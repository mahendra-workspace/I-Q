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
     - **System ClassLoader (Application ClassLoader)**
       - Loads classes from the application's classpath (e.g., the CLASSPATH environment variable or JAR files specified at runtime).
       - Delegates to the Extension ClassLoader.
       - This is the default class loader for most user-defined classes.
     - **Custom ClassLoaders**
       - Developers can define their own class loaders by extending the ```ClassLoader```
       - Useful for Dynamically loading classes from non-standard sources (e.g., network, database).
11. **Difference b/w JAR and WAR files and how to deploy**
    - **JAR**
      - Used to package Java applications (standalone or libraries).
      - Contains compiled ```.class``` files, resources (e.g., properties), and metadata in ```META-INF/MANIFEST.MF```.
      - Deployed to systems with a JVM, typically for standalone applications or librarie.
      - Can be executed directly if it contains a ```main()``` method. Example: ```java -jar MyApp.jar```.
      - Flat structure with compiled classes and resources in the root directory.
    - **WAR**
      - Used to package web applications (Java-based, adhering to the servlet/JSP specification).
      - Includes all components of a web app: servlets, JSPs, HTML, CSS, JS, and web.xml (in WEB-INF).
      - Deployed to a Java web server or container like Apache Tomcat, Jetty, or WildFly.
      - Cannot be executed directly; requires deployment in a server/container.
      - Hierarchical structure with WEB-INF/ folder for classes, web.xml, and other server-side components.
12. **Idempotent Methods in REST API**
    - In REST APIs, idempotent methods are HTTP methods where making multiple identical requests has the same effect as making a single request.
    - These methods ensure that repeating the request does not produce different results or side effects beyond the first execution.
    - **GET**
      -  Retrieves data from the server.
      -  Multiple GET requests do not change the server state or data.
    - **PUT**
      - Updates or replaces an existing resource or creates a new one if it doesn't exist.
      - Repeated PUT requests with the same payload result in the resource being in the same state.
    - **DELETE**
      - Repeated DELETE requests on the same resource have the same effect (i.e., the resource is removed).
      - Once deleted, subsequent DELETE requests should not cause additional side effects.
    - **HEAD**
      -  Similar to GET but retrieves only headers (no response body).
    - **OPTIONS**
      - Retrieves available HTTP methods for a resource.
13. **diffrence between get and load methods**
    - In Hibernate, the get() and load() methods are used to retrieve an object from the database.
    - While both are part of the ```Session``` interface.
    - **```get()``` Method**
      - Retrieves the object immediately from the database.
      - Use when you are not sure if the object exists (returns ```null``` if not found).
      - Always hits the database at the time of method call.
      - Returns the actual object instance directly.
      - Works inside and outside a transactional context.
    - **```load()``` Method**
      - Returns a proxy object immediately, fetching data only when accessed (lazy loading).
      - Use when you are sure the object exists (throws an exception if not found).```org.hibernate.ObjectNotFoundException```
      - Returns a proxy object unless the object is accessed.
      - Returns a proxy object unless the object is accessed.
      - Works properly only in a transactional context (to resolve proxies).
 14. **What is Spring Boot?**
     - Spring Boot is an extension of the Spring Framework that simplifies the development of stand-alone, production-grade Spring-based applications.
     - It provides auto-configuration, embedded servers (like Tomcat), and opinionated defaults to reduce boilerplate code and speed up development.
     - Ideal for building REST APIs, microservices, and web applications.
     - **Key Features of Spring Boot**
       - Auto-Configuration: Automatically configures your application based on the dependencies you add.
       - Standalone: No need for external servers; it comes with embedded servers like Tomcat, Jetty, or Undertow.
       - Production-Ready: Includes features like actuator for monitoring and managing your app in production.
       - Spring Ecosystem Integration: Works seamlessly with other Spring projects like Spring Data, Spring Security, and Spring Cloud.
     - **Bean Related annotation**
       - **```@Component```**
         - It indicates that an annotated class is a spring bean/component. It also tell spring container to automatically create spring bean and Ioc container automatically manage this process.
         - By default bean name is same as class name but first latter of class name is small latter. we can specify name using ```@Component("beanName")```
         - Ioc implement annotation based configuraion.(No need for ```New``` keyword)
           
       - **```@Autowired```**
         - The @Autowired annotation in Spring and Spring Boot is used for dependency injection. It allows Spring to automatically inject beans (dependencies) into your class, eliminating the need for manual configuration or instantiation.
         - It is used in contructor injection, setter injection and field injection.
         - Spring scans the application context for a matching bean (based on type or name) and injects it into the annotated field, constructor, or method. If no matching bean is found, Spring throws a ```NoSuchBeanDefinitionException```.
         - Use ```@Autowired(required = false)``` to make the dependency optional. If no matching bean is found, Spring will not throw an exception.
         - Ioc implement annotation based configuraion.(No need for ```New``` keyword)
         
       - **```@Qualifier```**
         - It is used in conjunction with Autowired to avoid confusion when we have two or more beans configured for same type.
         - it require bean nama eg. ```@Qualifier("vegPizza")```
         - Ioc implement annotation based configuraion.(No need for ```New``` keyword)
           
       - **```@Primary```**
         - It is used to give higher preference to a bean when there are multiple beans of the same type.
         - it is a class level annotation and used with ```@Component``` annotation.
         - Ioc implement annotation based configuraion.(No need for ```New``` keyword)
           
       - **```@Bean```**
         - It indicates that a method produces a bean to be managed by the spring container.
         - It usually declared in Configuration class to create a spring bean definations.
         - By default bean is same as method name . we can specify bean name using @Bean(name="beanName")
         - It provides ```initMethod``` and ```distroyMethod``` attributes to perform certain actions before bean initialization or bean bean destruction by a container. eg. ```@Bean(initMethod="init", destroyMethod="destroy")```
         - It is a java based configuration(it need ```New``` keyword).
        
       - **Stereotype annotations**
         - These annotations are used to create spring beans automatically in the application context(Spring IoC container)
         - The main sterotype annotation is ```@Component```
         - By using this annotation, Spring provides more stereotype meta annotations such as @Service, @Repository, @Controller
         - @Service annotation is used to create spring beans at the service layer.
         - @Repository is used to create spring beans for the repositories at the DAO layer.
         - @Controller is used to create Spring beans at the controller layed.
       - **```@Lazy```**
         - By default, Spring creates all singleton beans eagerly at the startup of application context.
         - We can load the spring beans lazily(on-demand) using @Lazy annotation.
         - @Lazy annotation can be used with @Configuration, @Component and @Bean annotations.
         - Eager Initialization is recommended to avoid and detect all possible errors immediately at the time of starting the server rather then runtime.
       - **```@Scope```**
         - Spring framwork defines 6 types of scopes such as
           - singleton: Only one instance of bean is created and shared across the entire application. This is default scope. Eg ```@Scope(value=ConfigurableBeanfactory.SCOPE_SINGLETON)``` 
           - prototype: A new instance of the bean is created every time it is requested. eg. ```@Scope(value=ConfigurableBeanfactory.SCOPE_PROTOTYPE)```
           - request
           - session
           - application
           - websocket
         - It is used to define a scope of the bean.
         - We use @Scope to define the scope of a @Component class or a @Bean definition.
 15. **Flow Of Spring Boot**
     - **Application Initialization:**
       - When we run a Spring Boot application, it starts by initializing the Spring Application Context. This is the core container that manages the lifecycle of beans and their dependencies.
     - **Auto-Configuration:**
       - Spring Boot uses auto-configuration to automatically configure application based on the dependencies we have added. For example, if we include ```spring-boot-starter-web```, Spring Boot will automatically configure an embedded Tomcat server and set up Spring MVC.
     - **Component Scanning:**
       - Spring Boot scans application for components (like ```@Component```, ```@Service```, ```@Repository```, ```@Controller```, etc.) and registers them as beans in the Spring Application Context.
     - **Dependency Injection:**
       - Once the beans are registered, Spring Boot injects the dependencies into the beans using the Inversion of Control (IoC) principle.
     - **Application Execution:**
       - After the context is initialized and all beans are wired together, the application is ready to handle requests (in the case of a web application) or execute the business logic.
     - **Shutdown:**
       - When the application is shut down, the Spring Application Context is closed, and all beans are destroyed in an orderly manner.
 16. **Inversion of Control (IoC)**
     - Inversion of Control (IoC) is a design principle in which the control of object creation, configuration, and lifecycle is transferred from the application code to a framework or container. In the context of Spring, the IoC container is responsible for managing the lifecycle of objects (beans) and their dependencies.
     - In traditional programming, the flow of control is determined by the application code. For example, if a class A needs an instance of class B, the developer explicitly creates an instance of B and passes it to A. This approach tightly couples the classes and makes the code harder to maintain and test.
     - **How IoC Manages Everything**
       - **Bean Definition:**
         - Beans are defined using annotations like @Component, @Service, @Repository, @Controller, or XML configuration. These definitions tell the IoC container what beans to manage.
       - **Bean Instantiation:**
         - The IoC container creates instances of the beans based on their definitions. This is done either at application startup or when the bean is first requested (lazy initialization).
       - **Dependency Injection:**
         - The IoC container injects the dependencies into the beans. This can be done via constructor injection, setter injection, or field injection.
       - **Lifecycle Management:**
         - The IoC container manages the lifecycle of beans, including initialization (via ```@PostConstruct``` or ```InitializingBean```) and destruction (via ```@PreDestroy``` or ```DisposableBean```).
       - **Configuration Management:**
         - The IoC container reads configuration properties (from ```application.properties``` or ```application.yml```) and injects them into beans using ```@Value``` or ```@ConfigurationProperties```.
      
 17. **Tight Coupling & Loose Coupling**
     - **Tight Coupling:**
       - Tight coupling occurs when two or more components are highly dependent on each other. Changes in one component often require changes in the other, making the system rigid and harder to maintain.
       - For example, if ClassA directly creates an instance of ClassB, it is tightly coupled to ClassB.
       - ```
         class Engine {
             public void start() {
                 System.out.println("Engine started.");
             }
         }
         class Car {
             private Engine engine;
             public Car() {
                 this.engine = new Engine(); // Tight coupling: Car directly creates an instance of Engine
             }
             public void start() {
                 engine.start();
             }
         }
         ```
     - **Loose Coupling:**
       - Loose coupling occurs when components are independent of each other and interact through well-defined interfaces or abstractions. Changes in one component have minimal or no impact on other components.
       - ```
         interface Engine {
             void start();
         }

         class PetrolEngine implements Engine {
             @Override
             public void start() {
                 System.out.println("Petrol Engine started.");
             }
         }
         class Car {
             private Engine engine;
             public Car(Engine engine) { // Loose coupling: Car depends on the Engine interface
                 this.engine = engine;
             }
             public void start() {
                 engine.start();
             }
         }
         ```
       - **How to Achieve Loose Coupling**
         - Use Interfaces or Abstract Classes: Depend on abstractions rather than concrete implementations.
         - Apply Dependency Injection (DI): Let a framework (like Spring) inject dependencies rather than creating them directly. For example using ```@Autowired``` annotation
      
 18. **What is Logging?**
     - Logging is the process of recording events, messages, and errors that occur during the execution of an application.
     - These logs help developers and system administrators monitor the application, debug issues, and analyze performance.
     - Spring Boot uses ```SLF4J (Simple Logging Facade for Java)``` as the logging abstraction and Logback as the default logging implementation.
     - You can configure logging in the ```application.properties``` or ```application.yml``` file.
    
 19. **What is Swagger?**
     - Swagger is a tool for designing, building, and documenting RESTful APIs.
     - Swagger automatically generates and maintains up-to-date API documentation, reducing the need for manual documentation.
     - Allows developers to test API endpoints directly from the documentation.
     - Swagger UI allows developers to test APIs without using external tools like Postman.
     - To use Swagger in Spring Boot, you need to add the Springfox or Springdoc OpenAPI dependency. Springdoc OpenAPI is the newer and more actively maintained library.
     - 
