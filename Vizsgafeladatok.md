# Vizsga kérdések

## Java, Maven, GIT, UML, TESZT

### Melyik állítás hamis az alábbiak közül? JAVA

1.  A szemétgyűjtő mechanizmust a virtuális gép biztosítja.

2. A lefordított bájtkód platform független.

3. Az Oracle szállítja a JDK-t, mely a JRE és olyan (főleg) parancssori fejlesztőeszközök, mint a fordító. A JRE-nek része a virtuális gép és az osztálykönyvtár.

4. **A virtuális gép elemzi a forráskódot, és soronként futtatja.**

   Válasz: 4 A JVM feladata a bytekód futtatása

### Melyik állítás igaz az alábbiak közül? JAVA

1. Java alkalmazások kizárólag fejlsztőeszközzel fejleszthetők.
2. **A fejlesztőeszköz is a fordítót és a JVM-et használja.**
3. Maven nélkül nem lehet Java projektet létrehozni.
4. A Javaban van standard projektfelépítés, könyvtárszerkezet.

### Milyen operációs rendszeren lehet Java alkalmazást futtatni? JAVA

1. **Mindegyiken, a Java alkalmazásokat az egyes platformokra elkészített Java Virtuális Gépek (JVM) futtatják, emiatt platformfüggetlen**
2. A Java kifejezetten a Microsoft Windows operációs rendszerhez készült programozási nyelv
3. A Java egy open-source programozási nyelv, ezért Linuxra készíthetünk vele programokat
4. A Java az Apple terméke, MacOS és IOS alkalmazásokat készíthetünk vele

### Melyik állítás hamis az alábbiak közül? MAVEN

1.  Java-ban nincs standard projektstruktúra

2.  A Maven alapelve a convention over configuration

3. **Az IDE nem tud Maven nélkül működni**

4.  A Maven parancssorból indítható, nem szükséges fejlesztőeszköz a használatához

   Válasz: maven egy szabvány eszköz amit a build folyamatot segíti elő

### Melyik könyvtárba kell elhelyezni a fájlokat Maven esetén? A megadott könyvtárnevek mindig a projekt főkönyvtárától értelmezendőek. MAVEN könyvtár struktúra

1.  **Az src/main/java könyvtárba kell elhelyezni a Java forrásfájlokat és az src/test/java könyvtárba a teszteseteket**

2.  A main könyvtárba kell elhelyezni a Java forrásfájlokat és a test könyvtárba a teszteseteket

3. A main/src/java könyvtárba kell elhelyezni a Java forrásfájlokat és a test/src/java könyvtárba a teszteseteket

4.  A java könyvtárba kell elhelyezni a Java forrásfájlokat és a java/test könyvtárba a teszteseteket

###  Mi azonosítja a Maven projektet (koordináták)?

1.  A projekt neve
2.  A projekt csomagneve és neve
3.  A projekt groupId, artifactId tulajdonsága
4.  **A projekt groupId, artifactId és version tulajdonsága**

### Válaszd ki az igaz állítást! MAVEN

1. A Maven az alkalmazás forráskódját az src/java/main könyvtárban tartalmazza
2. A Maven koordináták kizárólag a group és ver.
3. **Az mvn package paranccsal lehet lefordítani a forráskódot, valamint összecsomagolni a jar állományt.**
4. A Maven preferálja, hogy mindent úgy adjunk meg, ahogy mi szeretnénk, azaz egyéni konfigurációkat használjunk.

### Válaszd ki az igaz állítást! GIT

1. **A push művelettel lehet a lokális repository-ból a commitokat feljuttatni a távoli repository-ba.**
2.  A push művelettel lehet a lokális repository-ba a commitokat bejuttatni.
3.  A commit adja hozzá a fájlokat a Githez, hogy arról tudjon a verziókezelő, de hogy bekerüljön, még egy plusz műveletet el kell végezni.
4.  Ha kitörlünk egy állományt, az automatikusan eltűnik a Git repo-ból, nem kell commit művelet.

### Melyik dolog nem szerepel egy UML diagramon? UML

1. **Lokális változók**
2. Interface implementálása
3. A példányváltozók láthatóságaa
4. A metódusok visszatérési értéke');

### Hogy hívjuk azt, amikor az programunk alapegységeit teszteljük? TESZT

1. **Unit test**
2. Regression test
3. Integration test
4. End-to-end test

### Melyik metódussal NEM lehet egy booleant visszaadó metódus visszatérési értékét tesztelni? TESZT

1. **assertThrows**
2. assertTrue
3. assertEquals
4. assertFalse

## Csomagok

### Melyik állítás igaz?

1.  **Nem érdemes a forrásállományokat csomagokon kívül elhelyezni**

2.  Ha az A osztályból el akarjuk érni egy másik csomagban lévő B osztályt, akkor csak importálással tudjuk azt elérni

3.  A csomag neve és a könyvtár neve eltérhet

4. Az A osztályból csak akkor használható a B osztály, ha beimportáljuk

   Válasz: csomag neve és könyvtár neve nem térhet el, tudjuk minősített névvel is elérni, nem kell az import

### Melyik csomag osztályai kerülnek automatikusan importálására, így azokat használhatjuk import nélkül is?

1. Nincs ilyen csomag, mindig importálni kell
2. **A java.lang csomag automatikusan importálásra kerül**
3. A String csomag automatikusan importálásra kerül
4.  A common csomag automatikusan importálásra kerül

### Melyik hamis az alábbi állítások közül?

1. **Az importáláskor csillaggal megadva beimportálhatjuk az adott csomagnak és annak összes alcsomagjának osztályát**
2. Nem kell importálni a java.lang csomag osztályait
3. Az importálással más csomagban lévő osztályokat lehet használnunk, anélkül, hogy minősítenénk
4. Az importálás helyettesíthető azzal, hogy az osztályt csomagnévvel minősítem

### Válaszd ki az igaz állítást!

1. Az összes csomag automatikusan importálásra kerül.
2. A Scanner automatikusan importálásra kerül.
3. A String osztályt importálni kell ahhoz, hogy használhassuk
4. **A java.lang csomag automatikusan importálásra kerül.**

### Válaszd ki az igaz állítást!

1. A private módosítószóval ellátott tagok az adott csomagban látszanak.
2. A láthatósági módosítószóval el nem látott tagok mindenütt látszódnak.
3. A public módosítószóval ellátott tagok csak az adott csomagban és leszármazottjaiban látszanak.
4. **Az attribútumokat private láthatósággal vegyük fel, így csak az adott osztályon belül látszódnak.**

## Java alapok

### Melyik hamis a következő állítások közül?

1.  Az osztály fő építőelemei a konstruktorok, metódusok és attribútumok

2. **Konstruktor megadása kötelező**

3. A getterek és setterek metódusok

4.  Az osztály publikus metódusai adják annak interfészét (attribútumokat ne tegyük publikusra)

   Válasz: Default Konstruktor

### Válaszd ki az igaz állítást!

