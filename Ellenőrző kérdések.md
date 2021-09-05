# Ellenőrző kérdések

## Szoftvertesztelés JUnit használatával

### Bevezetés a JUnit használatába

- Definiáld a unit teszt fogalmát!
  * Az adott programozási nyelv legkisebb egységét tudjuk tesztelni. OOP esetén az osztály a legkisebb egység. Hiszen hogy vizsgálni tudjuk a metódus működését, először példányosítani  kell egy objektumot az adott osztály alapján.
- Milyen struktúrát érdemes követni egy teszteset megírásakor?
  * Given-fázis: tartalmazza a előfeltételeket, itt előkészítjük az adott teszt eseteket, pédányosítjuk az objektumot, beállítjuk annak megfelelő állapotára
  * When-fázis meghívjuk a tesztelendő metódust
  * Then-fázis megnézzük, hogy a kapott eredmény megfelel-e az álltalunk elvárt eredménynek 
- Milyen annotációval kell ellátnunk a metódusainkat, illetve milyen beállítást kell elvégezni az alkalmazáson, hogy a teszteseteket működésre bírjuk?
  * Junit-ot fel kell venni teszt scopa-val
  * src/test/java könyvtárban helyezzük el a teszteseteket 
  * src/test/resources a teszt esethez tartozó erőforrásokat itt helyezzük el
  * @Test látjuk el a teszt metódusainkat

### Az első teszteset létrehozása

- Egy Maven projekt esetén hova kell helyezni a tesztosztályokat?
  * src/test/java könyvtárban helyezzük el a teszteseteket 
- Milyen elnevezési konvenciókat érdemes betartani tesztek írásánál?
  * A tesztosztály neve utaljon a tesztelendő osztály nevére, valamint az src/test/java könyvtáron belül ugyanolyan nevű csomagban helyezkedjen el, mint a tesztelendő osztály. A tesztosztály ugyanis csak így fogja “látni” a tesztelendő osztályt.
  * A tesztmetódus (teszteset) neve utaljon a tesztelendő metódus nevére, és ne legyen
    visszatérési értéke (void).
- Mi a helyzet a láthatósági módosítószavakkal?
  * nem kellenek hisz a tesztet senki se fogja kívülről meghívni

### Unit tesztelés ígéretei

- Sorolj fel a unit tesztelés hozadékaiból néhányat!
  * Fejlesztő írja, amikor az adott osztályt, ezért a hibák gyorsan kiderülnek, azonnal lehet javítani őket,igy nem megy el feleslegesen sok idő és energia a hiba keresésével
  * Támogatja a refactoringot, amikor az alkalmazásunkat csak strukturálisan változtatjuk és funkcionálisan nem.A refaktoring után is sikeresen le kell futniuk. Tehát igy ellenőrizhetjük, hogy valőjában is csak strukturális változás volt a kódban és nem funkciónális.
  * Regresszió biztosítása, azaz ha valami már egyszer működött, akkor a későbbi módosítások során is működőképes marad majd.
  * Segítségül lehet hívni a unit tesztelést hibajavítás közben is. Először unit teszttel reprodukáljuk a hibát, majd csak utána kezdünk hozzá a javításhoz. Így biztosíthatjuk, hogy ez a hiba többet nem fog jelentkezni.
  * Ha egy komplex rendszerünk van sok unit teszttel, és egy későbbi módosítás során valamit elrontunk, akkor gyorsabban lehet rátalálni a hibás komponensre és javítani azt.
  * A unit tesztelés támogatja azt, hogy az alapvető objektumorientált paradigmákat betartsuk. High cohesion: egy adott osztály mindig egy jól meghatározott feladattal rendelkezik, és ezt a feladatot hiba nélkül meg is valósítja. Low coupling: az osztályok közötti kapcsolat laza, egy osztály nem függ túlságosan egy másiktól. A unit teszteket úgy érdemes megírni, mintha mi független felek lennénk és ezt az osztályt használni
    szeretnénk. Test Driven Development: úgy fejlesztünk, hogy előbb írjuk meg a teszteseteket és csak utána magát az osztályt. Ez is azt támogatja, hogy először kívülről nézzünk rá a saját, fejlesztendő osztályunkra, és azt olyanra tudjuk megírni, hogy akár mások által is könnyen használható legyen.
  * A unit tesztelés nagy előnye, hogy egyszerűsíti a fejlesztést. A hibák ezáltal hamarabb kiderülnek, vagyis a hibajavítás költsége jóval kevesebb. Egy bonyolult alkalmazás változtatása közben a tesztesetekkel lehet automatikusan ellenőrizni, hogy azok a funkciók, melyeket nem módosítunk,  nem romlottak-e el a módosítás hatására.
  * A unit teszt önmaga dokumentálja is a kódot, hiszen kiderül belőle az osztály működése, sőt, “élő dokumentációként” működik. Ugyanis amennyiben módosul az osztály, akkor nem kell külön észben tartani, hogy még a dokumentációt is módosítani kell. Erre ugyanis eleve rákényszerül a fejlesztő, hiszen a módosítás folytán a teszt eleve le sem fog fordulni vagy le sem fog futni.

