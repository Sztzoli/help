# Java Spring Boot Microservices

## Bevezetés

### Bevezetés a Spring Framework és Spring Boot használatába

A **Spring Framework** egy keretrendszer nagyvállalati alkalmazások fejlesztésére. Keretrendszer azért, mert az általunk írt komponenseket ő maga hozza létre, azaz példányosítja az általunk írt osztályokat. Ezt úgy is szokás mondani, hogy keretrendszer az, amely az általunk írt komponensek életciklusát vezérli.

Nagyvállalati alkalmazásnak azokat az alkalmazásokat nevezzük a Java világában, amelyek számára nem elegendőek a *Java Standard Edition*-be beépített tulajdonságok, hanem valamilyen további tulajdonságokra van szükség. A Spring Framework bizonyos problémákra saját megoldást biztosít, de ez a ritkább, mert a legtöbb esetre már létező third party library-ket integrál egy egységes modellbe.

Felmerülő igények, problémák egy nagyvállalati alkalmazás fejlesztése esetén, amelyek a Java SE-ben nem, vagy csak túl nagy munka árán megvalósíthatóak:

- A komponenseket nem a programozónak kell példányosítania és figyelni az életciklusukat, hanem a keretrendszer ezt elvégzi helyette.
- Fontos a távoli elérés másik számítógépről, interneten keresztül, sokszor böngészőből.
- Elvárás, hogy a keretrendszer maga biztosítsa a többszálúságot, és ne a programozónak kelljen azzal foglalkoznia, hogy hogyan tudja az alkalmazást egyszerre több felhasználó is párhuzamosan használni. Vagyis a programozó programozhasson úgy, mintha az alkalmazásnak csak egy felhasználója lenne, a többit pedig a keretrendszer oldja meg helyette.
- A perzisztencia problémakörének kezeléséhez a Java SE-ben csak a JDBC található, amely már elavult technológia. Egyrészt nagyon sokat kódot kell írni, hogy adatbázist tudjunk kezelni vele (“bőbeszédű”), másrészt gyakorlatilag minden egyes metódushívásnál foglalkozni kell a kötelezően kezelendő `SQLException` kivételel (*checked exception*).
- Fontos a tranzakciókezelés, hogy tudjunk atomi műveleteket definiálni. Fontos továbbá az elosztott tranzakciókezelés, ahol vannak olyan műveletek, amelyek egyszerre két erőforrással is dolgoznak. Ilyenek például a két adatbázison átívelő tranzakciók, amikor az egyik műveletet az egyik, másik műveletet a második adatbázisban kell elvégezni.
- Elvárás az aszinkron üzenetküldés, tipikusan valamilyen *message oriented middleware* használata, azaz hogy egy alkalmazás üzeneteket tudjon küldeni egy másik alkalmazás számára. Azért aszinkron, mert nem várja meg a választ, hanem *“send-and-forget”* modellben működik.
- Fontos az ütemezés (*scheduling*), hogy bizonyos műveletek valamilyen időközönként fussanak le automatikusan, és ne kelljen ehhez felhasználói beavatkozás.
- Egy nagyvállalati alkalmazás tipikusan nem önmagában létezik, hanem más alkalmazásokhoz kell integrálódnia. Egy keretrendszernek kell tudnia támogatni az integráció bizonyos módjait, azaz az alkalmazások közötti kommunikációt.
- Elvárás az auditálhatóság, hogy vissza lehessen nézni, hogy ki, mikor, milyen műveletet hajtott végre az alkalmazáson belül.
- Fontos a konfigurálhatóság, azaz hogy az alkalmazás több különböző környezetben is tudjon futni (tesztkörnyezet, éles környezet, stb.), és ezekhez különböző beállításokat lehessen megadni.
- Az alkalmazás üzemeltethető legyen, vagyis igény az, hogy az alkalmazás naplózható, monitorozható legyen, valamint hogy az üzemeltetők be is tudjanak avatkozni, ha erre van szükség.
- Fontos a biztonság, az autentikáció és az autorizáció, vagyis hogy valamilyen módon be lehessen jelentkezni, illetve hogy a felhasználók csak a nekik rendelt szerepkörök alapján tudjanak műveleteket végezni.
- Az alkalmazást le lehessen fedni automatizált tesztekkel, ezáltal csökkentve a hibák számát. A tesztelhetőség által az alkalmazás architektúrája is könnyebben megérthetővé, áttekinthetővé tud válni.

A Spring Framework ahhoz, hogy ezeket a nagyvállalati igényeket kielégítse, a következő tulajdonságokkal rendelkezik:

- A fejlesztőnek a Spring Frameworkben egyszerű Java objektumokat kell implementálnia (*POJO – Plain Old Java Object*), ezek a komponensek. A komponensek a konténer felügyelete alatt állnak, az vezérli az életciklusukat, az példányosítja le őket, és az is engedi el a referenciát akkor, amikor már nincs rá szükség. A konténer neve a Spring Frameworkben **application context**.
- A komponensek nem önmagukban léteznek, hanem közöttük kapcsolatok vannak, ezeket is a konténer felügyeli. A Spring Framework valójában egy *Dependency Injection* vagy *Inversion of Control* keretrendszer.
- A konténer a komponensek és kapcsolataik leírására, a konfiguráció létrehozására három különböző módot használ: XML, annotáció és Java kód.
- A Spring Framework támogatja az aspektusorientált programozást, azaz bizonyos műveleteket egy helyre össze lehet gyűjteni és aztán a konfigurációval lehet bekapcsolni őket, ilyenek a biztonság, a naplózás, a tranzakciókezelés, stb.
- A Spring Framework nem mindent önmaga implementál, hanem a leggyakrabban használt, legelterjedtebb third party library-ket integrálja egy egységes modellbe úgy, hogy azután ezeket nagyon egyszerű legyen használni és konfigurálni. A Springet ezért *glue kód*-nak is szokták nevezni.
- A Spring Framework egyik fő jellemzője az ún. *boilerplate kódok* eliminálása abból a célból, hogy a fejlesztőnek ne a technológiai problémák megoldásával kelljen töltenie az időt, hanem csak az alkalmazás üzleti logikájára koncentrálhasson. Ezek olyan kódrészletek, amelyeknek önmagukban nincs túl nagy hasznuk, és a fejlesztő csak azért írja őket, mert a keretrendszer, 3rd party library megköveteli.
- A konténert (application context) úgy kell elképzelni, hogy vannak benne különböző komponensek, amelyek között fennállnak bizonyos kapcsolatok. A fejlesztő implementálja, a konténer pedig példányosítja őket és beállítja a közöttük lévő kapcsolatokat.
- A Spring tipikusan háromrétegű webes alkalmazások fejlesztésére való, erre használják a legszélesebb körben. A három réteg:
  - A legalsó réteg a perzisztens réteg, amely az adatbázissal tartja a kapcsolatot, ezt a Spring **Repository** rétegnek hívja.
  - A középső réteg az üzleti logika réteg, ahol az üzleti entitások és az üzleti folyamatok vannak implementálva, ezt a Spring **Service** rétegnek hívja.
  - A legfelső réteg a felhasználói felület réteg, a *user interface*, azaz prezentációs réteg, amely a felhasználóval tartja a kapcsolatot, ezt a Spring **Controller** rétegnek hívja.
- A Spring Framework része a **Spring MVC**, amely egy Spring gondolatiságához illeszkedő webes keretrendszer.
- A Spring nem kezeli a HTTP-t, ennek kezelését egy webkonténerre bízza (pl. Tomcat, Jetty).

---

### Bevezetés a Spring Boot használatába

A Spring Framework egy viszonylag régebb óta létező keretrendszer, a Spring Boot sokkal fiatalabb. Azért hozták létre, mert észrevették, hogy a Spring Frameworkben egy alkalmazás konfigurálása, a beanek testreszabása és összekapcsolása, illetve a különböző third party library-k integrálása elég sok plusz munkával jár. A **Spring Boot**-ban ezeket már előre megírták helyettünk. Kitalálták az ún. *autoconfiguration*-t, ami azt jelenti, hogy a Spring Boot induláskor megvizsgálja, hogy milyen third party library-k vannak a classpath-on, és automatikusan konfigurálja ezeket, méghozzá ún. intelligens alapértékekkel, vagyis a leggyakrabban, legáltalánosabban használt konfigurációkkal. Ettől természetesen el is lehet térni, ha ez valamiért szükséges vagy fontos. A Spring Boot nem egy új keretrendszer, hanem a Spring Frameworkre épül rá és annak a használatát könnyíti meg.