1. Az osztályok tagjai kizárólag az attribútumok (fields), metódusok és getter/setterek.
2. Az attribútumok (fields) speciális metódusok.
3. **A konstruktorok felelősek az objektum állapotának inicializálásáért.**
4. A metódusok tárolják az attribútumok (fields) értékeit.

### Melyik helyes main() deklaráció? MAIN

1.  public static int main(String[] args)
2.  public final int main(String args)
3.  public final void main(String args[])
4.  **public static void main(String[] args)**



### Melyik írja ki a konzolra azt, hogy Hello World? SOUT

1. **System.out.println("Hello World")**
2.  print("Hello World")
3.  System.console.print("Hello World")
4. println("Hello World")

### Melyik írja ki a konzolra a String msg változó értékét? SOUT

1. **System.out.println(msg)**
2. System.console.write(msg)
3. msg.toString()
4. System.print("msg")

### Melyik hamis a kódolási konvenciókkal kapcsolatban? KONVEKCIÓ

1. Változónevek első karaktere, ha betű, kisbetű legyen

2. Metódusnevek első karaktere, ha betű, kisbetű legyen

3. **Osztálynevek első karaktere, ha betű, kisbetű legyen**

4. A konstans értékek nevei csupa nagybetűvel és a szavak között aláhúzás karakterrel szerepeljenek

   Válasz Osztályneve első karaktere ha betű mindig nagy betű

### Melyik változónév helyes a Clean Code alapelvek szerint? CLEAN CODE KONVENKCIÓK

1. **firstName**
2.  cc
3.  last_name
4.  FirstName

### Melyik érvényes Java kulcsszó? Kulcscszó

1. **new** 
2. main
3. function'
4. Int


### Melyik kulcsszóval hivatkozhatunk egy objektumon belül saját magára? Kulcsszó

1. **this**
2. instance
3. that
4. super

### Melyik kulcsszó jelöl ciklust? Kulcsszó

1. **while**
2. if
3. switch
4. return

### Melyik helyes definíció, amennyiben csak a beépített osztálykönyvtárt használjuk?

1.  Int i = 0;

2. **int i = 0;**

3.  arraylist names = new List

4.  char c = null;

   Válasz: Int az nincs, helyesen list names = new arraylist, char az primitív nem lehet null
### Mely állítás igaz a következők közül? FINAL
1.  Ha final kulcsszóval deklarálunk egy lokális változót, akkor annak a deklarációkor értéket kell adni
2.  Ha final kulcsszóval deklarálunk egy lokális változót, akkor bármikor adhatunk neki értéket a metóduson belül
3.  **Ha final kulcsszóval deklarálunk egy lokális változót, akkor az első használat előtt adnunk kell neki értéket**
4.  Ha final kulcsszóval deklarálunk egy lokális változót, akkor int típus esetén az értéke mindig 0

### Melyik hamis az alábbiak közül az attribútumokra vonatkozóan? ATTRIBÚTUMOK
1.  Az attribútumok kezdőértékkel rendelkeznek, pl. egész számok esetén ez 0
2.  **A lokális változók kezdőértékkel rendelkeznek, pl. egész számok esetén ez 0**
3.  Deklaráljuk az attribútumokat private módosítószóval, és csak metódusokon (pl. getter és setter) keresztül férjünk hozzá
4.  Attribútumok értékei pl. konstruktorban is inicializálhatóak

### A példányváltozók elrejtésének több előnye is van. Az alábbiak közül melyik NEM az? ATTRIBÚTUMOK

1. **A privát változókat titkosítja a JVM, így egyesetleges hacker-támadás során nagyobb biztonságban vannak az adataink.**
2.  A privát változókat nem tudjuk véletlenül módosítani egy másik osztályból, így könnyebb ügyelnünk az adataink koherenciájára.
3.  Az osztályunk belső szerkezetét meg tudjuk úgy változtatni, hogy ez más osztályban levő kódra ne legyen hatással, ez által könnyebben karbantartható lesz a kódbázisunk.
4.  Ha csak metóduson keresztül van lehetőség módosítani egy változó értékét, akkor be tudunképíteni extra validációkat.

### Hogyan hozható létre egy oszály új példánya? CLASS

1. A class kulcsszóval
2. Egy új fájl létrehozásával
3. A konstruktor meghívásával
4. **A new kulcsszó segítségével**



### Válaszd ki az igaz állítást! CLASS

1. **Az osztály egy modell, és ez alapján több példány hozható létre.**
2. Egy osztályból egy példány hozható létre.
3. A példányosítás során mindig új osztály születik.
4. Egy objektumból több példány példányosítható.

### Válaszd ki az igaz állítást! KONSTRUKTOR

```java
public class Trainer {
    private String name;
    private int yearOfBirth;
    public Trainer(String name) {
        this.name = name;
        yearOfBirth = 30;
    }
}
```

1. A name formális paraméter elfedi az attribútumot, így a name valójában nem kap értéket.
2. A yearOfBirth attribútumnak így nem lehet értéket adni.
3. A yearOfBirth attribútum értéke 0 marad, hiszen az az attribútum alapértelmezett értéke.
4. **A name értéke a példányosításkor konstruktorban átadott érték lesz, a yearOfBirth értéke 30.**

### Válaszd ki a hamis állítást! THIS

1. A this kulcsszó az aktuális példányra vonatkozik.

2. **Mivel az attribútum elfedheti a formális paramétert, a this kulcsszót kell használni.**

3. A formális paraméter elfedheti az attribútumot.

4. A setter metódus feladata egy attribútum értékének beállítása.

   Válasz: fordítva igaz

### Mi hamis a lokális változókkal kapcsolatban? LOKÁLIS VÁLTOZÓK

1. lokális változók nem kapnak kezdőértéket

2. **A final kulcsszóval ellátott lokális változónak a deklarálás sorában értéket kell adni (pl. final int i = 5;)**

3. A lokális változók a stacken helyezkednek el

4. A nem null értékû referencia típusú lokális változók egy heapen elhelyezkedő objektumra mutatnak

   Válasz: Használat elött kell értéket neki adni

### Mi az a konstruktor? KONSTRUKTOR

1. Új példány létrehozása
2. Új osztály létrehozása
3. **A konstruktor hasonlít egy metódusra, amely automatikusan lefut új példány létrehozásakor**
4. Egy változó

### Mely igaz a következő állítások közül? KONSTRUKTOR
1. Kötelező minden osztályban konstruktort megadni
2.  **A konstruktor neve meg kell, hogy egyezzen az osztály nevével**
3. A konstruktor visszatérési értéke lehet void
4.  A konstruktort a példányosítás után is meg lehet   hívni

### Mely állítás igaz az implicit (default) konstruktorral kapcsolatban? KONSTRUKTOR
1.  Fogadhat paramétereket
2.  private módosítószóval rendelkezik
3.  Amennyiben definiálunk egy paraméteres konstruktort, az implicit (default) konstruktor továbbra is hívható
4. **Törzsében szerepel egy super() hívás**

### Melyik metódussal lehet túlterhelni (overload) a következő metódust? METHOD OVERLOADING
public Course createCourse(String name) {}

