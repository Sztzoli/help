# Udemy-Spring Framwork 5

## 02 Building Spring Boot Web App

`mvn sprin-boot:run` terminálból igy is lehet elindítani a spring-boot projektet



h2 console:

application.properties-be

```
spring.h2.console.enabled=true
```

akkor a http://localhost:8080/h2-console/ megjelenik a böngészőben

```
spring.datasource.url=jdbc:h2:mem:testdb
```

mindenképp érdemes hozzá adni mert különben a spring-boot logból kel kinézni mindig amit generált



@Manytomany

```java
@ManyToMany
@JoinTable(name = "author_book",
        joinColumns = @JoinColumn(name = "book_id"),
        inverseJoinColumns = @JoinColumn(name = "author_id"))
private Set<Author> authors = new HashSet<>();
```

```java
@ManyToMany(mappedBy = "authors")
private Set<Book> books = new HashSet<>();
```

egy közös tábla lesz



thyleafe

```html
<html lang="en" xmlns:th="http://www.thymeleaf.org">
```

```html
<tr th:each="book : ${books}">
    <td th:text="${book.id}" >123</td>
    <td th:text="${book.title}">Spring in Action</td>
    <td th:text="${book.publisher.name}">Wrox</td>       
</tr>
```

táblázatot generál



## Dependency Injection

konstruktor injektionnál nem tudjuk kikerülni hogy implementáljuk az osztályt

konstruktor injektionnál müködik @autowired nélkül is 

 `ls -Force` powershell kilistáza a rejtettfájlokat is

**@Qualifier**

konstruktor 

```java
public ConstructorInjectedController(@Qualifier("constructorGreetingService") GreetingService greetingService) {
    this.greetingService = greetingService;
}
```

setter

```java
@Qualifier("setterInjectionGreetingService")
@Autowired
public void setGreetingService(GreetingService greetingService) {
    this.greetingService = greetingService;
}
```

property

```java
@Qualifier("propertyInjectionGreetingService")
@Autowired
public GreetingService greetingService;
```

**Primary Bean**

```java
@Primary
@Service
public class PrimaryGreetingService implements GreetingService{
```

ez lesz az alapértelmezett bean a Greetingservice-nél a @Qualikier felül írja

**Profile**



```java
@Profile("EN")
@Service("i18nService")
public class I18nEnglishService implements GreetingService{
```

```java
@Profile("ES")
@Service("i18nService")
public class I18nSpanishService implements GreetingService{
```

```java
public I18nController(@Qualifier("i18nService") GreetingService greetingService) {
    this.greetingService = greetingService;
}
```

igy még konfikt lesz mifel 2 sevice van egy néven

a application.propeties-be

```
spring.profiles.active=EN
```

```java
@Profile({"ES", "default"})
@Service("i18nService")
public class I18nSpanishService implements GreetingService{
```

default profile, ez lesz az alapértelmezett ha nincs active profile

## Spring Configuration

Spring Framework Stereotypes:

@Component

@Controller,@service, @Repository

@RestController: Controller és @ResponseBody

Component Scan:

Spring commpoment scannel lesznek ezek a beans megtalálva

Springboot aotuconfiguration scaneli a main packaget és a sub classokat

ha kicül esik akkor package scan

```java
@ComponentScan(basePackages = {"guru.springframework.didemo","com.springframework.pets"})
```

## External Properties

Property rangsor:

* java system propeties
* JNDI
* SPRING_APPLICATION_JSON
* comnand line arguments
* Test Properties (for testing)

Propertires source:

```java
@PropertySource("classpath:datasource.properties")
@Configuration
public class GreetingServiceConfig {


    @Bean
    FakeDataSource fakeDataSource(@Value("${guru.username}")  String username,
                                  @Value("${guru.password}") String password,
                                  @Value("${guru.jdbcurl}") String jdbcurl) {
        FakeDataSource fakeDataSource = new FakeDataSource();
        fakeDataSource.setUserName(username);
        fakeDataSource.setPassword(password);
        fakeDataSource.setPassword(jdbcurl);
        return fakeDataSource;
    }
```

```properties
guru.username=superuser
guru.password=dbPassword
guru.jdbcurl=someUrlforDB
```

envirenment variable: GURU_USERNAME=UserFromEnvVar!

Program arguments:

--guru.password=PasFromCommandLine
--guru.username=UserFromCommandLine



Spring bootnál a properties a application.propertiesbe kerül és igy nem kell a @PropertySource



Springboot profile:

application-dev.properties

application-qa.properties



Properties binding

```java
@ConfigurationProperties("guru")
@Configuration
@Getter
@Setter
public class SFGConfiguration {

    private String userName;
    private String password;
    private String jdbcurl;
}
```

Constructor Binding:



```java
@ConstructorBinding
@ConfigurationProperties("guru")
```

és a főConfigosztályra

```java
@EnableConfigurationProperties(SfgConstractorConfig.class)
```



## Spring MVC



### Thyemleaf



```html
<html lang="en" xmlns:th="http://www.thymeleaf.org">
```

```html
<tr th:each="book : ${books}">
    <td th:text="${book.id}" >123</td>
    <td th:text="${book.title}">Spring in Action</td>
    <td th:text="${book.publisher.name}">Wrox</td>       
</tr>
```

táblázatot generál

```html
<div class="card-body">
    <div class="table-responsive" th:if="#{lists.isEmpty(recipes)}">
        <table class="table table-hover">
            <thead class="thead-inverse">
            <tr>
                <th>ID</th>
                <th>Description</th>
            </tr>
            </thead>
            <tr th:remove="all">
                <td th:text="${recipe.id}">1234</td>
                <td th:text="${recipe.description}">Tasty</td>
            </tr>
            <tr th:remove="all">
                <td th:text="${recipe.id}">1235</td>
                <td th:text="${recipe.description}">Tasty</td>
            </tr>
            <tr th:each="recipe : ${recipes}">
                <td th:text="${recipe.id}">1236</td>
                <td th:text="${recipe.description}">Tasty</td>
            </tr>
        </table>
    </div>
</div>
```

th:if ha üres a lista

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet"
      integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous"
th:href="@{/webjars/bootstrap/5.0.1/css/bootstrap.min.css}">

