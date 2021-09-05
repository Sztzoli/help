# Spring interjú kérdések

## Mire való a Spring, miért van?

 A Spring Framework egy keretrendszer nagyvállalati alkalmazások fejlesztésére. A nagyvállalati alkalmazásnak azokat az alkalmazásokat nevezzük ahol nem elegendő a JSE, további tulajdonságokra van szükség.

Felmerülő problémák:

* komponenseket példányosítását és életciklus vezérlést a keretrendszer végzi
* távoli elérés
* párhuzamosság
* perzisztencia: JSE elavult JDBC sok boiler kód és kötelezően kezlendő kivétel (checked exception)
* tranzakció kezelés
* aszinkron üzenetküldés
* ütemezés
* konfigurálhatóság
* naplózás, monitorozás
* biztonság
* automatizált tesztelés

## Application context

A fejlesztőnek a Springbe egyszerű java objektumokat kell implementálnia (POJO-Plain old java object), ezek a komponensek. a Komponensek a konténer felügyelete alatt állnak: vezérli az életciklusát, az példányosítja őket, és engedi el a referenciát amikor már nincs rá szükség. A konténer neve application context. Ezt egy map ként kell elképzelni. 

## *Dependency Injection* vagy *Inversion of Control* keretrendszer.

* Inversion of control: beanek közötti kapcsolat. amikor egyik bean meghivja a másik beant akkor közte ott van a spring vagyis mikor meghivom a másik beant akkor jeltem a springnek és ő hivja meg. Mindig keretrendszeren keresztül történik a hivás és a keretrendszer betud avatkozni.
* dependency injection: IoC egyik megvalósitása. Ez is a kapcsolatokról szól hogy hogyan szerzek referenciát egy másik beanre. Definiálom azt h szükségem van egy másik beanre és a keretrendszer adja oda nekem. A keretrendszer adja oda nekem a függöséégemet.
  * attribútum: egységbezárás meg sérti
  * setter : opciónális függöség
  * konstruktor : ajánlott ha egy konstruktor van akkor nem kell @Autowired annotáció



## Spring MVC

A Sring MVC alkeretrendszere a Spring frameworknek, aminek segítségével kezelni tudjuk a Http kéréseket, válaszokat.

## TomCat

java nyelven készült webserver és servlet container mert implementálja a Sun féle Java servlet-et és a JavaServer Pages specifikációkat.

## Spring Bean

Egyszerű Java osztály. A fejlesztő hozza létra. a Spring tudróluk és ő példányosítja le.Beanek közt lehetnek függöségek és aazeknek a függöségeknek a beállítása is a spring feladata. Az apllication contexten belül helyezkednek el, a konténer vezérli az életciklusukat.

* Repository
* Service
* Controller
* component

alapértelmezetten singleton beanek jön létre vagyis

A componentscan olvassa fel őket.

@Bean 3-party libary vagy speciális példányosítás adunk meg

## Rest webszolgáltatások

alkalmazás erőforrások gyűjteménye, melyeken crud műveleteket lehet végre hajtani

mire valók: 

* két alkalmazás tudj egymással kommunikálni

Http Metódusok: megmondja hogy az erőforráson milyen műveletet akarok végezni

* POST
* GET
* PUT: idempotens
* DELETE

URL: erőforrás egyedi útvonala

HttpStátuszkód: szerenék valamilyen müveletet elvégezni az előforráson és ez ennek az eredménye:

* 