1. public Course create(String name) {}

2. public SpecificCourse createCourse(String name){}

3.  **public Course createCourse(String name, Level level) {}**

4.  public Course createCourse(String name) {}

   Válasz: 1 nem ugyan az a method név, 2 visszatérésiérték különböző, 4 ugyanaz mint az eredeti fordítási hiba

### Válaszd ki az igaz állítást! METHOD

1. A return utasítás csak a metódus végén lehet.
2. A return utasítás egy metódusban csak egyszer szerepelhet.
3. A void visszatérési típusú metódusnál nem használhatunk return utasítást.
4. **A return utasításnak nem kell pontosan olyan típust visszaadni, mint a visszatérési érték, hiszen itt is lehet típuskonverzió.**

### Melyik állítás NEM igaz? METHOD OVERLOADING

1. **Ha egy metódust túltöltünk (overload-olunk), azaz több különböző változatot deklarálunk belőle, amik csak a paraméterlistában térnek el, azt jelölhetjük a @Overload annotációval.**
2.  Ha egy metódust túltöltünk (overload-olunk), azaz több különböző változatot deklarálunk belőle, amik csak a paraméterlistában térnek el, azt jelölhetjük a @Overload annotációval.
3.  Metódusok túltöltése (overload-olása) esetén a paraméterek neve nem számít, csak a paraméterek típusa azok sorrendjében nézve.
4.  Egy örökölt metódust csak akkor kötelező felülírni (override-olni), ha az az ősosztályban absztraktként van deklarálva, a leszármazott osztály pedig nem absztrakt.




### Melyik hamis a Java memóriakezelésével kapcsolatban? STAC,HEAP
1.  **Az objektumok a stacken jönnek létre**
2.  A lokális változók, ha referenciák, a referencia a stacken jön létre, az objektum a heapen
3.  A primitív típusú lokális változók a stacken jönnek létre
4.  Minden metódushívás kap egy külön területet a stacken, melybe a lokális változók értékei kerülnek

### Melyik állítás hamis az immutable osztályokkal kapcsolatban? IMMUTABLE OSZTÁLY
1.  Érdemes az attribútumait final kulcsszóval ellátni, hogy csak egyszer lehessen neki értéket adni.
2.  Használatuk azért is hasznos, mert paraméterként átadva biztosak lehetünk benne, hogy a hívás során nem változik az értéke.
3. A String osztály immutable
4.  **A metódusai módosíthatják az attribútumok értékét, csak a paraméterek értékét nem módosíthatják**



### Mely igaz a JavaBeans konvenciókkal kapcsolatban? JAVABEANS
1.  Minden Java osztálynak JavaBeansnek kell lennie

2.  Kötelezően lenniük kell getter és setter metódusainak

3.  Minden típus esetén ugyanazt az elnevezést kell alkalmaznunk, get prefix, utána az attribútum neve, aminek az első karaktere nagybetű, pl. getName()

4. **Attribútum, és a hozzá tartozó metódusok összefoglaló neve property**

   Válasz: private, getter, setter, üres konstruktor

### Az alábbiak közül melyik nem ciklus? CIKLUS

1. **switch**
2.  while
3.  for
4.  do-while

### Mi az a scope? SCOPE

1. Változók hatóköre.
2. Referencia egy objektumra.
3. Függvény visszatérési értéke.
4. Függvény bemenő paramétere.

### Létre akarok hozni egy Object típusú példányt, és elmenteni őt egy Object típusú változóba, hogyan tudom ezt megtenni? OBJECT

1. **Object object = new Object();**
2. Object object = Object();
3. Object object = new Object;
4. Object = new Object();

### Egy korábbi sorban már létrehozott Object object változóm értékét szeretném felülírni egy új Object példánnyal, hogyan tudom ezt megtenni? OBJECT

1. **object = new Object();**
2. Object object = new Object();
3. object = Object();
4. object = new object();');

## TÍPUS, TÍPUSKONVERZIÓK

### Adott két változó: ADATTÍPÚS

int a = 2;
int b = 4;
Milyen adattípusban tárolható a következő kifejezés értéke: b % a == 0?

1. **boolean**
2. int
3. Integer
4. false

### Mi lesz a következő utasítás eredménye? KONVERZIÓK

double d = 3 + 5 / 2

1. Fordítási hiba.
2. d értéke 4
3. **d értéke 5**
4. d értéke 4.5

### A következő típuskonverziók közül melyik nem fordul le? TÍPUSKONVERZIÓK

1. byte b = 100
2. **int i = 1.1**
3. double d = 1
4. int i = (int) 1.1

### Hogyan konvertálunk egy egész számot String típusú változóba (int i = 5)? KONVERTÁLÁS

1. String s = i + "";
2. String s = Integer.toString(i);
3. String s = "" + i;
4. **Mindegyik megoldás helyes**

### Hogyan hozol létre egy szövegből egész számot? String s = "5" KONVERTÁLÁS

1. int i = s;
2. int i = (String) s;
3. int i = String.parse(s);
4. **int i = Integer.parseInt(s)**

### Mi hamis a típuskonverzióval kapcsolatban? TÍPUSKONVERZIÓ

1. Típuskonverzió operátorok alkalmazásakor, paraméterátadáskor, metódus visszatéréskor történhet

2. **int típusból Integer típussá alakításkor implicit típuskonverzió van**

3. A típuskonverzió értelmezett primitív és referencia típusok esetén is

4. A típuskonverzió implicit, ha nem írjuk ki, explicit ha kiírjuk és kerek zárójeleket alkalmazunk

   Válasz: autoboxing van

### Melyik igaz az alábbi állítások közül? INT Típus

1. Egész literálok megadása csak tizes számrendszerben történhet

2. Változót a következőképpen deklarálunk: let a = 0;

3. Változót a következőképpen deklarálunk: var a = 0;

4. **Változót a következőképpen deklarálunk: int a = 0;**

   Válasz: egész literált meglehet adni 8,16 és 2 számrendszerben is, a let és a var másik programozási nyelv. bár a var az létezik itt is talán

### Melyik nem primitív típus? TÍPUS

1. **String**
2. int
3. char
4. double

### Melyik primitív típus? TÍPUS 

1. **double**
2.  Dog
3.  Object
4.  String

### Melyik primitív típus? TÍPUS

1. **char**
2. Integer
3. String
4. Boolean[]

### Az int mérete

1. 8 bit
2. 16 bit
3. **32 bit**
4. 64 bit

### Melyik állítás hamis az alábbiak közül?

1. Az Integer.MAX_VALUE statikus változó tárolja az Integer típusú változók legnagyobb lehetséges értékét
2. **Véletlenszámot a Random.nextInt(100) metódushívás ad vissza**
3. A PI értékét a Math.PI konstans tárolja
4. Két szám közül a nagyobbat a következő hívás adja vissza: Math.max(a, b)');

## Öröklődés, abstract, interface

### Mely deklaráció fordul le? ABSTRACT

1. public abstract class Canine { public void speak(); }