A Spring Boot képes az alkalmazást *self-contained*-ként létrehozni. Ez azt jelenti, hogy maga az alkalmazás tartalmazza a futáshoz szükséges konténert is.

A Spring Boot további előnye a nagyvállalati üzemeltethetőség, vagyis hogy egy üzemeltető információkat tud kinyerni az alkalmazásból (monitorozás) és akár be is tud avatkozni.

Létrehoztak egy https://start.spring.io/ weboldalt, ahol le lehet generálni egy üres alkalmazást, meg lehet adni a projekt Maven koordinátáit, majd ezekkel legenerálódik számunkra egy ZIP állomány, amelyet kicsomagolva és a fejlesztőeszközben megnyitva máris elkezdődhet a fejlesztés.

A Spring Boot moduláris, nekünk csak a számunkra szükséges modulokat kell felvennünk külső függőségként.

A Spring Boot különösen alkalmas kis alkalmazások, *microservice*-ek fejlesztésére, hiszen önmagában is futtatható állományt kapunk, amely mindent tartalmaz az alkalmazás működéséhez, ráadásul könnyen telepíthető és üzemeltethető is.

Ha a feljebb említett weboldalon egy Maven projektet generáltatunk, akkor a letöltött ZIP állományban egy klasszikus Maven projektstruktúra található. Az `src/main/resources` könyvtáron belül található egy kiemelt konfigurációs állomány, az `application.properties`. A Spring Boottal kapcsolatban mindent ebben az állományban kell konfigurálni, ez egyébként a projekt generálásakor üres. Két könyvtárat érdemes még megemlíteni: a `static`, ebbe kerülnek webes alkalmazás esetén a statikus állományok, amelyek nem módosulnak, vagyis a HTML-, CSS- és JavaScript-fájlok, illetve a `templates`, ebbe pedig template-ek kerülnek, amennyiben szerver oldali HTML-generálást akarunk. Két előre legenerált osztály az `Application.java` végű, amellyel el lehet indítani az alkalmazást, és a `Tests.java` végű, amely egy nagyon egyszerű üres tesztesetet tartalmaz, amit elindítva azt lehet megvizsgálni, hogy a Spring jól van-e bekonfigurálva, az application context egyáltalán elindul-e. (A projekt generálásakor az alkalmazás nevét tartalmazó prefix kerül az osztályok neve elé, pl. ha az alkalmazás neve `employees`, akkor `EmployeesApplication.java` és `EmployeesTests.java`.)

A `pom.xml`-be a következő komponensek kerülnek be:

- A `pom.xml` egy másik projektnek lesz a leszármazottja, ezért egy *parent projekt* lesz benne definiálva: `org.springframework.boot:spring-boot-starter-parent`. Ide vannak felvéve és innen öröklődnek a függőségek, a verziószámokkal együtt, ezért nem kell őket megadnunk.
- Ha kiválasztjuk, hogy egy webes alkalmazást szeretnénk generálni, akkor eleve felveszi nekünk függőségként a *Tomcat*-et, ami a default konténer lesz, felveszi a *Jackson*-t, ami a Java objektumok és a JSON dokumentumok közötti megfeleltetésért felelős.
  \> A *Hibernate Validator* újabb verziókba már nem kerül bele.
- Teszthez szükség van a Spring Bootnak az `org.springframework.boot:spring-boot-starter-test` moduljára, amely nagyon sok függőséget felvesz: *JUnit 5*, *Mockito*, *AssertJ*, *Hamcrest*, *XMLUnit*, *JSONassert*, *JsonPath*.

---

### Spring Beanek

A Spring alkalmazás alapvető építőkövei a **Spring Bean**-ek, amelyek egyszerű Java osztályok. Ezeket a fejlesztő hozza létre. A Spring keretrendszer tud róluk és ő példányosítja le ezeket, nem a fejlesztőnek kell ezt megtenni. A Spring Beanek között természetesen lehetnek függőségek és ezeknek a függőségeknek a beállítása is a keretrendszer feladata. Mindezeket a Springnek valamilyen konfigurációval lehet megadni. A Spring Beanek **POJO**-k, azaz **Plain Old Java Object**-ek, tehát semmiféle különös elnevezési konvenciónak nem kell megfelelniük, semmilyen interfészt nem kell implementálniuk. Az application contexten belül helyezkednek el, a konténer vezérli az életciklusukat. Ez azt jelenti, hogy a konténer példányosítja őket, valamint engedi el a referenciát akkor, ha már nincs rájuk szükség, hogy a *garbage collector* be tudja őket gyűjteni.

A Spring Beanek nem ömlesztve vannak, hanem tipikusan rétegekbe rendezve helyezzük el őket. A legalsó, perzisztens rétegben vannak a repository beanek, a középső, üzleti logika rétegben a service-ek és a legfelső, felhasználói rétegben a controllerek.

A Springben alapértelmezetten a singleton tervezési mintát használják, ezért minden bean egyszer és csak egyszer jön létre. Amikor egy webes alkalmazás esetén bejön egy HTTP-kérés, akkor ugyanez a példány kerül megszólításra. Ez abban az esetben lehet probléma, ha a bean tárol valamilyen állapotot, ezért az a legegyszerűbb, ha nem definiálunk benne állapotot tároló attribútumot, csak pl. más beanekre történő hivatkozásokat.

Ha az alkalmazás jar típusú, akkor a belépési pontja a `main()` metódus. Amikor a `https://start.spring.io` oldalon legeneráltatunk egy alkalmazást, akkor létrejön egy `Application` osztály, rajta van a `@SpringBootApplication` annotáció, és van egy `main()` metódusa, ezzel lehet elindítani az alkalmazást.

```
@SpringBootApplication
public class EmployeesApplication {

  public static void main(String[] args) {
    SpringApplication.run(EmployeesApplication.class,
      args);
  }

}
```

A `@SpringBootApplication` maga egy ún. metaannotáció, azaz rajta is egy csomó annotáció van:

- Ezek közül az egyik az `@EnableAutoConfiguration`, amely azt mondja, hogyha a classpath-on talál valamilyen library-t, amihez van konfigurációja, akkor azt automatikusan konfigurálja föl, automatikusan tegye elérhetővé a fejlesztő számára.
- A `@SpringBootConfiguration` annotáción rajta van a `@Configuration` annotáció, ami azt jelenti, hogy ebben az osztályban is tudunk konfigurációt Java kóddal megadni. Tehát ha nekünk valamiért nem jók az intelligens alapértékek, vagy saját magunk szeretnénk valamit beállítani, akkor ezt ebben az osztályban megtehetjük.
- A `@ComponentScan` annotáció azt jelenti, hogy automatikusan felolvassa azokat az osztályokat, amelyeken rajta van a következő annotációk valamelyike: `@Component` jelzi az általános objektumokat, `@Repository` a perzisztens rétegbe tartozó objektumokat, `@Service` az üzleti logika rétegbe tartozó objektumokat és a `@Controller` pedig a user interface rétegbe tartozó objektumokat. Ez utóbbi mellett megjelent a `@RestController` annotáció, mely a `@Controller` annotációt egészíti ki további funkcionalitással.

A *Controller* komponensek egyszerű Java osztályok (POJO-k), a Spring Framework részeként megvalósított Spring MVC részei. Arra valók, hogy a felhasználótól a bejövő kéréseket értelmezzék, és azokra válaszoljanak. Rajtuk van a `@Controller` annotáció. Ezen osztályok forráskódjában is elég gyakran használatosak a különböző annotációk, ugyanis ezekkel tudunk konfigurálni különböző dolgokat, például hogy milyen URL-en lehessen ezeket meghívni, milyen kéréseket vár, milyen válaszokat ad vissza, kell-e ezeket validálni, stb. Nem feltétlenül van Servlet API függősége (bár a Spring MVC nagyon erősen támaszkodik a Servlet API-ra). A legjobb gyakorlat az, hogyha kerüljük a Servlet API-nak a használatát és legfeljebb a Springes osztályokra függünk, vagy lehetőleg még azokat se használjuk, hanem kizárólag a Java Standard Editionben meglévő osztályokat és Springes annotációkat. Az ezen osztályokban található metódusok elnevezésére nincs különösebb konvenció és ezek paraméterezése is flexibilis lehet. A Controllereket kétféleképpen szoktuk használni. Abban az esetben, hogyha olyan alkalmazást írunk, amelyek a HTML tartalmat a szerveroldalon állítják elő, akkor a metódusok egy templatenek (sablonnak) a nevét adják vissza, amelyben az értékeket később a Spring cseréli ki. RESTful webszolgáltatások esetén viszont a visszaadott objektumot megpróbálják leképezni valahogy a HTTP response-ba, tipikusan JSON vagy XML formátumban.

