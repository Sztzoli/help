## 0.hét 2 óra

Flyway

* migrate - létrehozza a táblát  ha üres, ha nem üres akkor nem fogja létre hozni hibával elszáll, érdemes eldobni a táblákat

* clean - nem érdemes mindig elfogja dobni a táblákat

* teszt esettnél való életben külön vannak az adatbázisok. legegyszerűbb 2 adatbázis létrehozása majd később lesz róla szó

* valós alkalmazásnál csak az adott táblát dobjuk

Teszt  

* Tilos id-vel teszt eseteket írni vagyis számot leírni, mindig vissza kell olvasni
* előbb gyerektábla törlés aztán szülő bővebben később

Polimorfizmus:

* Többalakúság. Azt jelenti, hogy egy példányosított objektum több formában is megjelenhet, az objektumot többféle típusú változónak is értékül lehet adni.
*  Az objektum *dinamikus típusa* az, amellyel konkrétan példányosítjuk, a példányosított objektumot azonban értékül adhatjuk többféle *statikus típusú* változónak is. 
* A változó statikus típusa lehet az objektum dinamikus típusával megegyező, de lehet annak bármely ősosztálya, vagy bármely, a dinamikus típus által implementált interfész is. Az objektum ezek bármelyikének alakjában megjelenhet, tehát bármelyik, az osztályhierarchiában lévő ősosztálya (akár az `Object` osztály), vagy azok által implementált bármely interfész alakjában is.

Dependency inversion

* DI-nek nevezzük azt, amikor egy osztály úgy használja egy másik osztály 
  objektumát, hogy nem az osztályára hivatkozik, hanem az általa implementált interfészre.
  Azaz amikor nem egy osztályra mutat egy függőség, hanem annak egy interfészére. 


## 1.hét
### 1 óra



Teszt

* given - when - than
* szúrópróba szerűen 
* minden szélsőséges esettre legyen egy metódus
* statikus metódusokat ne használjunk
* állapotot ne tároljunk
* lefedettség 80%
* TDD
* független
* JUnit újrapéldányosítja a teszt osztályt minden tesz előtt
* third party libary-t nem tesztelünk



 Házi meetingroomba implementálni meetingek listája időre is lehet

### 3 óra

surfire-plugin-maven: 

* junit 4ig nem kellet
* goals runs a unit test application
* maven  eredetileg egy régebbi surfire-plugin-maven van ezért kell új
* maven csak egy build rendszer
* ha nincs mvn clean package Build Failure

Git egyszerre többen dolgozunk rajta

* mindig pull commit és push elött
* confict: ugyanaz a sor módosult
* repo-> setting-> manage acces-> invite collaborator onnantol már ő is tud pusholni

### 4 óra (péntek)

## 2 hét

### hétfő

JUnit

* fail() -> elavult kivételt dobó metódus
* asume -> előfeltétel írás
* meta annotáciok magyarázása

### szerda

* hamcrastet nem nagyon frissítik, mig AsserJ olvashatóbb és gyakrabban frissítik
* legtöbb helyen Junit4 + Hamcrest
* spy inkább mockolni kellene
* argumentcapture



Elkezdjük ellenőrizni az előrehaladásotokat. Ennek több lába van: ott vagytok-e konzultáción, megnézitek-e a videókat, valamint megcsináljátok-e a gyakorlati feladatokat. Ez utóbbihoz szeretném segítségeteket kérni! Kérem, hogy a teszt témakörhöz tartozó projekteket a `senior-solutions` repository-ban, a `locations-solution` mappába helyezzétek el. A Spring Bootos feladatokat pedig a `locations-spring-solution` mappában.Kérem megértéseteket ezzel kapcsolatban. Védelmünkre elmondom, hogy való életben nagyon gyakran fogsz ilyen kérésekkel találkozni, hogy nevezd át, mozgasd át, tedd ide, tedd oda, és ezeket gond nélkül meg kell oldanod. Ha ezek problémát okoznak, akkor gyakorolni kell. Néhány segítség a variáláshoz. Ezerféleképp meg lehet csinálni, én így szoktam repo-t átnevezni:

- commitolj és push-olj fel mindent
- zárd be az IDEA-t
- nevezd át a GitHub felületén a repository-t
- clone-ozd ki újra
- nyisd meg az IDEA-ban újra

Így szoktam projektet átnevezni egy repository-n belül:

- commitolj és push-olj fel mindent
- zárd be az IDEA-t
- töröld le az IDEA fájljait (`.idea` könyvtár, `.iml` fájl)
- nevezd át fájlkezelővel a könyvtárat
- írd át az `artifactId` -t a `pom.xml` -ben notepaddel
- nyisd meg újra IDEA-ban



### péntek



## 3 hét

### Docker

# 4 hét

## rest

* client-server applikáció clien kéréseket küld a szervernek
* erre van dokumentáció ha ezt be tartjuk akkor fog jól működni mindegy milyen nyelven
* http kérés és műveletekből áll
* CRUD müveletek
* kérés a server json ba adja vissza a response-t
* @restContorller magában foglalja és hogy a getet bodyként küldi ki, spring meg a status be állítja
* de Responseentity más mint a body
* DTO tervezési minta
* command - single response elve
* requestparam reqestpath az url mókolja
* request param = locations?name=pest szürésnél érdemes használni
* reqestpath entitást add vissza
* requestbody httpreqest bodyját adja
* post érdemes erőforrást létrehozni put-tal updatelni -> idempotencia müveltet többször elvégzek nem változik
* uri egyedi azonositó
* url is uri

## 5 hét

rest -assure - az spring független









  