2. public class Canine abstract { public abstract void speak(); }

3. public class Canine { public abstract void speak(); }

4. **public abstract class Canine { public void speak(){ } }**

   Válasz:

   1. hiányzik abstract a metódusból
   2. abstract a class előtt van fordítási hiba amúgy jó lenne
   3. nem abstract a class
   4. Ez a jó hisz a metódus nem absztrakt és van törzse (jelen esetben ez üres)

### Melyik nem igaz az absztrakt osztályokra? ABSTRACT

1. Lehetnek példányváltozóik.
2. Nem példányosíthatók.
3. **Csak absztrakt metódusaik lehetnek.**
4. Lehetnek absztrakt metódusaik.'



### Válaszd ki a Building osztály House alosztályának megfelelő definiálását! ÖRÖKLŐDÉS

1. **public class House extends Building {}**
2. public subclass House extends Building {}
3. public class House subclass of Building {}
4. public class Building.House {}



### Az alábbiak közül melyik igaz az absztrakt osztályokra?

1. **Származhatnak egy másik absztrakt osztályból.**
2. Nem lehetnek példányváltozóik.
3. Absztrakt osztályból való leszármazáshoz az implements kulcsszót használjuk.
4. Csak absztrakt metódusokat tartalmazhatnak.

### Adottak a következő állítások. Az A és E osztály. A B és D interfész. A C absztrakt osztály. IMPLEMETS EXTENDS

Melyik helytelen a következő megadások közül?

1. class F implements B { }

2. **class F extends A, E { }**

3. class F extends E { }

4. class F implements B,D { }

   Válasz: Java-ban csak egyszeres öröklődés van

### Melyik helyes deklaráció interfészen belül? INTERFACE

1. **public void doMore(long bow);**

2. public void doMore(long bow) {}

3. private short hop = 23;

4. public Name();

   Válasz:

   1. helyes
   2. metódus törzs nem kell
   3. private változó nem lehetséges
   4. visszatérési tipus kell, nincs konstruktor

### Melyik módosító nem alkalmazható az interfészekben definiált változókon? INTERFACE

1. public
2. final
3. static
4. **abstract**

### Melyik állítás igaz?

1. Egy interfész tartalmazhat nem final változókat.

2. Egy osztály csak egy interfészt implementálhat.

3. **Egy absztrakt osztály tartalmazhat nem final változókat.**

4. Az extends kulcsszóval jelöljük, ha egy osztály megvalósít interfészt.

   Válasz:

   1. interface alapból public final
   2. bármennyi interface lehet
   3. abstrakt lehet final meg nem final
   4. implements kulcsszó


## String
### Melyik típus a leginkább alkalmas szöveg tárolására?

1. **String**
2.  char
3. Integer
4.  Character

### Mely állítás igaz a String osztályra?

1. Hosszát a size() metódussal lehet lekérni

2. **Állapota nem módosítható**

3.  A toUpperCase() metódus az objektum állapotát módosítja úgy, hogy a kisbetűket nagybetűkre cseréli

4.  Értéke nem lehet null

   Válasz: a String immutable, méretét a .length(), toUpperCase() objektum állapotát nem módosítja hisz immutable

### Válaszd ki, hogy melyik értékadás a helyes!

1.  String s = 5;

2. String s = '5';

3.  **String s = "";**

4.  String s = (String) 5;

   Válasz: 5 az int, '5' az char, ilyen meg nem létezik (String)

### Melyik kód megfelelő Java String-ek összehasonlítására?

1.  s1 = s2
2.  s1 == s2
3.  **s1.equals(s2)**
4. Mindhárom

### Hogyan hasonlítunk össze String értékeket?

1. Mindig az == operátorral.
2. Az attól függ. Bizonyos esetekben a == operátorral.
3. **Mindig az equals() metódussal.**
4. Csak ha az egyik oldal literál, akkor kell az equals() metódust alkalmazni.

### Mit ír ki az alábbi kódrészlet?
String s = "dog";
s.toUpperCase();
System.out.println(s);

1.  **dog**

2.  DOG

3.  Nem fordul le

4.  Üres string-et

   Válasz: immutable .toUC nem változtat az objektumon
   
### Hogyan lehet egy szövegben sortörést elhelyezni?
1.  Csak System.out.println() használatával
2.  **String s = "a\nb";**
3.  String s = "a\BRCRb";
4.  String s = "a" + \n + "b";
5. Válasz: "\n"-nel lehet, 3,4 nem fordul le



### Ha String word = "banana", akkor melyik kifejezés adja vissza az első a betű helyét?

1. **word.indexOf("a")**
2.  word.charAt(2)
3.  word.lastIndexOf("a")
4.  indexOf(word, "a")

### Ha String word = "papaya", akkor melyik kifejezés adja vissza az utolsó p betű helyét?

1. **word.lastIndexOf("p")**
2. word.indexOf("p")
3. lastIndexOf(word, p)
4. word.charAt(2)

### Mit ír ki az alábbi kódrészlet?

System.out.println("apple".substring(2, 4));

1. **pl**
2. ppl
3. pp
4. ple

### Mit ír ki az alábbi kódrészlet?

String s = null;

System.out.println("foo".equals(s));

1. Nem fordul le

2. NullPointerException keletkezik

3. true

4. **false**

   Válasz ha fordítva lenne akkor nullpointer lenne

### Mit ír ki a következő kódrészlet?

```java
String s = null;
s = "foo";
s.toUpperCase();
System.out.println(s);
```

1. Nem fordul le, mert a második sorban értékadás van, és a String immutable

2. **foo**

3. FOO

4. Hiba futás közben

   Válasz: String immutable

## Enum

### Mi az enum?

1. **Egy típus, előre felsorolt konstansok tárolására.**
2.  Memória címek felsorolása.
3.  A hét napjainak felsorolása.
4. Egy típus, előre felsorolt változók tárolására

### Melyik hamis a felsorolásos típusokkal kapcsolatban?
1. A felsorolásos típus elemeihez egy egész szám van rendelve
2.  String alapján is lehet a felsorolásos típus egy elemét elkérni
3.  switch szerkezetben használható
4.  **Felsorolásos típusnak nem lehet konstruktora**

### Melyik utasítással lehet végigmenni a felsorolásos típus elemein?
public enum Day {
FIRST, SECOND
}

1.  for (Day day: Day) {}
2.  **for (Day day: Day.values()) {}**
3.  for (Day day : Day.items()) {}
4.  for (Day day: Day.values) {}

### Amennyiben van egy s String típusú változó, hogyan alakítjuk át enum típussá?

1. **Weekdays w = Weekdays.valueOf(s);**
2. Weekdays w = (Weekdays) s;
3.  Weekdays w = new Weekdays(s);
4.  Weekdays w = s;

### Az alábiak közül melyik követi az enum értékek felsorolásának konvencióját?

1. Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
2. monday, tuesday, wednesday, thursday, friday, saturday, sunday
3. "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY", "SATURDAY", "SUNDAY"
4. **MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY**

## Kollekciók, tömb