Milyen annotációkat szokás gyakran használni ezekben az osztályokban?

- `@Controller`: ezt kell rátenni ezekre az osztályokra azért, hogy a component scan megtalálja és felolvassa őket, vagyis hogy a Spring MVC egyáltalán tudjon róluk.
- `@RequestMapping`: ezzel tudjuk megmondani, hogy milyen URL-en figyeljen az adott metódus. Ezt meg lehet adni osztályszinten is, ekkor az összes metódusra vonatkozik. Ha mindkét helyen szerepel (osztály- és metódusszinten), akkor konkatenálódik, tehát összeadódik. Az URL-t meg lehet adni *wildcard* karakterek használatával is (például `*`), illetve a HTTP metódus megadható a `method` paraméterrel is.
- `@ResponseBody`: ha egy metódusból visszatérünk, azt egy template-névként próbálja a Spring értelmezni. Akkor kell a metódusra rátenni ezt az annotációt, ha meg akarjuk mondani a Springnek, hogy a visszatérési értéket alakítsa át JSON formátumúvá.

```
@Controller
public class EmployeesController {

    @RequestMapping("/")
    @ResponseBody
    public String helloWorld() {
        return "Hello World!";
    }
}
```

A *Service* komponensekre rá kell tenni a `@Service` annotációt.

```
@Service
public class EmployeesService {

    public String helloWorld() {
        return "Hello World at " + LocalDateTime.now();
    }
}
```

Nézzük meg, hogyan lehet hivatkozni az egyik komponensből a másik komponensbe. Kötelező betartani azt, hogy csak a magasabb szinten elhelyezkedő osztály láthat rá az eggyel alacsonyabb szinten elhelyezkedő osztályra. Azaz a Controller csak a Service réteget látja, a Service pedig csak a Repository réteget. A Controller nem hívhatja a Repository-t, és az előzőekben leírt kapcsolatok fordítva sem történhetnek meg (pl. a Repository nem láthatja a Service-t). Az egy szinten lévő beanek természetesen látják egymást.

**Dependency injection**-nel lehet hozzáférni a függőségekhez. A Spring háromfajta dependency injectiont ismer a beanek közötti függőségek megadásakor: az attribútum, a konstruktor és a setter metódus alapján lehet dependency injectiont megadni. Ez a gyakorlatban azt jelenti, hogy deklarálunk egy attribútumot, és ennek értéket vagy közvetlenül adunk, vagy konstruktoron keresztül, vagy setter-en keresztül. A legjobb gyakorlat, amit a Spring mond, az az, hogy a bean működéséhez kötelezően szükséges függőségeket konstruktorban adjuk át, az opcionális függőségeket pedig, amelyek nélkül tud működni a bean, setter injectionnel.

Ha az osztályban csak egy konstruktor van, akkor automatikusan konstruktor injection van.

```
@Controller
public class EmployeesController {

    public final EmployeesService employeesService;

    public EmployeesController(EmployeesService employeesService) {
        this.employeesService = employeesService;
    }

    @RequestMapping("/")
    @ResponseBody
    public String helloWorld() {
        return employeesService.helloWorld();
    }
}
```

Ha viszont több konstruktor van, akkor nekünk kell kiválasztanunk, hogy melyik kerüljön meghívásra, ilyenkor kell rátenni az `@Autowired` annotációt.

---

### Konfiguráció Javaban

A `@SpringBootApplication` annotáció egy metaannotáció, azaz rajta is vannak további annotációk. Ezekből az egyik a `@ComponentScan` annotáció, ami azt jelenti, hogy az adott csomagban és az alatta lévő csomagokban található összes Spring Beant megtalálja, vagyis azokat az osztályokat, amelyeken rajta van a következő annotációk valamelyike: `@Component`, `@Repository`, `@Service` vagy `@Controller` vagy `@RestController`.

Van azonban lehetőség arra is, ha mi nem a `@ComponentScan`-t akarjuk használni, hanem explicit módon, Javaban szeretnénk megadni a beanjeinket. Ezt Java konfigurációnak nevezik. Ezt akkor szoktuk használni, amikor a Service osztályainkból nem akarunk Springes dolgokra hivatkozni, nem akarjuk őket módosítani, nem akarjuk rájuk tenni a `@Service` annotációt. Ebben az esetben Javaban kell megadnunk, hogy a Spring hogyan példányosítsa az osztályunkat, és ekkor a Spring Frameworköt *non-invasive* módon használjuk, ami azt jelenti, hogy nem kell a saját osztályunkból a Springre hivatkozni. Ezt a konfigurációt egy külön osztályban kell megadnunk, amelyet a `@Configuration` annotációval látunk el. Tipikusan rétegenként szoktuk külön állományokba kitenni a konfigurációs utasításokat. A legjobb gyakorlat egyébként az, hogy a third party library-ket Java konfigurációval adjuk meg, a saját beanjeinket pedig component scannel, ugyanis ezeket tipikusan csak példányosítani kell, azt pedig a Spring is automatikusan el tudja végezni helyettünk az annotáció alapján.

Ha egy Service osztályon nincs rajta a `@ComponentScan` annotáció, a component scan nem fogja felolvasni. Ahhoz, hogy mégis Spring Bean legyen belőle, a következőt kell tennünk: a konfigurációs osztályon (ami nem a Service, hanem egy másik osztály) szerepelnie kell a `@Configuration` annotációnak, valamint létre kell hoznunk egy metódust ebben az osztályban, amelynek visszatérési értéke ennek az osztálynak egy általunk példányosított példánya, és erre a metódusra rá kell tennünk a `@Bean` annotációt. A Spring meg fogja hívni ezt a metódust és amit ez a metódus visszaad, azt el fogja helyezni az application contextben, vagyis pontosan ugyanaz történik, mintha az osztályra rátettük volna a `@Service` annotációt.

```
@Bean
public EmployeesService employeesService() {
  return new EmployeesService();
}
public class EmployeesService {

    public String helloWorld() {
        return "Hello Dev Tools at " + LocalDateTime.now();
    }
}
```

Látható, hogy ebben az esetben mi magunk, explicit módon példányosítottuk a Service osztályunkat. Ez akkor lehet különösen hasznos, ha valamiért nekünk nem elég egy egyszerű példányosítás, hanem olyan példányra van szükségünk, amelyen előtte meghívunk még más metódusokat, akár különböző paraméterekkel.

Fontos megjegyezni, hogy vagy a Service osztályon kell szerepelnie a `@Service` annotációnak, vagy pedig valahol az alkalmazáson belül kell lennie egy `@Bean` annotációval ellátott metódusnak, amely létrehozza a Service osztály egy példányát, mert ha ezek egyike sincs, akkor a Service osztály a Spring számára láthatatlan marad, és a Spring nem fogja azt megtalálni.

---

### Build és futtatás Mavennel

Ha a `https://start.spring.io/` oldalt használjuk arra, hogy a projektünk vázát legeneráltassuk, akkor ott ki lehet választani, hogy a Maven legyen a *build tool* vagy Gradle. Maven projekt választása esetén a klasszikus Maven projektstruktúrát kapjuk. Ha le szeretnénk buildelni az alkalmazásunkat, akkor az `mvn clean package` parancsot kell kiadni, amely a `clean` parancs hatására letörli a `target` könyvtárat, a `package` hatására pedig több különböző lépés után létrejön maga az alkalmazásunk, egy JAR állomány. Ezek a lépések a következők: az osztályok lefordítása, az erőforrás állományok megfelelő helyre másolása, illetve a tesztesetek futtatása.