<script src="/webjars/jquery/3.6.0/jquery.min.js"></script>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4" crossorigin="anonymous"
th:src="@{/webjars/bootstrap/5.0.1/js/bootstrap.min.js}"></script>
```

th:href kicseréli a css, th:src meg a scriptet



### HTTP protocol



```
wro4j-maven-plugin
```

https://wro4j.readthedocs.io/en/stable/MavenPlugin/



###  i18n

```
#I18n
spring.messages.basename=messages/messages
```



## JPA

* @OneToOne
  * 1 entitás egy másik entitással áll kapcsolatban
* @OneToMany
  * 1 egy entitás tartozik list set map
* @ManyToOne
  * inverz kapcsolata a One To Manynek 
* @ManyToMany
  * many kapcsolodik manyhez
  * mindegyiknek lest vagy set referenciája van a másikra
  * join table használunk h leírjuk ezt a kapcsolatot  



* Egyirányú kapcsolat 
  * mapping egy irányból van csak a másik oldal nem tud a másikról
* Kétirányú kapcsolat
  * mindkét oldal tud egymásról
  * Javasolt ezt használni, mert igy objekt gráfon mindkét irányba mehetünk  

### Owning Side

* Owning side fog ja tartalmazni a foreign key az adatbázisban
* One to One az a oldal ahol a foreign key meghatározott
* OneToMany és ManytoOne a many oldal
* "mappedBy" hatérozuk meg az a oldalt meg "Owns" a referenciát a kapcsolatnak

### Fetch Type

* Lazy Fetch Type - data nincs addig lekérdezve mig nem hivatkoznak rá
* Eager Fetch Type - data alapból le van kérdezve
  * OneToMany - Lazy
  * ManyToOne- Eager
  * ManyToMany- Lazy
  * OneToOne- Eager

### JPA Cascade Types

- controllája a állapot változtatásokat a szülőtől és gyerek objectig
  * PERSIST - save utasítás végig megy a kapcsolodó entitásokon
  * MERGE - kapcsolodó entitások merge amikor a owning entitás merge-ve lesz
  * REFRESH - kapcsolódő entitások frissülnek ha a owning entitás frissül
  * REMOVE - eltávolítja az kapcsolodó entitásokat mikot eltávolítjuk a owning entitást
  * DETACH - detach az összes entitást amikor a manuális detach történik
  * ALL - összes egyszerre
- Allapértelmezetten nincs cascade

### Create és Update Timestamps

* jó gyakorlat ha használjuk ezeket a entitásokon audit okán
* JPA támogatja: @PrePersist és a @PreUpdate
* Hibernate: @CreationTimestamp és @UpdateTimestamps



### Hibernate DDL Auto

* DDL = Data Definition Language
  * DML = Data Manipulation Language
* Hibernate property-e spring property-vel lehet beállítani
  * spring.jpa.hibernate.ddl-auto
* Opciok: none, validate, update, create, create-drop
* Spring Boot create-drop használ beágyazott adatbázisoknál (hsql,h2,derby) vagy semmit

### Initialize Hibernate-vel

* Data betölthető import.sql-ből
  * Hibernate tulajdonság (nem Spring specifikus)
  * gyökérkönyvtárban kell lennie
  * akkor hajtódik végre csak mikor a ddl-auto create vagy create-drop van beállítva

### Spring JDBC

* Spring Boot schema.sql és data.sql tölti be, gyökérkönyvtárból
* Spring Boot betölti a shema-${platform}.sql és a data-${platfrom}.sql
  * be kell állítani spring.datasource.platfrom
* Zavart okozhat a Hibernate DDL auto property-e
  * érdemes none-ra vagy validate-re állítani



## Project Lombok

## Testing Spring FrameWork Application

### JUnit 4 annotations

* @Test
* @Before - minden test elött végre hajtodik(read input data, initialize class)
* @After - Minden teszt után végre hajtodik. vlean up test envireoment. save memory
* @BeforeClass - Egyszer hajtodik csak végre staticusnak kell lennie hogy müködjön
* @AfterClass - A legvégén hajtodik végre statikusnak kell lennie h müködjön
* @ignore - Test-et disable-é teszi
* @Test(excepted = Exception.class) - Fails ha nem dobja a megnevezet exception
* @Test(timeout = 10) Fails ha a method hosszab mint 100 millisecond



### Spring Boot annotations

* @RunWith(SpringRunner.class) - Run test with Spring Context
* @SpringBootTest - Search for Spring Bott Application for configuration
* @TestConfiguration - Sperify a Spring configuration for your test
* @MockBean - Injektálja Mockito Mock
* @SpyBean - Injekt mokito Spy
* @JsonTest - Készit a Jackson or Gson object mapper via SpringBoot
* @WebMvcTest - http server nélkül tsztelünk web context
* @DataJpaTest - Used to test Data layer with embedded database
* @JdbcTest - like DatajpaTest nincs configuráva az entity manager
* @DataMongoTest - Configures an embedded MongoDB for testin
* @RestClientTest - creat mock server for testing rest client
* @AutoConfigurationRestDock - Allow you to use Spring Rest Docs in test, creating API documentation
* @BootStrapWith - Used to configure how the testContext is bootstrapped
* @ContextHierarchy - Allow you create a context hierarchy with @ContextConfiguration
* @ActiveProfiles - Set witch Spring Profiles are active for the test
* @TestProperySource - Configure the property source for the tese
* @DirtiesContext - Resets to Spring Context after the test (Expensive to do)
* @WebAppConfiguration -Indicates Spring should use a Web Application context
* @TestExecutionListeners - Allow you to specify listeners for testing events
* @Transactional - Run test in transaction, roolback when complete be default
* @BeforeTransaction - Action to run before transaction
* @AfterTransaction - Action to run after transaction
* @Commit - Specifies the transaction shoul be commited after the test.
* @Rollback - Transaction shoud be rolled back after test (Default action)
* @Sql - Specify SQL script to run before 
* @SqlConfig - Define meta data fir SQL scripts
* @SqlGroup - Group of @Sql annotations
* @Repeat - Repeat test x number times
* @Timed - Similar to JUnit timeout, de itt megvárja hogy tesz végig fusson
* @IfProfileValue - Indicates test is eneable for a specific testing enviroment
* @ProfileValueSourceConfiguration - Specify a profile value source

### JUnit5

* @Test(excepted = Exception.class) -> assertThrows
* @Test(timeout = 10) -> assertTimeout
* @RunWith(SpringRunner.class) -> @ExtendWith(SpringExtension.class)
* @Before -> @BeforeEach
* @After -> @AfterEach
* @BeforeClass -> @BeforeAll 
* @AfterClass -> @AfterAll 
* @Ignore -> @Disable
* @Category -> @Tag



## Crud operation with Spring MVC

Command object are Data Transfer Object (DTO) in MVC.

DTO is a pattern where an object is used to encapsulate data, and send it from one subsystem of an application to another.

DTOs are most commonly used by the Services layer in an N-Tier application to transfer data between itself and the UI layer. The main benefit here is that it reduces the amount of data that needs to be sent across the wire in distributed applications.

Now consider a CreditCard entity that represents a credit card. We won't send the CreditCard entity to the front end - it contains whole lot of sensitive data. Our frontend only needs to display to user their registered credit cards as:

Credit Card Number: XXXXXXXXXXXXX345

Credit Card Type: Visa

So we create a CreditCardCommand with only two fields. creditCardNumber and creditCardType.

Now someone need to convert the CreditCard entity to CreditCardCommand and vice versa. The converter does that.

Although this might not be the perfect use case, but I hope you got the thing.



From Spring point of view taken *from Spring Documentation:*

Command Object is a JavaBean which will be populated with the data from your forms

Think of Command Object as a POJO/JavaBean/etc.. that backs the form in your presentation layer.

Once the form is submitted, all the individual attributes are mapped/bound to this object. On the way up to presentation, Command Object properties may be used to pre/populate the form.