### Milyen módon hivatkozhatunk az int[] numbers tömb első elemére? TÖMB

1. **numbers[0]**
2. numbers(0)
3.  numbers[1]
4.  numbers(i)

### Melyik utasítással lehet egy ötelemű tömböt definiálni? TÖMB

1.  **int[] x = {0, 1, 2, 3, 4};**

2. int[4] x;

3.  int array[] = int{5};

4.  int array[5] = new int[];

   Válasz: 2 nincs ilyen fordítási hiba, 3 egy elemű tömb, 4 fordítási hiba

### Mit ír ki az alábbi kódrészlet? TÖMB
int[] i = {1, 2, 3, 4};
System.out.println(i[4]);

1.  Nem fordul le

2.  0

3.  4

4. **IndexOutOfBoundsException kivétel keletkezik**

   Válasz: indexelés 0-tól kezdődik

### Mit ír ki az alábbi kódrészlet? TÖMB

```java
final int i
    i = 3;
int[] n = {1, 2, 3};
System.out.println(n[i]);
```

1. Nem lehet final változónak értéket adni.

2. **ArrayIndexOutOfBoundsException kivétel**

3. 3

4. 0

   Válasz. indexelés

### Mit ír ki az alábbi kódrészlet? TÖMB
`int[][] i = new int[3][3];`
`System.out.println(i[2][2]);`

1. Nem fordul le

2.  **0**

3.  2

4.  IndexOutOfBoundsException kivétel keletkezik

   Válasz: mindig kapnak kezdő értéket int -> 0, double -> 0.0, boolean -> false, referenciánál -> null;

### Mit ír ki az alábbi kódrészlet?

```java
int[] n = {1, 2, 3};
for (int i: n) {
    System.out.println(i);
}
```

1. **Sortöréssel elválasztva: 1 2 3**
2. Sortöréssel elválasztva: 0 1 2
3. Sortöréssel elválasztva: 0 0 0
4. Sortöréssel elválasztva: 3 3 3

### Milyen módon lehet egy listát feltölteni elemekkel? LISTA

1.  List names = {"Joe", "John"};

2.  **List names = Arrays.asList("Joe", "John");**

3. List names = new List

4. List names = new ArrayList

   Válasz: 1 fordítási hiba, 3-4 nem tölt fel listát



### Mit ír ki az alábbi kódrészlet? LISTA

```java
List<String> names = new ArrayList<>();
names.add("John Doe");
names.add("John Doe");
System.out.println(names.length);
```

1. 1
2. **Nincs length attribútuma, csak metódusa, ezért nem fordul le.**
3. 2
4. Nincs length attribútuma, csak metódusa, ezért 0.

### Melyik állítás hamis a következők közül? TÖMB,LISTA
1.  A következő utasítás egy üres listát hoz létre: List names = new ArrayList
2. **A lista elemeit a következőképp adhatjuk meg: List names = {"Joe", "Jane"};**
3.  A lista mérete a size() metódussal kérdezhető le
4.  A listába új elemeket lehet hozzáadni, és elemeket lehet törölni

### Az alábbiak közül melyik állítás igaz? LISTA

1. **Több elemet egyszerre törölni a List names-ből az names.removeAll(namesToRemove) metódussal**
   **lehet, ahol az namesToRemove a törlendő elemek listája.**
2.  Az ArrayList belsejében egy tömb van, ezért a tömbökhöz hasonlóan előre meg kell adni a méretét
   létrehozáskor.
3.  Az List names legelső elemét az names.get(1) metódussal lehet elkérni.
4.  Bármilyen típusú érték kerülhet egy ArrayList-be, például: `ArrayList<int> integers = new ArrayList<>()`


### Melyik hamis a következő állítások közül? MÉRET
1.  A tömb mérete a következőképp kérdezhető le: names.length

2.  A String hossz a következőképp kérdezhető le: name.length()

3.  **Egy lista mérete a következőképp kérdezhető le: names.length()**

4.  A tömb és a lista indexelése nullától kezdődik

   Válasz: .size()

### Melyik állítás igaz a következők közül? Tömb,Lista
1. A tömb második eleméhez hozzáférhetünk a következő módon: names.get(1)

2.  A lista harmadik eleméhez hozzáférhetünk a következő módon: names.get(3)

3.  **A lista kiírása esetén (System.out.println) a lista elemei vesszővel elválasztva kerülnek kiírásra (toString metódus tehát helyesen implementált)**

4.  A tömb contains() metódusával lehet megnézni, hogy egy elem szerepel-e a tömbben

   Válasz: 1 helyesen names[1], 2 az a 4. elem, 4 contains() nincs a listánál

### Válaszd ki a következő programrészletre igaz állítást! LIST PRIMITIVTIPUS
```java
List<int> numbers = new ArrayList<>();
numbers.add(0);
numbers.add(1);
numbers.add(2);
```

1. **Nem lehet primitív típussal listát létrehozni.**
2. Autoboxing történik.
3. Autoboxing nélkül is működik, a lista hossza 3.
4. Mind a két oldalt a List szónak kell állnia a példányosítás miatt.

### Milyen metódusokat lehet meghívni a list változón, ha a következőképpen definiáljuk?

```java
List<SomeClass> list = new ArrayLst<>();
```

1. Csak az Object osztály metódusait.
2. **Csak a List interfész metódusait**
3. Csak az ArrayList osztály metódusait.
4. Csak a Collection interfész metódusait.