A `spring-boot-maven-plugin` szerepel a legenerált `pom.xml` állományban, ugyanis ennek a feladata az, hogy miután létrejön a JAR állomány, amiben a lefordított osztályok és az erőforrás állományok vannak, abba még magát a webkonténert, a Tomcatet is belecsomagolja. Ezt úgy teszi meg, hogy az eredeti, “kis” JAR állományt (pl. `employees-0.0.1-SNAPSHOT.jar`) átnevezi `employees-0.0.1-SNAPSHOT.jar.original` névre, és létrehoz egy új, “nagy” JAR állományt, amelyben már benne van a Tomcat konténer is.

Ha szeretnénk elindítani az alkalmazásunkat, azt Maven használatával is megtehetjük. Ehhez az `mvn spring-boot:run` parancsot kell kiadnunk. Ennek hatására először elindul Tomcat és figyelni fog az alapértelmezett 8080-as porton, valamint a Tomcaten belül maga az alkalmazás. Így az alkalmazásunkat már böngészőből is meg tudjuk majd nyitni, le tudunk kérni belőle egy oldalt. Ha az adott gépre nincs telepítve a Maven, csak a JDK, akkor a következő paranccsal indítható az alkalmazás: `java -jar` és ezután következik a JAR állomány teljes neve, tehát például: `java -jar employees-0.0.1-SNAPSHOT.jar`. Mivel ebben a JAR fájlban bele van csomagolva a Tomcat, ezért automatikusan az fog elindulni, és rajta pedig a Springes alkalmazás.

A `https://start.spring.io/` oldalon generált alkalmazás tartalmaz egy ún. Maven wrappert is, ami arra való, hogy akkor futtassuk, ha nincs telepítve az adott számítógépre a Maven. Ez letölti az internetről a Maven-t, kicsomagolja és úgy indítja el a build folyamatot. Ennek az az előnye, hogy nem kell előre külön telepíteni a Gradle-t, mert maga az wrapper megteszi ezt. Használható pl. az `mvnw package` parancs kiadásával.

---

### Build és futtatás Gradle használatával BÓNUSZ

Amennyiben a `https://start.spring.io/` használatával generáltatjuk le az alkalmazásunk vázát, és ott a Gradle projektet választjuk ki, akkor egy olyan projekt jön létre, amelyet Gradle-lel tudunk majd buildelni.

A Gradle-höz két plugint is írtak a Spring Boot fejlesztői. Az egyik az `io.spring.dependency-management` plugin, amely arra való, hogy Maven-szerű függőségkezelést biztosítson, vagyis maga a Spring definiálja a függőségek verziószámait, és amikor mi megadjuk a függőséget, nem kell a verziószámot külön megadnunk, hanem automatikusan a Spring fejlesztői által előre megadott verziószámokat fogja használni. A másik az `org.springframework.boot`, amely képes az előző plugin figyelembe vételével a JAR állományból egy másik, olyan JAR állomány létrehozására, amelybe belecsomagolja a Tomcat webkonténert is.

A `https://start.spring.io/` oldalon generált alkalmazás tartalmaz egy ún. Gradle wrappert is, ami arra való, hogy akkor futtassuk, ha nincs telepítve az adott számítógépre a Gradle. Ez letölti az internetről a Gradle-t, kicsomagolja és úgy indítja el a build folyamatot. Ennek az az előnye, hogy nem kell előre külön telepíteni a Gradle-t, mert maga az wrapper megteszi ezt.

Használható pl. az `gradlew build` parancs kiadásával.

Ezenkívül a Gradle konfigurációs állománya tartalmaz függőséget a JUnit 5-re is.

Nézzük meg, milyen *task*-okat lehet használni:

- Ha le akarjuk buildelni a teljes alkalmazást, elő akarjuk állítani a JAR állományt, akkor a `gradle build` parancsot adjuk ki. Ez nem túl sok mindent ír ki a konzolra, ezért ha jobban szeretnénk látni, hogy mi történik, akkor használjuk a `-i` kapcsolót, amely `INFO` szintű naplózást ad vissza (`gradle -i build`).
- Amennyiben az alkalmazást futtatni is szeretnénk, tehát először elindítani a beépített Tomcat konténert, majd pedig azon az alkalmazást, akkor a `gradle bootRun` parancsot kell kiadni. Ha az adott gépre csak a JVM van feltelepítve, akkor a következő paranccsal indítható az alkalmazás: `java -jar` és ezután következik a JAR állomány teljes neve, tehát például: `java -jar employees-0.0.1-SNAPSHOT.jar` Mivel ebbe a JAR fájlba bele van csomagolva a Tomcat, ezért automatikusan az fog elindulni, és rajta pedig a Springes alkalmazás.

---

### Unit és integrációs tesztek

A Spring Framework fel van készítve a tesztesetek implementálására. Akár Maven, akár Gradle projektet választunk ki a generálás során, a JUnit 5, a Hamcrest és az AssertJ (meg még néhány, teszteléshez használható függőség) alapból a classpath-ra kerül, vagyis ezen eszközöket automatikusan tudjuk használni a tesztesetek megírásához.

Amikor unit teszteket írunk, akkor nem indítjuk be a Springes dolgokat, az application contextet, mert ott már valamiféle integráció történik, az már nem tisztán unit teszt. Unit tesztek azok, amikor konkrétan egy Java osztályt akarunk letesztelni. Ezt csak akkor tudjuk megtenni, ha mi magunk le tudjuk példányosítani. A Springet tudjuk *non-invasive* módon használni, tehát alapértelmezetten adott az, hogy tudjunk egyes komponenseket unit tesztelni.

```
@Test
void testSayHello() {
  EmployeesService employeesService = new EmployeesService();
  assertThat(employeesService.sayHello())
    .startsWith("Hello");
}
```

Külső hivatkozással rendelkező osztályokat pedig úgy tudunk tesztelni a Spring bevonása nélkül, hogy a külső hivatkozásként tartalmazott objektumot kicseréljük egy *test double*-re, például egy *mock* objektumra. Ez úgy viselkedik, mintha az eredeti objektum lenne, ugyanolyan metódusai vannak, de igazi működés nincs ezek mögött.

```
@ExtendWith(MockitoExtension.class)
public class EmployeesControllerTest {

  @Mock
  EmployeesService employeesService;

  @InjectMocks
  EmployeesController employeesController;

  @Test
  void testSayHello() {
    when(employeesService.sayHello())
      .thenReturn("Hello Mock");
    assertThat(employeesController.helloWorld())
      .startsWith("Hello Mock");
  }
}
```

Integrációs teszt írásakor már elindul a Spring application contextje, ő maga fogja létrehozni a beaneket, ő végzi el a beanek közötti kapcsolatok kialakítását, vagyis a dependency injectiont. A tesztosztályt a `@SpringBootTest` annotációval kell ellátni. Ez egy metaannotáció, szerepel rajta egy `@ExtendWith(SpringExtension.class)` annotáció. Ez azt mondja meg a JUnit 5-nek, hogy ezt a tesztosztályt az `SpringExtension`-nel kell lefuttatni. A JUnit 5-ben az *Extension*-ök valók arra, hogy a tesztesetek előtt és után bizonyos kódrészletek lefussanak, jelen esetben beindításra kerüljön az application context. Valójában a Spring tesztfuttatója a különböző tesztesetek között nem indítja be mindig újra az application contextet, hanem cache-eli azt, annak érdekében, hogy megfelelő gyorsasággal fussanak a tesztek. Az application context így az első teszteset előtt fog beindulni, és az utolsó után áll le, és minden teszteset ugyanabban az application contextben fog lefutni. Ezért vigyázni kell, hogy az application contextnek ne legyen állapota, ne módosítsuk az állapotát a tesztesetekkel. A beanek injektálhatóak a tesztbe az `@Autowired` annotációval (dependency injection).

```
@SpringBootTest
public class EmployeesControllerIT {

  @Autowired
  EmployeesController employeesController;

  @Test
  void testSayHello() {
    String message = employeesController
      .helloWorld();
    assertThat(message).startsWith("Hello");
  }
}
```

Az integrációs teszteket tartalmazó tesztosztály neve elnevezési konvenció szerint kapja az `IT` végződést (pl. `EmployeesControllerIT`), amely az *integrációs teszt* kfejezés rövidítése.

A Mavenben különválasztható, hogy melyik fázisában melyik tesztek fussanak le, mert a unit teszteket a surefire plugin indítja el, az integrációs teszteket pedig a failsafe plugin. A surefire plugin alapértelmezetten a következő nevű tesztosztályokat indítja el:

- `**/Test*.java`
- `**/*Test.java`
- `**/*Tests.java`
- `**/*TestCase.java`

A failsafe plugin alapértelmezetten a következő osztályokat indítja el:

- `**/IT*.java`
- `**/*IT.java`
- `**/*ITCase.java`

---

### Developer Tools BÓNUSZ

A Spring Boot-hoz jár egy **Developer Tools** is, ami a fejlesztési folyamatot könnyíti meg.

Nézzük meg, milyen lehetőségeket ad nekünk a Developer Tools:

- Felülír bizonyos property-ket, például kikapcsolja a template cache-t. A template cache azt jelenti, hogy a Spring Boot alapértelmezetten cache-eli a template-eket, vagyis ha már egyszer betöltötte őket, akkor onnantól memóriából szolgálja ki. Ez megnehezíti a fejlesztést, hiszen ha hozzányúlunk a template-ekhez, akkor minden esetben újra kell indítani az alkalmazást. Developer Tools használata esetén tehát nincs template cache.
- Automatikus újraindítás, ha változik az alkalmazás egy része, akkor automatikusan újraindítja azt, nem kell nekünk megtennünk.
- Globális beállítási lehetőségek a saját számítógépen belül, tehát nem kell projektenként mindig beállítani bizonyos tulajdonságokat, valamint attól sem kell félnünk, hogy véletlenül a verziókövető rendszerbe commitoljuk azokat.
- Lehetőség van távoli eléréssel az alkalmazás módosítására, frissítésére, majd az automatikusan újra is indul.

Ahhoz, hogy a Developer Tools-t használjuk, fel kell venni a `pom.xml`-be a `spring-boot-devtools` függőséget.