### Futtatás Mavennel

- Miért tudja a Maven a teszteseteket futtatni?
  * A Maven beépítetten támogatja a JUnitot, méghozzá a Surefire plugin segítségével. A Maven egy életciklust definiál az adott projektekhez, amely különböző fázisokból áll.
- Sorold fel egy Maven projekt buildelésének életciklusait!
  * `validate` - validate the project is correct and all necessary information is available
  * `compile` - compile the source code of the project
  * `test` - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
  * `package` - take the compiled code and package it in its distributable format, such as a JAR.
  * `verify` - run any checks on results of integration tests to ensure quality criteria are met
  * `install` - install the package into the local repository, for use as a dependency in other projects locally
  * `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.
- Hogyan tudjuk csak a `test` életciklust futtatni IDEA-ban illetve parancssorból?
  * maven test

### Tesztesetek életciklusa

- Milyen annotációval kell ellátnom egy metódust, hogy minden egyes teszteset előtt lefusson?
  * @BeforeEach
- Hogyan lehet meghatározni a tesztesetek lefutási sorrendjét? Melyik ezek közül az alapértelmezett műkődés?
  * @TestMethodOrder annotávióval
    * MethodOrderer.Alphanumeric: itt a tesztesetek ábécé-sorrendben kerülnek lefuttatásra.
    *  MethodOrderer.OrderAnnotation: ekkor tehetünk a tesztesetekre @Order annotációt, amelyet egy egész számmal paraméterezhetünk, és sorrendben, a számok alapján fogja a JUnit lefuttatni a tesztmetódusokat.
    *  MethodOrderer.Random: véletlenszerű lefuttatás. A JUnit egyébként alapértelmezetten így futtatja a teszteseteket. Ezzel nagyon jól lehet azt is tesztelni, hogy a teszteseteink valóban függetlenek-e egymástól.
- Mi történik a tesztosztállyal minden egyes teszt lefutása előtt?
  * minden teszt előtt példányosítja az osztályt
- Mire kell figyelni amikor több tesztesetünk van egy osztályban?
  * függetlenek legyenek egymástól
- Milyen annotációval kell ellátni a teszt esetett, hogy a futtatókörnyezet ne futtassa le?
  * @Disabled

### Assert

- Milyen JUnit assert metódusokat ismersz?

  * assertNull() és assertNotNull(): a paraméterként átadott referenciát vizsgálja, hogy az null-e.

  *  assertEquals() és assertNotEquals(): használható primitív és referencia típusú paraméterekkel is. Két paramétert kell neki átadni, és azok egyezőségét vizsgálja. Primitív típusú paraméterek esetén megnézi, hogy azok konkrét értéke egyenlő-e (==). Referencia típusú paraméterek esetén meghívja azok equals() metódusát és ez alapján nézi az egyezőségüket. Lebegőpontos számok esetén a bináris számábrázolásból adódó pontatlanságok figyelembevételére megadható egy harmadik paraméter is, ahol megadhatjuk a hibahatárt, amin belül egyenlőnek kell tekinteni az elvárt és az aktuális értéket.

  * assertSame() és assertNotSame(): referenciákat hasonlít össze kifejezetten az == operátorral.

  *  assertTrue() és assertFalse(): ennek paraméterül egy boolean értékű kifejezést adhatunk át, és a teszteset akkor fut le sikeresen, ha ennek a kifejezésnek az értéke a metódus nevében szereplő értékkel egyezik meg.

  *  fail(): lehetséges az is, hogy explicit módon elbuktassuk a tesztesetet.

  *  assertArrayEquals(): két tömböt hasonlíthatunk össze.

  *  assertIterableEquals(): az Iterable interfész implementáló osztályok objektumainak összehasonlítására használható, vagyis tipikusan kollekcióknál használjuk. Végignézi, hogy ugyanazok az elemek szerepelnek-e a paraméterként átadott két kollekcióban.

  *  assertLinesMatch(): string listák összehasonlítására, de nem csak a pontos egyezőséget vizsgálja, hanem az elvárt értéknél megadhatunk például egy reguláris kifejezést is, és azt vizsgálja, hogy az aktuális érték ennek megfelel-e.

  *  assertAll(): egyszerre több assertXXX() kifejezést adhatunk neki át paraméterül (lambda kifejezésekben), és mindet kiértékeli attól függetlenül, hogy sikeres vagy sikertelen-e. Mindegyiknek az eredményét külön-külön megjeleníti.

    ```java
    assertAll(
    () -> assertEquals("John Doe", employee.getName()),
    () -> assertEquals(49, employee.getAge(2019))
    );
    ```

    

- Hogyan kell/lehet paraméterezni az `assertEquals()` metódust?

- Hogyan használható az `assertAll()` metódus?

- Pusztán JUnit használatával hogyan lehet tesztelni objektumokat tartalmazó kollekciókat?

### Kivételkezelés és timeout tesztelése

- Milyen metódust használunk annak eldöntésére, hogy a tesztelendő metódus dobott-e kivételt?

  * ```java
    IllegalArgumentException iae = assertThrows(
    IllegalArgumentException.class,
    () -> new Employee("John Doe", 1800));
    assertEquals("Invalid year: 1800", iae.getMessage());
    ```
  
- Hogyan tudom tesztelni, hogy a dobott kivétel a megfelelő hibaüzenetet dobta-e?

- Hogyan tudom tesztelni, hogy egy metódus a megfelelő időn belül futott-e le?

  * assertTimeout(ofMinutes(2), () -> employeeService.calculateYearlyReport());

### Egymásba ágyazás

- Hogyan tudjuk csoportosítani a teszteseteinket?
  * @Nested annotációval belső osztályokat hozzunk létre

### Tagek és metaannotációk

- A belső osztályokon kívül hogyan tudjuk a teszteseteket csoportosítani?

  * @Tag annotációval osztályra vagy akkár metódusokra is rakhatjuk

- Milyen beállítást kell elvégezni a `pom.xml`-ben hogy csak bizonyos annotációkkal ellátott tesztesetek fussanak le?

  * ```xml
    <plugin>
    	<artifactId>maven-surefire-plugin</artifactId>
    	<version>2.22.0</version>
    	<configuration>
    		<groups>unit</groups>
    	</configuration>
    </plugin>
    ```

- Mi az a metaanotáció?

  * az annotáció amit létrehozzunk, további annotációkat tartalmaz

### Tesztesetek ismétlése

- Milyen paramétereket lehet megadni a `@RepeatedTest` annotációnak?

  * 1 paraméter egész szám, hányszor ismételje a tesztet
  * 2 paraméter name: "Get age {currentRepetition}/{totalRepetitions}"

- Honnan tudhatjuk, hogy épp hányadik ismétlés zajlik a teszteset futtatásakor?

  * 2 paraméter name: "Get age {currentRepetition}/{totalRepetitions}"

- Hogyan tudjuk ezt kihasználni, hogy különböző expected - actual párokkal futtassunk egy tesztesetet?

  * ```java
    private int[][] values = {{2000, 0}, {2010, 10}, {2015, 15}, {2050, 50},
    {1990, -10}};
    @RepeatedTest(value = 5, name = "Get age
    {currentRepetition}/{totalRepetitions}")
    void testGetAge(RepetitionInfo repetitionInfo) {
    Employee employee = new Employee("John Doe", 2000);
    assertEquals(values[repetitionInfo.getCurrentRepetition() - 1][1],
    employee.getAge(values[repetitionInfo.getCurrentRepetition() - 1][0]));
    }
    ```

### Paraméterezett tesztek

- Milyen beállítást kell elvégezni a `pom.xml`-ben hogy paraméterezett teszteket tudjunk futtatni?

  * ```xml
    <dependency>
    	<groupId>org.junit.jupiter</groupId>
    	<artifactId>junit-jupiter-params</artifactId>
    	<version>5.5.1</version>
    	<scope>test</scope>
    </dependency>
    ```

- Milyen paramétereket lehet megadni a `@ValueSource` annotációnak?

  * ```java
    @ParameterizedTest
    @ValueSource(strings = { "racecar", "radar", "able was I ere I saw elba" })
    void palindromes(String candidate) {
    assertTrue(isPalindrome(candidate));
    }
    ```

  * ```java
    @EnumSource(value = TimeUnit.class, names = { "DAYS", "HOURS" })
    ```

  * ```java
    @ParameterizedTest(name = "year {0} - age {1}")
    @MethodSource("createAges")
    void testGetAge(int year, int age) {
    	Employee employee = new Employee("John Doe", 2000);
    	assertEquals(age, employee.getAge(year));
    }
    static Stream<Arguments> createAges() {
    	return Stream.of(
    		arguments(2000, 0),
    		arguments(2010, 10),
    		arguments(2050, 50),
    		arguments(1990, -10)
    	);
    }
    ```

  * ```java
    @CsvFileSource(resources = "/get-age.csv")
    ```

- Hogyan lehet megadni enumok értékeit paraméterezett teszteknek?

- A `@MethodSource` annotációval ellátott teszteknél milyen elvárás van a tesztesetek előállítását végző metódusra?

- Hogyan lehet CSV állományból betölteni teszt eseteket?

### Dinamikus tesztek

- Milyen annotációval kell ellátnom a dinamikus teszteket előállító metódust?

  * ```java
    @TestFactory
    Stream<DynamicTest> arePalindromes() {
    return Stream.of("racecar", "radar", "mom", "dad")
    .map(text ->
    dynamicTest(
    "Is palindrome? " + text,
    () -> assertTrue(isPalindrome(text))));
    }
    ```

- Milyen példányokat ad vissza ez a metódus?

### Tempdirectory extension

- Hogyan tudok fájlkezeléssel kapcsolatos műveleteket tesztelni?

  * ```java
    @TempDir
    Path tempDir;
    @Test
    void testWriteEmployee() throws IOException {
    Path file = tempDir.resolve("john-doe.txt");
    new EmployeeWriter()
    .write(file, new Employee("John Doe", 1970));
    assertEquals("John Doe, 1970", Files.readString(file));
    }
    ```

### JUnit legjobb gyakorlatok

- Mik azok a F.I.R.S.T. elvek?
  * F -Fast gyorsnak kell lenniük
  * I-Isolated: függetlennek kell leniük
  * R-Repatable: megismételhető, mindigugyanazz legyen az eredmény
  * S- Self-Validating: a tesztek automatizáltak legyenek ne kelljen a fejlesztőnek manuálisan ellenőriznie(ne sout hanem assert)
  * T- Thorough: alaposság. Lehetőleg az adott tesztelendő funkciót összes elágazását teszteljük, teszteljük határértéknél, extrém nagy, extrém kicsi, null, üres stb

---
## Szoftvertesztelés Hamcrest, AssertJ és Mockito használatával

### Hamcrest

- Mi az a Hamcrest? Miért van létjogosultsága?
  * 3. party library tesztelésre, Junit korllátozott a JavaBeans osztályoknál és a kollekcióknál
- Milyen metódus használható egyszerű ellenőrzésekre Hamcrestben? Hogyan kell paraméterezni?
  * assertThat(aktuális érték, matcher)
- Mi az a matcher?
- Sorolj fel négy matchert!
  * equalTo
  * instanceOf
  * startWith()
  * endWith()
- Miért egyszerűbb kollekciókat tesztelni Hamcrest segítségével?
  * contains(), hasitem()

### AssertJ

- Mi az az AssertJ? Miért van létjogosultsága?

  * 3. party library tesztelésre, Junit korllátozott a JavaBeans osztályoknál és a kollekcióknál

- Mit jelent az, hogy az assertek fluentek? Mi az oka, hogy a fejlesztőeszköz tud segíteni egy-egy metódus hívásánál?

  * hasonlít a természetes nyelvben megfogalmazott mondatokra, metódusait nem kell statikusan imprtálni

- Hogyan tudok kollekciókat tesztelni AssertJ segítségével?

  * ```java
    assertThat(employeeNames)
    .hasSize(2)
    .contains("John Doe", "Jack Doe")
    .doesNotContain("Jane Doe");
    ```

- Mi az a tuple?

  * ha nem egy hanem töb autributom értéket akkarjuk vizsgálni akkor tuple-t használunk

  * ```java
    assertThat(employees)
    .extracting(Employee::getName, Employee::getYearOfBirth)
    .contains(tuple("John Doe", 1970),
    tuple("Jack Doe", 1980));
    ```

- Mire használható a soft assert?

  * ha nem bukik el azonnal a teszt esett, hanem ezeket összegyüjti és csak a vágán irja ki

### Mockito

- Mi az a Mockito? Mikor használjuk?

  * unit tesztelés egyszerű lehetőségeit egy olyan osztály esetében, melynek külső függőségei vannak. Segítségünkre lesz ebben a Mockito
    keretrendszer. test double-t használink ez olyan interfészel rendelkezik mint az eredeti osztályunk, de ugyvannak a metódusok implementálva, hogy a tesztteléshez megfelelő legyen.

- Mit jelent az, hogy egy implementáció fake?

  * Dummy: ez gyakorlatilag nem csinál semmit, a metódusai üresek, csak arra van, hogy leforduljon a tesztesetben az adott osztály.
  * Fake: ez már működő implementáció, hasonlóan viselkedik, mint az éles, de sok korlátozással rendelkezik. Ilyen például egy valódi adatbázis helyett egy in-memory, tehát egy memóriában működő, az adatokat a memóriába elmentő kollekció.
  * Stub: olyan test double, amely előkészített válaszokkal rendelkezik. Tehát megadjuk neki, hogy ha meghívják valamelyik metódusát, akkor konkrétan mit adjon vissza. Emiatt nem is használható általánosan, csak az adott, konkrét tesztesetnél tud működni.
  *  Mock: ez nemcsak hogy meg lehet mondani neki, hogy milyen válaszokat adjon vissza,de még arra is képes, hogy rögzíti a tesztelendő osztály rajta futtatott hívásait, és ezekre tudunk asserteket írni, hogy a megfelelő metódusai lettek-e meghívva a megfelelő paraméterekkel.

- Mi a különbség a mock és a stub között?

- Hogyan tudok mock objektumot előállítani?

  * EmployeeRepository repository = mock(EmployeeRepository.class);
  * @Mock annotávió

- Mire való a `when()` metódus?

  * ```java
    when(repo.findEmployeeByName(anyString()))
    .thenThrow(
    new IllegalStateException("Constraint violation"));
    ```

- Mire való a `verify()` metódus?

  * ezzel ellenőrizzük hogy az adott metódus meghívásra került-e

- Hogyan tudom ellenőrizni, hogy egy metódus megfelelő paraméterekkel lett-e meghívva?

  * ArgumentCaptor

---