### Hogyan járjuk be egy lista elemeit? LISTA BEJÁRÁS
1. **for (String s: list) {System.out.println(s);}**
2. for (String s in list) {System.out.println(s);}
3. for each (String s: list) {System.out.println(s);}
4.  for (int i = 0; i



### Az alábbiak közül melyik nem implementálja a Collection interfacet-t? COLLECTION

1. **Enum**
2. HashSet
3. ArrayList
4. LinkedList

### Melyik Collection implementációt célszerű választanunk, ha gyakran kell elemeket hozzáadni vagy eltávolítani, azonban ritkábban index szerinti elérésre is szükség lehet, és egy elemet lehet, hogy többször is fel akarunk venni? LIST 

1. **LinkedList**
2. HashMap
3. HashSet
4. ArrayList

### Melyik Collectionre nem igaz, hogy a benne levő elemeket ki tudom venni a hozzáadás sorrendjében? COLLECTION

1. LinkedList
2. ArrayDeque
3. **HashSet**
4. LinkedHashSet

### Milyen metódusa nincs a Collection interfésznek? COLLECTION

1. **get(K key)**
2. size()
3. add(E element)
4. iterator()

### Miért okoz fordítási hibát az alábbi kódrészlet? COLLECTION

```java
List<HashMap<Queue<Boolean>, ArrayList<Set<double>>>> mess;
```

1. A List interfész, helyette valamilyen azt implementáló osztályt kell megadni
2. A kódrészlet nem okoz fordítási hibát
3. Kollekciókat nem lehet ilyen mélyen egymásba ágyazni
4. **Nem lehet primitív típust megadni típusparaméternek**

### Mit ír ki? COLLECTION

```java
public class Main {
    public static void main (String[] args) {
        Map<String, String> someMap = new HashMap<>();
        someMap.put("someKey","someValue");
        someMap.put("someKey","someOtherValue");
        System.out.print1n(someMap.size() + someMap.get("someKey"));
    }
}
```

1. Futásidőben exception keletkezik, mivel a someKey kulcs már szerepel a mapben, ezért nem lehet újra felvenni.
2. 2someOtherValue
3. **1someOtherValue**
4. 1someValue

## Kivételezés
### Melyik igaz a kivételkezelésre?
1.  Csak beépített kivételeket használhatunk

2.  A keletkezett kivételt minden esetben kezelnünk kell a metódusban

3.  **A kivételt tovább dobhatjuk a hívónak**

4.  Az összes kivétel unchecked kivétel

   Válasz: lehet saját kivételt használni, tovább lehet dobni a kivételt, kivételek lehetnek checked is

### Melyik nem a kivétel kezeléshez kapcsolódó kulcsszó?

1. **final**
2. try
3.  catch
4.  throws

### Hogyan dobható Exception kézzel?

1. **throw new MyException();**
2. throw MyException;
3. throws new MyException();
4.  throws myException;

### Mi a különbség az Exception és az Error közt?

1. **Az Exception olyan szituációt reprezentál, ami "megoldható", míg az Error általában olyan hibát jelent, ami után nem folytatható a program futása**

2. Az Error olyan szituációt reprezentál, ami "megoldható", míg az Exception általában olyan hibát jelent, ami után nem folytatható a program futása.

3. Az Error nem a Throwable osztályból származik, míg az Exception igen.

4. Az Exception nem a Throwable osztályból származik, míg az Error igen.

   Válasz: Error és a Exception is Throwable

### Mi a különbség a checked és az unchecked exception között?

1. Ha saját exceptiont írunk, az csak checked exception lehet, unchecked nem.

2. A catch blokk nem kapja el az unchecked exceptiont, hiszen ez jellemzően rendszerhiba.

3. **A checked exceptionnél a program fordításakor ellenőrzi a compiler, hogy felkészültünk-e rá, és ha nem, akkor fordítási hibát kapunk.**

4. Unchecked exception esetén a try-catch-finally-nél a finally ág nem hajtódik végre.

### Mit ír ki a következő kód?
```java
public class TestException {
    public void throwException() {
        System.out.print("throwex ");
        throw new RunTimeException();
    }
    public static void main(String[] args) {
        try {
            System.out.print("try");
            new TestException().throwException();
        } catch (Exception re) {
            System.out.print("catch ");
        } finally {
            System.out.print("finally ");
        }
        System.out.println("done");
    }
```

   

1. try throwex catch done
2. try throwex finally done
3. **try throwex catch finally done**
4. Futási idejű hibával megáll a program futása.



### Melyik deklaráció írja le, hogy a metódus NullPointerException és IOException kivételt is dobbat?

1. public void print() throw NullPointerException | IOException
2. public void print() throws NullPointerException | IOException
3. public void print() throw NullPointerException throw IOException
4. **public void print() throws NullPointerException, IOException');**



### Mit ír ki az alábbi Java kód?

```java
public class Test {
    public void doSomething() {
        throw new RuntimeException();
    }
    public static void main(String[] args) {
        try {
            new Test().doSomething();
        }
        catch (Throwable t) {
            System.out.println("Yupp");
        }
    }
}
```

1. Nem fordul le, mert a doSomething() metódus nem definiálja a fejben (method header) a RuntimeException kivételt (exception)
2. **Yupp**
3. Az alkalmazás leáll, mert nem kezelt kivétel (unchecked exception) keletkezik
4. Nem ír ki semmit, az alkalmazás hiba nélkül lefut');

## KÓDRÉSZLET
### Mit ír ki az alábbi kódrészlet? OSZTÁLY HÍVÁS

```java
public class Incrementer {
    
    public int inc(int i) {
	return i + 1;
	} 
    
public static void main(String[] args) {
int i = 5;
System.out.println(inc(i));
}
}
```

1.  **Nem fordul le**

2.  5

3.  6

4. Kivételt dob

   Válasz: new Incrementer.int(i) esetben fordult volna le, amugy fordítási hiba
   
### Mit ír ki az alábbi kódrészlet? KONSTRUKTOR
```java
public class WithName {
private String name;
public WithName(String name) {
name = name;
}
public String getName() {
return name;
}
public static void main(String[] args) {
WithName withName = new WithName("Joe");
System.out.println(withName.getName());
}
}
```
1.  Nem fordul le

2.  **null**

3. Joe

4.  IllegalArgumentException kivétel keletkezik

   Válasz: a konstruktorban nem a attribútumnak állítottuk be az értékét, igy maradt az alapértelmezett értéke ami null. Helyesen this.name = name.

### Mit ír ki az alábbi kódrészlet? PARAMÉTERÁTADÁS PRIMITIV TÍPÚS
```java
public class Incrementer {
public void inc(int i) {
i++;
}
public static void main(String[] args) {
int i = 5;
new Incrementer().inc(i);
System.out.println(i);
}
}
```
1.  **5**

2.  6

3.  Nem fordul le

4.  Kivételt dob

   Válasz: azért nem 6 mivel javában értékszerinti paraméter átadás van, és a primitivnél nincs visszahatás.

### Mi az értéke a következő kifejezésnek? OR OPERATOR
(3 > 5) || (1/0 == 0)

1.  true

2.  false

3.  **java.lang.ArithmeticException hiszen nullával való osztás van**

4.  0

   Válasz: ha 3<5 lenne akkor true lenne!!!

### Melyik kódrészlet nem helyes? + OPERÁTOR
1.  int a = 0; int b = 1; int c = a + b;

2.  Integer a = 0; Integer b = 1; Integer c = a + b;

3.  **BigInteger a = new BigInteger(0); BigInteger b = new BigInteger(1); BigInteger c = a + b;**

4.  String a = "0"; String b = "1"; String c = a + b;

   Válasz:a.add(b);

### Melyik értékadás helyes az alábbiak közül? KONVERZIÓ CASTOLÁS
1.  byte b = 300;

2.  long k = 10; int i = k;

3.  **long k = 10; int i = (int) k;**

4. long l = 2.5;

   Válasz: 1 fordítási hiba, ha castolnánk akkor 300-256=44 lenne, 2 fordítási hiba: castolni kell, 4 fordítási hiba ha castolnánk akkor 2 lenne

### Mit ír ki az alábbi kód? TÖMB WHILE
```java
public static void main(String[] args) {
int []a = {1,2,3,4,5,6};
int i = a.length - 1;
while(i>=0){
System.out.print(a[i]);
i--;
}
}
```
1.  123456
2.  **654321**
3.  65432
4.  IndexOutOfBoundsException

### Mit ír ki az alábbi kód? SCOPE
```java
public static void main(String[] args) {
for(int i = 0; i <= 5; i++){
System.out.print(i);
}
System.out.print(i);
}
```
1.  012345

2.  0123455

3.  **Nem fordul le**

4. IndexOutOfBoundsException

   Válasz: nem látja az i-t

### Mit ír ki az alábbi kód? SWITCH
```java
String s = "aaa";
switch (s) {
case "bbb":
System.out.print("3b");
case "aaa":
System.out.print("3a");
case "ccc":
System.out.print("3c");
}
```
1.  Nem fordul le, hiszen String van a switch
   feltételben

2.  3a

3.  **3a3c**

4. Kivétel keletkezik

   Válasz: mivel nincs break ezért tovább megy a következőre

### Mit ír ki a következő kódrészlet? SWITCH

```java
String s = "2";
switch (s) {
    case "1":
        System.out.print("one ");
    case "2":
        System.out.print("two ");
    case "3":
        System.out.print("three ");
    default:
        System.out.print("booo ");
}
```

1. Nem fordul le, mert switch szerkezetnél nem használható String

2. two

3. **two three booo**

4. two three;

   Válasz: break hiánya miatt

### Mennyivel tér vissza az alábbi metódus, ha a következőképp hívjuk boolean isValid = isValidNumber("5");?
```java
public boolean isValidNumber(String number) {
try {
int value = Integer.parseInt(number);
if (value < 0 && value > 10) {
return true;
}
return false;
} catch (NumberFormatException nfe) {
return false;
}
}
```
1.  true
2.  **false**
3.  NumberFormatException keletkezik a hívás helyén
4.  Nem fordul le a kód

### Adott az alábbi kódrészlet: IMMUTABLE PARAMÉTER ÁTADÁS
```java
private String name;
private List<String> courses;
public TrainerData(String name, List<String> courses) {
this.name = name;
this.courses = new ArrayList<>(courses);
}
public String getName() {
return name;
}
public List<String> getCourses() {
return courses;
}
}
```
Melyik hamis az alábbi állítások közül?

1.  A TrainerData osztály name attribútuma osztályon kívülről módosítható, ugyanis nincs final módosítószóval ellátva

2.  A TrainerData immutable, még a courses lista tartalma sem változtatható kívülről

3.  A name attribútum módosítható, 
   pl. így: new TrainerData("John Doe", Arrays.asList("Biology")).getName().toUpperCase();

4. **Mindhárom hamis**

   Válasz:1 hamis, mivel nincs setter és private, 2 hamis mivel a referenciáját nem változhatom de  tartalmát igen trainerData.courses.add("sör"); megoldás új referenciaként visszaadni, 3 hamis String immutable

### Mit ír ki az alábbi kódrészlet? THIS VISSZATÉRÉSI ÉRTÉK
```java
public class WithName {
private String name;
public WithName(String name) {
this.name = name;
}
public void modifyName(String name) {
return this.name;
}
public static void main(String[] args) {
System.out.println(new WithName("John Doe").modifyName("Jack Doe"));
}
}
```
1.  John Doe

2. Jack Doe

3. null

4. **Nem fordul le**

   Válasz: modifíName() az void de közben vissza add egy Stringet. Helyesen public String  modifíName()

### Mit ír ki az alábbi kódrészlet?
```java
public class Numbers {
public String addFive(String s) {
return s + 5;
}
public static void main(String[] args) {
System.out.println(new Numbers().addFive(10));
}
}
```
1.  105

2.  15

3.  **Nem fordul le**

4.  Futás közben kivételt dob

   Válasz: 10 az int és nem String. helyesen "10";

### Mit ír ki az alábbi kódrészlet? STRING LIST IMMUTABLE
```java
public class NameConverter {
public void convertNames(String name, List<String> otherNames) {
name = name.toUpperCase();
for (int i = 0; i < otherNames.size(); i++) {
otherNames.set(i, otherNames.get(i).toUpperCase());
}
}
public static void main(String[] args) {
String name = "John Doe";
List<String> names = new ArrayList<>(Arrays.asList("Jane Doe"));
new NameConverter().convertNames(name, names);
System.out.print(name);
System.out.print(" ");
System.out.print(names);
}
}
```
1.  **John Doe [JANE DOE]**

2.  JOHN DOE [JANE DOE]

3.  John Doe [Jane Doe]

4.  [John Doe, Jane Doe]

   Válasz: String immutable, a list tartalmán lehet változtatni

### Mit ír ki az alábbi kódrészlet? RETURN
```java
public class NameConverter {
public String convertName(String name) {
if (name.equals("")) {
return;
}
return name.toUpperCase();
}
public static void main(String[] args) {
System.out.println(new NameConverter().convertName(""));
}
}
```
1.  **Nem fordul le**

2.  Üres string, azaz ""

3.  null

4. Futás közben hiba keletkezik

   Válasz: nincs visszatérési érték.
   
### Mit ír ki az alábbi kódrészlet? Bejárás
```java
public List<Course> createCourses(String... names) {
List<Course> courses = new ArrayList<>();
// Bejárás
}
```
Melyik a helytelen módja a paraméterek bejárásának?

1.  for (String name: names) { courses.add(new Course(name)); }

2. **for (int i = 0; i< names.length; i++) { courses.add(new Course(names.get(i))); }**

3.  for (int i = 0; i< names.length; i++) { courses.add(new Course(names[i])); }

4.  Egyik megadási mód sem helyes

   Válasz: .get() listánál van

### Mit ír ki az alábbi kódrészlet? THIS
```java
public class Builder {
private String name;
public Builder setName(String name) {
this.name = name;
return this;
}
public String build() {
return name;
}
public static void main(String[] args) {
System.out.print(new Builder().build());
System.out.print(" ");
System.out.print(new Builder().setName("John Doe").setName("Jack Doe").build());
}
}
```
1. Nem fordul le
2. **null Jack Doe**
3. Jack Doe
4. null John Doe



### Adott az alábbi kódrészlet. STATIC METHOD
```java
public class Concatenator {
public static String convert(int a, int b) {
return Integer.toString(a) + Integer.toString(b);
}
public static void main(String[] args) {
// ???
}
}
```
A main metódusból hogyan lehet meghívni a convert metódust?

1.  Csak a Concatenator.convert(5, 6); utasítással
2.  Csak a convert(5, 6); utasítással
3.  Csak a new Concatenator().convert(5, 6); utasítással
4.  **Mindhárom utasítással, de nem mindegyik javasolt**

### Mit ír ki az alábbi kódrészlet? STATIC ATTRIBUTUM
```java
public class State {
private static int instance = 0;
public State() {
instance ++;
}
public static void main(String[] args) {
new State();
new State();
System.out.println(instance);
}
}
```
1.  Nem fordul le
2.  0
3.  1
4.  **2**

### Mit ír ki az alábbi kódrészlet? Feltételezzük, hogy a két osztály két külön .java fájlban van deklarálva, a megfelelő könyvtárakban. STATIC IMPORT
```java
package foo;
public class Foo {
public static int value = 10;
}
package bar;
import static foo.Foo;
public class Bar {
public static void main(String[] args) {
System.out.println(value);
}
}
```

1.  **Nem fordul le**

2. 10

3. 0

4. Futás közben hiba

   Válasz: Helyesen inport static foo.Foo.value vagy wildcar

### Adott a következő kódrészlet: KONSTRUKTOR
```java
public class Trainer {
private String name;
public Trainer(String name) {
this.name = name;
}
}
```
Mely állítás hamis az alábbiak közül?

1.  **Az osztály példányosítható a következő módon:**
   **Trainer t = new Trainer();**

2.  Az osztály példányosítható a következő módon:
   Trainer t = new Trainer("Anonymous");

3. Az osztály példányosítható a következő módon:
   Trainer t = new Trainer(null);

4. Nem kerül legenerálásra paraméter nélküli implicit konstruktor, hiszen van explicit konstruktor

### Adott a következő kódrészlet: KONSTRUKTOR
```java
public class Trainer {
private String name;
private int age;
public Trainer(String name) {
this(name, 0);
}
public Trainer(String name, int age) {
this.name = name;
this.age = age;
}
}
```
Az alábbi konstruktorok melyik nem illeszhető be a fenti osztályba harmadik konstruktorként?

1.  public Trainer() {this(null, 0);}

2.  public Trainer() {super();}

3.  **public Trainer() {String name = "anonymous"; this(name);}**

4.  public Trainer(int age) { this(null, age); }

   Válasz: this mindig a legelső

### Mit ír ki az alábbi kódrészlet? ÖRÖKLŐDÉS KONSTRUKTOR
```java
class A {
String s = "-";
protected A() { this("d"); s += "a"; }
private A(String e) { s += "d"; }
}
class B extends A {
B() { super(); s += "b"; }
}
class C extends B {
C() { s += "c"; }
public static void main(String... boo) {
System.out.println((new C()).s);
}
}
```
1.  **-dabc**

2.  -abc

3.  -adbc

4.  -cba

   Válasz: Konstruktorok nem öröklődnek, mindig az ős konstruktor hivódik meg előszőr vagyis C() -ben van egy rejtett super() ezért meghivja B() ami meghivja protected A()-at ami meg private A()-t igy akkor -+d+a+b+c = -dabc 

### Mit ír ki az alábbi kódrészlet? INSTANCEOF
```java
class Ex1 {
public static void main(String[] args) {
int a[] = { 1,2,3,4}; // 1
System.out.print(a instanceof Object); // 2
}
}
```
1.  **true**

2. false

3. Nem fordul le az egyessel jelölt sor

4. Nem fordul le a kettessel jelölt sor

### Adott a következő kódrészlet: ÖRÖKLŐDÉS LÁTHATÓSÁG
```java
public class Human {
private String name;
}
```
Ha létrehozunk egy leszármazottat (Trainer extends Human), melyik állítás hamis?

1.  Leszármazottban elérhető a name attribútum, ha a Human osztályban protected láthatósági módosítóval látjuk el

2. Definiáljunk egy publikus gettert az attribútumnak, és akkor a leszármazottban is hozzá lehet férni a getterrel

3.  **A super.name hívással is hozzá lehet férni a leszármazottban**

4.  A protected módosítószó a package private kiterjesztése, használatakor nem csak az azonos csomagban lévő osztályok, hanem bármely leszármazott eléri az adott tagot

   Válasz: 1 igaz, 2 igaz, 3 hamis private nem látjuk, 4 igaz

### Adott a következő kódrészlet: ÖRÖKLŐDÉS
```java
class Mid {
public int findMid(int n1, int n2) {
return (n1 + n2) / 2;
}
}
public class Calc extends Mid {
public static void main(String[] args) {
int n1 = 22, n2 = 2;
// Egészítsd ki
System.out.println(n3);
}
}
```
Mit kell a megjegyzés helyére írni, hogy 12 értéket írja ki?

1.  **Calc c = new Calc(); int n3 = c.findMid(n1,n2);**

2.  int n3 = super.findMid(n1,n2);

3.  Calc c = new Mid(); int n3 = c.findMid(n1, n2);

4. int n3 = this.findMid(n1,n2);

   Válasz: 1 mivel public és nincs felülirva ezért látja, 2 nem fordul le, 3 se fordul le, 4 se fordul le

### Adott az alábbi kódrészlet: ÖRÖKLŐDÉS
```java
class Plant {
String getName() { return "plant"; }
Plant getType() { return this; }
}
class Flower extends Plant {
// Hiányzó kód
}
class Tulip extends Plant { }
```
Melyik sor nem illeszthető a hiányzó kód helyére?

1. Tulip getType() { return new Tulip(); }

2. Plant getType() { return this; }

3. **Object getType() { return this; }**

4. Flower getType() { return this; }

   Válasz:

    1 Tulipán típust vár vissza tulipánt kap vissza,

    2 Plant típust vár vissza Flower egy Plant

   3 Objectet vár vissza, Flowert kap fordítási hiba

   4 Flowert vár vissza Flowert kap

### Adottak a következő kódrészletek. ABSTRACT INTERFACE

```java
abstract class X {
public abstract void methodX();
}
interface Y {
}
```

Melyik kódrészlet helytelen?

1. **class Z extends X implements Y { public void methodZ(); }**

2. abstract class Z extends X implements Y { public void methodZ() {} }

3. class Z extends X implements Y { public void methodX() {} }

4. abstract class Z extends X implements Y { }

   Válasz:

   1. nem fordul le methodX() nincs felülírva vagy az osztály abstractá téve
   2. jó abstract ezért nem kötelező felülírnia
   3. felül van írva
   4. jó abstract ezért nem kötelező felülírnia



### Adott a következő kódrészlet. Melyik sort kell beilleszteni a komment helyére, hogy true értéket írjon ki? 

```java
public class Bird extends Animal implements CanFly {}
public interface CanFly {}
public abstract class Animal {}
public class AnimalService {
    public static void main(String[] args) {
        Bird bird = new Bird();
        // 
    }
}
```

1. System.out.print(bird.instanceof(CanFly.class))

2. **System.out.print(bird instanceof CanFly)**

3. System.out.print(bird instanceof CanFly.class)

4. System.out.print(bird.instanceof(Animal))

   Válasz

   1. .instanceof helytelen a zárójelezés is .class nem kell
   2. ok
   3. .class nem kell
   4. .instanceof helytelen .class nemm kell zárójel se kell amugy true lenne



### Mit ír ki az alábbi kódrészlet? SCOPE

```java
int i = 5;
if (i % 2 != 0) {
    String value = "Odd";
}
System.out.println(value);
```

1. **Nem fordul le.**
2. Odd
3. null
4. Futás közben hibával leáll.



### Mit ír ki az alábbi kódrészlet? CIKLUS

```java
for (int i = 3; i >=0; i--) {
    System.out.println(i);
}
```

1. **Sortöréssel elválasztva: 3 2 1 0.**
2. Sortöréssel elválasztva: 3 2 1.
3. Sortöréssel elválasztva: 2 1 0.
4. Nem fordul le.
