```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

Ha változik valami a classpath-on, akkor a Developer Tools újraindítja az alkalmazást. IDE-függő, hogy ez mikor történik meg. Eclipse esetén mindig, ha elmentünk egy állományt. IDEA-ban viszont a *Build/Rebuild Project* menüpont használatával (Ctrl + F9 billentyűkombináció).

Úgy oldották meg, hogy két osztálybetöltő van, az egyik a saját kódot tölti be, a másik pedig a függőségeket, tehát újraindításkor nem cseréli ki a sok függőséget, a third party library-ket. Ha viszont a függőségeken változtatunk, tehát a `pom.xml`-hez nyúlunk hozzá, akkor nekünk kell manuálisan újraindítani az alkalmazást. Ilyenkor a háttérben a webkonténer, a Tomcat is újraindul.

Az IDEA-val való fejlesztéskor történhet olyan, hogy az IDEA letörli a `.class` állományt, majd újra lefordítja. Ha pont a kettő között történik meg az újraindítás, akkor nem fogja megtalálni a `.class` állományt. Ehhez a következőt kell beállítani az `application.properties` állományban:

```
spring.devtools.restart.poll-interval=2s
spring.devtools.restart.quiet-period=1s
```

A LiveReload egy ehhez kapcsolódó lehetőség: ha szerveroldalon módosítunk valamit, akkor ez a böngészőben azonnal látszik. Ehhez a böngészőbe föl kell tenni egy LiveReload plugint. A Developer Tools a szerveren elindít egy LiveReload szervert, és a szerver és a böngésző plugin között kialakul egy WebSocket kapcsolat. Amikor pedig a szerveroldalon újraindítás történik, akkor erről értesül a böngésző plugin, és automatikusan frissíti az oldalt.

Statikus állományok változtatása esetén a böngészőre átváltva azonnal látszik a változtatott erőforrás. Ez is IDE-függő, hogy mi számít változtatásnak a Developer Tools számára.

*Global Settings* esetén a saját számítógépemen globálisan felül tudom írni az alkalmazás konfigurációját. Ebben az esetben a *home*-könyvtáramon belül létre kell hozni egy `.config/spring-boot` alkönyvtárat, és ebben el kell helyezni a saját properties állományunkat, amelyben meg kell adni azokat az értékeket, amiket felül akarok írni.

*Remote Applications* használatakor a `spring-boot-maven-plugin`-t tudjuk felkonfigurálni. Az alkalmazás lokális fejlesztésekor a *Remote Client Application*-t kell elindítani, ez hozzácsatlakozik a távoli számítógépen futó alkalmazásunkhoz, és ha változik egy állomány, akkor azt a hálózaton átviszi (a `.class` fájlt), ezt a szerveroldalon lévő alkalmazás észreveszi és újra fog indulni. Ez nagyon jól használható fejlesztő- és tesztkörnyezetben, de azért éles környezetben ne használjuk, mert megvannak a maga veszélyei.

---

### Twelve Factor App

A **Twelve-Factor App** egy olyan ajánlásgyűjtemény, melyet a *Heroku* platform fejlesztői dolgoztak ki arra, hogy hogyan lehet olyan alkalmazást fejleszteni, amely a felhőbe telepíthető és üzemeltethető. A Twelve-Factor App tehát nem más, mint szabályok és javaslatok gyűjteménye. Ha ezeket betartjuk, akkor az alkalmazásunkat egyszerű lesz felhőbe telepíteni. Nem csak felhőben futó alkalmazás esetén érdemes ezeket betartani, hanem klasszikus alkalmazások esetén is, hiszen ezzel az üzemeltetési költségeket biztosan csökkenthetjük, valamint a hibázási lehetőségek is minimalizálhatóak.

A kidolgozásakor a *cloud*-ot, a *Platform as a Service (PaaS)*-t és a *continuous deployment*-et tartották szem előtt, hiszen a Heroku nem más, mint egy PaaS-szolgáltató.

A *Platform as a Service* azt jelenti, hogy a szolgáltató számunkra nem egy virtuális gépet ad, tehát nem nekünk kell rá az operációs rendszert, az adatbázisokat, az alkalmazásszervereket telepíteni, hanem a szolgáltató ezt elvégzi helyettünk. Nagyon sok ilyen szolgáltató létezik (pl. Google App Engine, Redhat Open Shift, Pivotal Cloud Foundry, Heroku, AppHarbor, Amazon AWS, stb.)

A Spring fejlesztése mögött a Pivotal nevű cég áll. Ők dolgozták ki a *cloud native* fogalmat. Ez egy jelző, azokat a cégeket, szervezeteket jellemzi, amelyek gyorsan képesek az automatizálás előnyeit kihasználva olyan alkalmazásokat fejleszteni, amelyek megbízhatóak és skálázhatóak. A fogalom megalkotásakor a *continuous delivery*-t, a *DevOps*-ot és a *microservice*-eket tartották szem előtt. Egy *cloud native* jelzővel rendelkező cég által kifejlesztett alkalmazás jellemzői:

- Tipikusan valahol a felhőben fut (PaaS-en, amely lehet publikus vagy privát is).
- Rendelkezik az *elastic* tulajdonsággal, vagyis ha maga az infrastuktúra észreveszi, hogy hirtelen megnövekedett a felhasználók száma, ezárt automatikusan skálázódik, hogy az alkalmazás ki tudja szolgálni a megnövekedett igényeket.

A Twelve-Factor App a következő 12 szabályt tartalmazza:

1. Verziókezelés: az adott alkalmazáshoz tartozó összes forráskódnak és erőforrás állománynak egy repository-ban kell lenniük, ugyanabban a verziókezelő rendszer repository-ban.
2. Függőségkezelés: az alkalmazás külső függőségeit explicit módon deklarálni kell és külön kell tárolni ezeket az alkalmazás forráskódjától.
3. Konfiguráció: az adott környezetekre jellemző konfigurációk nem az alkalmazás részét képezik, hanem az adott környezet részének kell lenniük.
4. Háttérszolgáltatások: el kell gondolkozni azon, hogy milyen külső háttérszolgáltatásokat akarunk igénybe venni, és ezeket külön kell kezelnünk. Ezek ne legyenek az alkalmazásunk részei, hanem ezek külön jelenjenek meg, és az alkalmazásunk ehhez kapcsolódjon. Ilyen például az adatbázis. Itt fontos megjegyezni, hogy a többi alkalmazás is, amihez a mi alkalmazásunk kapcsolódik, háttérszolgáltatásnak minősül.
5. Vegyük külön a build, a release és a futtatás lépéseit! Ezek ne keveredjenek, hanem legyenek jól szeparálva!
6. Folyamatok: Az alkalmazás állapotmentes folyamatokból álljon. Az állapotmentesség nagyon fontos, hiszen az alkalmazásunk csak így lehet tetszőlegesen skálázható.
7. Port hozzárendelés: fontos, hogy meg tudjuk mondani, hogy az alkalmazásunk melyik porton induljon el. Ez is a skálázhatóság miatt fontos, hogy akár több alkalmazáspéldányt is el lehessen indítani párhuzamosan, ha arra van szükség.
8. Párhuzamosság: fontos arra figyelni, hogy az alkalmazást a felhasználók párhuzamosan is teljes értékűen igénybe vehessék, ne legyenek a párhuzamosságból eredő problémák.
9. Mivel felhőkörnyezetben dolgozunk, fontos, hogy az alkalmazás gyorsan tudjon elindulni és gyorsan tudjon leállni is.
10. Próbáljunk arra törekedni, hogy az éles és a fejlesztői környezet a lehető legjobban hasonlítson egymásra. Így minimalizálható a hibák elkövetésének lehetősége.
11. Naplózás: fontos, hogy az alkalmazás naplózzon. A Twelve-Factor App azt mondja, hogy lehetőleg a konzolra naplózzon, mert az alkalmazásnak nem feladata a naplózás céljának meghatározása, hanem az üzemeltető és az infrastruktúra dolga az, hogy ezt a naplót oda továbbítsa/mentse, ahova szükséges. Tehát a naplózás céljáról ne az alkalmazás döntsön, hanem ezt kívülről lehessen megadni standard, operációs rendszer szintű eszközök használatával.
12. Felügyeleti folyamatok: az alkalmazás mellett tároljuk és ugyanúgy verziókezeljük azokat a felügyeleti folyamatokat, amelyeket ad-hoc módon kell lefuttatni. Ez azért fontos, hogy ne lehessen ilyeneket kívülről, egyszeri esetekben lefuttatni.

Ezenkívül van egy könyv is, amelyet szintén a Pivotalnál írtak. A címe: *Beyond the Twelve-Factor App*. Ez főleg példákat hoz arra, hogy hogyan lehet a fenti 12 szabályt megvalósítani. Ezek közül néhányat érdemes kiemelni:

- A könyv azt mondja, hogy először alakítsuk ki az API-t és utána fejlesszük le az alkalmazást. (Erről megoszlanak a vélemények, sokan vannak, akik ezt pontosan fordítva látják jónak.)
- A konfigurációnál kiemeli a jelszavak és tanúsítványok használatának fontosságát.
- Azt írja, hogy különös figyelmet kell fordítani az autentikációra és az autorizációra, vagyis arra, hogy hogyan történik az alkalmazásba való bejelentkezés és a hozzáférések szabályozása. Ha állapotmentes alkalmazást írunk, akkor nem tárolhatjuk el magában az alkalmazásban a felhasználók adatait, hanem valamilyen más módon kell ezt megoldani.
- Telemetria: ezeket az alkalmazásokat monitorozni kell tudni, azaz az alkalmazás állapotát lehessen lekérdezni, és az így kapott adatokat visszamenőlegesen tárolni és akár grafikusan megjeleníteni is lehessen.

---

### Bevezetés a Docker használatába

A Spring Boot beépítetten tartalmaz Docker-támogatást. Nézzük meg, mi is az a Docker, hol könnyíti meg a munkánkat!

A **Docker** egy operációs rendszer szintű virtualizáció. Nagyon hasonlít a klasszikus virtualizációra, csak éppen kevésbé erőforrás-igényes, ugyanis ebben az esetben nem kell a teljes operációs rendszert telepítenünk és futtatnunk. A virtualizáció használatával különálló, jól elkülönített környezeteket tudunk létrehozni, Docker esetén saját fájlrendszerrel, saját telepített szoftverekkel, függőségekkel együtt. Ezek a létrehozott környezetek viszont csak egy jól meghatározott módon tudnak egymással kommunikálni. A fejlesztéskor a saját számítógépünkkel dolgozunk, de az éles környezet, ahol az alkalmazás futni fog, eltérhet ettől, tehát az alkalmazásunk akár máshogy is működhet. Ha viszont mindkét helyen Dockerben futtatjuk, akkor a két környezet nem tér el egymástól, ezért bízhatunk benne, hogy az éles környezetben nem fognak előjönni olyan hibák, amelyeket csak ott lehet reprodukálni. Ha egyszerre több alkalmazás fejlesztésében veszünk részt, akkor nem kell azzal küzdeni, hogy az adott számítógépre a különböző fejlesztőkörnyezetek különböző verzióit hogyan telepítsük föl, hanem meg tudjuk azt csinálni, hogy létrehozunk egy Docker-konténert, amelyben az adott szoftver egyik verziója, és egy másikat, amiben egy másik verziója van feltelepítve. Azt is egyszerűen meg tudjuk tenni, hogy ilyen módon egy több számítógépből álló hálózatot reprodukálunk. A microservice-ek esetén az is fontos lehet, hogy a Docker konténerrel azonnal egy kész környezetet kapunk, és nem kell egy másik alkalmazást feltelepítenünk, annak minden komponensével együtt.

A Docker architektúrája úgy néz ki, hogy az infrastruktúrára (az adott számítógépre) feltelepítünk egy operációs rendszert, arra a Dockert, és azon lehet futtatni a különböző környezeteket. A Docker sok komponensből, modulból áll. Ezek közül a következőket érdemes megemlíteni:

- Docker Hub: ez egy publikus szolgáltatás Docker image-ek tárolására és megosztására.
- Docker Compose: egyszerre több Docker konténert lehet vele egyidejűleg kezelni és elindítani.
- Docker Swarm: olyan eszköz, amellyel teljes hálózatot lehet felépíteni, natív cluster támogatást tartalmaz.
- Docker Machine: távoli Docker környezetek üzemeltetéséhez használható.

Két fontos fogalom:

A **Docker image** valójában egy (több) fizikai állomány, ez tartalmazza az adott környezetet, annak fájlrendszerét, a feltelepített szoftvereket. Ez az *Image Registry*-ben helyezhető el, tehát például a Docker Hub-on, publikusan. A **Docker konténer**: amikor az image-et letöltjük és elindítjuk, akkor jön létre a saját gépünkön egy konkrét futó példány.

A következő parancsokat lehetnek fontosak a Docker használatakor:

- Az image-eket a `docker images` paranccsal lehet lekérdezni.
- A `docker run`-nal lehet elindítani egy adott image-et (pl. `docker run hello-world` a `hello-world` nevű image-et indítja el). Ha a kívánt image nem található a számítógépünkön, akkor a Docker automatikusan letölti annak a legfrissebb verzióját a Docker Hub-ról, majd el is indítja azt.
- A futó konténereket a `docker ps` paranccsal lehet kilistázni.
- Az összes konténert (a leállítottakat is) pedig a `docker ps -a` paranccsal.
- Egy korábban leállított konténert a `docker start` paranccsal lehet újraindítani.
- A `docker version` paranccsal lehet lekérdezni a Docker verziószámát.
- A `docker run -p 8080:80` parancs azt jelenti, hogy az elindított konténerben elindul egy webszerver, amely a konténer 80-as portján kezdi meg a kiszolgálást. Ez a port hozzákapcsolódik a saját host-számítógépünk 8080-as portjához, és mi azon keresztül kaphatjuk vissza a webszerver által szolgáltatott dolgokat.
- A `docker run -d -p 8080:80` parancs esetén a `-d` kapcsoló hatására azonnal visszakapjuk a promptot, miközben elindul a konténer a háttérben.
- A `docker stop` paranccsal együtt egy számot megadva lehet leállítani egy adott konténert. Amikor elindul egy konténer, akkor egy hash-t kap, amelyre a leállításhoz hivatkozni kell. (Például: `docker stop 517e15770697`.) Ha ennek az első három száma egyedi, akkor elegendő azt is beírni.
- A `--name` paraméter használatával nevet is adhatunk az egyes konténereknek, hogy ne a hash-ekkel kelljen dolgoznunk, ezt követően természetesen hivatkozhatunk rájuk a nevükkel is.
- A `docker logs -f` hatására hozzá tudunk csatlakozni az adott konténerhez, és meg tudjuk nézni, hogy az mit ír ki a konzolra. A `-f`-fel folyamatosan látjuk a kiírt üzeneteket, ahogy azok kiírásra kerülnek.
- Egy konténer törléséhez ki kell adni először a `docker stop` parancsot, és ha ilyen módon leállítottuk, akkor a `docker rm` paranccsal törölni lehet.
- A `docker images` paranccsal az összes letöltött vagy létrehozott image-et ki lehet listázni.
- A `docker rmi` paranccsal ki tudjuk törölni az adott image-et.

Fontos megkülönböztetni az előbbiekben említett `run` és `start` parancsot: a `run` egy image-ből készít új konténert és elindítja, a `start` pedig egy már korábban létrehozott és leállított konténert indít újra.

---

### Java alkalmazások Dockerrel

Ha az alkalmazásunkat Docker konténerben szeretnénk futtatni, ahhoz először létre kell hozni a Docker image-et.

> A videóhoz képest itt kicsit más parancsokat használunk, de alapvetően nagyon hasonló.

Standard Dockeres eszközökkel ez a következőképpen néz ki:

```
FROM adoptopenjdk:14-jre-hotspot
WORKDIR /opt/app
COPY target/*.jar employees.jar
CMD ["java", "-jar", "employees.jar"]
```

Először létre kell hozni az alkalmazás gyökerében egy `Dockerfile` nevű fájlt, amelyben leírhatjuk, hogyan álljon össze az image. Ennek az első sora a `FROM` után tartalmazza azt, hogy milyen, már létező image-ből indulunk ki. Nem kell ugyanis minden esetben elölről kezdeni, hanem támaszkodhatunk már meglévő image-ekre. Ezután a `WORKDIR` paranccsal hozunk létre egy `/opt/app` könyvtárat az image-en belül. Az ezt követő parancsok ebben a könyvtárban fognak dolgozni. A `COPY` paranccsal a `target` könyvtárban szereplő JAR állományunkat másoljuk át az aktuális (`/opt/app`) könyvtárba, így ez már a konténeren belül szerepel. A `CMD` után pedig kiadunk egy parancsot, amivel elindítjuk a JVM-et, és paraméterül pedig átadjuk a JAR állomány elérési útját. (Ez a parancsot a konténer indításakor adja ki, és nem az image buildelésekor.)

A `docker build -t employees .` paranccsal a Docker-t megkérjük arra, hogy az adott könyvtárból (erre utal a parancs végén lévő pont (`.`) karakter) olvassa fel a `Dockerfile`-t, illetve az összes többi fájlt is megkapja a Docker, hogy azokat be tudja másolni az image-be, tehát a `COPY` parancs valójában ezért fog működni. A `-t employees` kapcsolóval mondjuk azt meg, hogy az image neve (*tag*) `employees` legyen. Ezzel tehát létrejön egy image, aminek a neve `employees`, és benne van egy JAR állományunk. Ahhoz, hogy ebből az image-ből létrehozzunk egy konténert, a következő parancsot kell kiadnunk: `docker run -d -p 8080:8080 employees` Így elindul az image alapján a konténer és azon belül elindul az alkalmazásunk is, ami a 8080-as porton várja a kéréseket, valamint a saját számítógépünk 8080-as portja automatikusan továbbításra kerül a konténer 8080-as portjára.

Lehetőség van a Docker vezérlésére Maven-ből is, ehhez egy plugin-t kell felvenni a `pom.xml`-be függőségként, és ennek meg kell adni egy konfigurációt is. Többféle ilyen plugin is van, a videóban a következő szerepel:

```
<plugin>
    <groupId>io.fabric8</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>0.32.0</version>
    <configuration>
      <verbose>true</verbose>
      <images>
          <image>
              <name>employees</name>
              <build>
                  <dockerFileDir>${project.basedir}/src/main/docker/</dockerFileDir>
                  <assembly>
                      <descriptorRef>artifact</descriptorRef>
                  </assembly>
                  <tags>
                      <tag>latest</tag>
                      <tag>${project.version}</tag>
                  </tags>
              </build>
              <run>
                  <ports>8080:8080</ports>
              </run>
          </image>
      </images>
  </configuration>
</plugin>
```

A `Dockerfile`, amit az előbb említett könyvtárban el kell helyezni, ebben az esetben így néz ki:

```
FROM adoptopenjdk:14-jre-hotspot
RUN mkdir /opt/app
ADD maven/${project.artifactId}-${project.version}.jar \
  /opt/app/employees.jar
CMD ["java", "-jar", "/opt/app/employees.jar"]
```

Ez nagyon hasonló az előzőhöz, csak itt placeholderekkel vannak megadva a Maven property-jei. A Mavenen keresztül kiadható parancsok a következők:

- `mvn package docker:build`: legyártja az adott image-et.
- `mvn docker:start`: elindítja az image alapján a konténert.
- `mvn docker:stop`: leállítja és egyben le is törli a konténert. (Minden egyes indításkor új konténert hoz létre.)

A Twelve-Factor Appra hivatkozva elmondható, hogy Docker használatakor fontos betartani a következőket:

- Az alkalmazásaink nagyon gyorsan induljanak el és álljanak le, ne legyenek hosszú inicializációs műveletek.
- Működjön a *graceful shutdown*, azaz az alkalmazás egy szabályos leállításkor tegyen rendet maga után.
- Biztosítani kell, hogy ne maradjon a leállítás után ellentmondásokkal teli adat (batch folyamatoknál is!). Ez egyrészt úgy biztosítható, hogy tranzakciókat használunk, hogy még véletlenül se fordulhasson elő az, hogy ha esetleg két művelet között leállításra kerül a konténer, akkor inkonzisztens adat marad a rendszerben. Másrészt pedig azt is lehet csinálni, hogy a műveleteink idempotensek, azaz nem probléma, ha kétszer egymás után elindításra kerülnek, mert mindenképpen ugyanazt az eredmény adják vissza.

---

### Docker Layers BÓNUSZ

A Docker az image-eket nem egyetlen állományban tartja, hanem többen. Ezeket *layer*-eknek nevezzük. Úgy működik, hogy amikor egy létező image-ből indulunk ki, akkor az egy (vagy több) layert alkot, és az eredeti image-et nem duplikálja, vagyis az csak egyszer szerepel a fájlrendszerben. Az új, létrehozott image-nek létrehoz egy új layert, amelybe már csak a két image közötti különbségeket rakja. Ez azért hasznos, mert így spórolni tud a tárhellyel és a hálózattal. Egy image-hez le lehet kérdezni a `docker image inspect` (+ image neve) paranccsal a hozzá tartozó layereket. A legjobb gyakorlat az, ha úgy építjük fel az image-einket, hogy a leggyakrabban változó állományokat külön layerbe tesszük. Tehát az operációs rendszerhez tartozó állományokat, a különböző third party library-ket alacsonyabb layeren érdemes tartani, mert ezek ritkábban változnak, viszont az alkalmazás saját dolgait (Java alkalmazás esetén az osztályok lefordított `.class` állományait) érdemes ezektől különböző layeren tárolni.

Manuálisan úgy lehet megoldani, hogy a Java alkalmazásunk több layerben legyen, hogy mi állítjuk össze a Docker image-et, figyelve arra, hogy a különböző fájlokat különböző `COPY` paranccsal másoljuk be az image-be. Először a ritkán változó részeket (a third party library-ket), majd utána a gyakran változó állományokat (a `.class` állományokat) kell bemásolni. Ez azt jelenti, hogy nem a teljes JAR állományt másoljuk be egyszerre, hanem kicsomagoljuk és részenként másoljuk be a JAR állomány különböző részeit.

A Spring alkalmazás felépítése úgy néz ki, hogy a `BOOT-INF/lib` könyvtárban vannak a third party library-k, a `META-INF` könyvtárban vannak a különböző leíró állományok, és a `BOOT-INF/classes` könyvtárban vannak az alkalmazáshoz tartozó állományok, vagyis az általunk írt osztályok lefordított CLASS állományai kerülnek ide. Ezeket az itt leírt sorrendben érdemes bemásolni az image-be, így azok különböző, egymásra rakódó layerekre fognak kerülni.

Az alkalmazás elindítása kicsit módosul, ugyanis ekkor már nem a `java -jar` paranccsal lesz indítható, hanem a `java -cp` paranccsal kell megadni a classpath-t, és paraméterül át kell adni több könyvtárat is, amelyeknek a tartalmát szeretnénk, ha bekerülne a classpath-ba.

```
FROM adoptopenjdk:14-jdk-hotspot as builder
WORKDIR app
COPY target/employees-0.0.1-SNAPSHOT.jar employees.jar
RUN jar xvf employees.jar

FROM adoptopenjdk:14-jre-hotspot
WORKDIR app
COPY --from=builder app/BOOT-INF/lib lib
COPY --from=builder app/META-INF META-INF
COPY --from=builder app/BOOT-INF/classes classes

CMD ["java", "-cp", "classes:lib/*", \
                "training.employees.EmployeesApplication"]
```

A Spring a `2.3.0.M2` verziója óta beépített támogatást tartalmaz arra, hogy layerekkel tudjunk Docker image-eket létrehozni. Kétféle megoldást támogat: a *layered JAR* és a *buildpack* létrehozását.

A *layered JAR* megoldás választásával arra utasítjuk a Spring Boot plugint, hogy úgy állítsa össze az alkalmazást, hogy a JAR maga eleve layereken helyezkedjen el, és utána, amikor ki akarjuk csomagolni, akkor csak egy parancsot kelljen ehhez kiadnunk. Ezt a `spring-boot-maven-plugin`-nak a következő konfigurációval lehet megadni:

```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
  <configuration>
    <layers>
      <enabled>true</enabled>
    </layers>
  </configuration>
</plugin>
```

Majd a következő parancsokat kell megadni ahhoz, hogy önmaga kitömörítse a JAR állományt:

```
java -Djarmode=layertools -jar target/employees-0.0.1-SNAPSHOT.jar list

java -Djarmode=layertools -jar target/employees-0.0.1-SNAPSHOT.jar extract
```

A `list` parancs kilistázza az adott JAR-ban lévő layerek tartalmát, az `extract` pedig ki is tömöríti azokat.

Az ehhez tartozó `Dockerfile` így néz ki:

```
FROM adoptopenjdk:14-jre-hotspot as builder
WORKDIR application
COPY target/employees-0.0.1-SNAPSHOT.jar employees.jar
RUN java -Djarmode=layertools -jar employees.jar extract

FROM adoptopenjdk:14-jre-hotspot
WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/spring-boot-loader/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/application/ ./
CMD ["java", \
  "org.springframework.boot.loader.JarLauncher"]
```

Ennek az első blokkja létrehoz egy image-et (ez a *builder*), ez kitömöríti a JAR állományt. A második blokk pedig létrehoz egy második image-et úgy, hogy a kitömörített állományokat másolja át az első image-ből. A `COPY` parancs minden esetben egy új layert hoz létre.

*Buildpack* használatakor Maven-ből vagy Gradle-ből tudunk közvetlenül Docker image-et gyártani. Ez egy magasabb absztrakciós szintet képvisel a `Dockerfile`-hoz képest. Ekkor a következő parancsokat kell kiadni:

- `mvn spring-boot:build-image` (ezzel létrejön az image)
- `docker run -d -p 8080:8080 –name employees employees:0.0.1-SNAPSHOT` (ezzel az image-ből létrejön és el is indul a konténer).

A Twelve-Factor Appnak is van iránymutatása a függőségekkel kapcsolatban:

- Az első szabály az, hogy az alkalmazás nem függhet az őt futtató környezetre telepített semmilyen csomagtól. Ez azt jelenti, hogy nem indulhatunk ki egy olyan image-ből, amely már eleve mindenféle JAR állományokat tartalmaz, hanem ezt magának az alkalmazásnak kell hordoznia.
- Másik szabály, hogy a függőségeket explicit módon deklarálni kell, vagyis meg kell mondani, hogy milyen külső függőségei vannak az alkalmazásnak. (Nem minősülnek függőségnek a különböző háttérszolgáltatások, pl. adatbázis, mail-szerver, stb., ezeket *backing-service*-nek hívja a Twelve-Factor App).
- Fontos, hogy az alkalmazást egybe kell csomagolni a függőségekkel, hiszen a futtató környezetben szükség van ezekre.
- A gyakran változó részeket külön Docker layerbe tegyük.
- Vigyázni kell arra, hogy a build folyamat megismételhető legyen: ne használjunk intervallumokat a verziószámok megadásakor, hanem adjuk meg a verziószámot explicit módon.

---

### Feltöltés GIT repository-ba

Amennyiben a projektünket szeretnénk feltölteni egy Git repository-ba (például a GitHubra), akkor először létre kell hoznunk ezt a repository-t. Ezt megtehetjük a GitHub webes felületén, ahol meg kell adnunk a projektünknek a nevét. Ezután ez a repository elérhető a következőhöz hasonló címen: `https://github.com/username/employees.git` (itt a `username` helyére természetesen a saját felhasználónevünk, az `employees` helyére pedig a saját repository-nk neve kerüljön.) Ezután a saját lokális számítógépünkön a következő parancsokat kell kiadni:

- `git init` - létrehoz egy lokális repository-t az adott könyvtárba
- `git add .` - ehhez a lokális repository-hoz hozzáadjuk az adott könyvtárban található állományokat
- `git commit -m "First commit"` - ezzel a paranccsal véglegesítjük, tehát feltöltjük a lokális repository-ba ezeket a fájlokat (a parancs maga a `git commit`, a `-m "First commit"` pedig csupán egy üzenet ehhez a commithoz)
- `git remote add origin https://github.com/username/employees.git` - ezzel a paranccsal összekötjük a lokális repository-t a távoli (a GitHubon létrehozott) repository-val
- `git push` - ezzel a paranccsal feltöltjük a lokális változtatásainkat a távoli repository-ba, a GitHubra

A GitHub webes felületén ezután azonnal meg is nézhető már, hogy fel lettek töltve a változtatások.

Természetesen az IDEA fejlesztőeszköz a parancssori műveletek helyett grafikus interfészt biztosít. Lásd a *Git / GitHub/ Share Project on GitHub* menüpontot!

A Twelve-Factor App-nak a verziókezelésre is vannak ajánlásai. Fontos, hogy egy repository egy alkalmazást tartalmazzon. Minden más, amit például függőségként definiálunk, az külön repository-ba kerüljön. Ennek a szabálynak a megszegése például az, ha egy több modulból álló alkalmazást modulonként külön repository-ban tárolunk. Ez elsőre jó ötletnek tűnhet, de a build-folyamatot nagyon nagy mértékben megbonyolítja. A szabályt sérti az is, ha ugyan több külön futtatható alkalmazásunk van, de ugyanazon a domainen, ugyanazon az adatbázison dolgoznak, mégis különböző repository-kban vannak. Ez azért nem igazán jó megoldás, mert ezek az alkalmazások nagyon összefüggenek, ha az egyik közülük módosul, akkor nagyon valószínű, hogy módosulnia kell a másiknak is. Ebben az esetben érdemes őket egy repository-ba összevonni, még akkor is, ha ezek különböző alkalmazások. Az viszont természetesen kerülendő, hogy teljesen különálló alkalmazások kerüljenek egy repository-ba. A különböző környezetekre telepített alkalmazásoknál alapvető igény, hogy egyszerűen meg tudjuk nézni, hogy mely verzióból készült. Ez nagyban megkönnyíti a hibakeresést. Fontos, hogy ez látható legyen a felhasználói felületen.

Fontos figyelni a *Conway törvény*-re: “azok a szervezetek, amelyek rendszereket terveznek, …kénytelenek olyan terveket készíteni, amelyek saját kommunikációs struktúrájuk másolatai”. A fejlesztő csapatok száma tipikusan együtt jár az alkalmazás moduljainak számával. Erre érdemes figyelni, hogy a különböző csapatok jól körülhatárolható keretek között, egymástól külön tudjanak dolgozni, így hatékonyabbak lesznek, és kevesebbet is kell majd a csapatok között szinkronizálni. Ha túl nagy az alkalmazás és egyszerre több csapat kezdene el dolgozni rajta, akkor érdemes valamit kitalálni, hogy ez hosszú távon ne legyen így, mert a közös munka nagyon be tudja lassítani a csapatokat. Tehát érdemes úgy felosztani a feladatot, hogy minden fejlesztő csapatnak meglegyen a maga külön kis microservice-e, és ezzel lehessen hatékonyabbá tenni a közös munkát.