# Mozi

## Feladat funkcionális követelményei

### Webes felhasználói felület
- Főoldalon a legnépszerűbb filmek
- Filmekre kattintva megtekinthető a film bemutatása
- Moziműsor megtekintése egy hétre előre
- Rá lehet szűrni a vetítésekre film, illetve dátum alapján
- Időpontra kattintva lehetőség nyílik jegyeket foglalni
- Meg kell adni, hogy hány főre és hogy diák vagy felnőtt jegy(ek)et szeretnénk foglalni
- Végül tudunk választani a szabad ülőhelyek közül és az adataink megadásával érvénybe lép a foglalás 

### Grafikus adminisztrátori felület
- Vetítések felvitele megfelelő időpontban
- Filmek felvitele, módosítása és törlése
- Foglalások megtekintése és kezelése

## Feladat nem funkcionális követelményei

- H2 adatbáziskezelő használata
- JPA
- MVC architektúra a felhasználói funkciók biztosítására
- A kliens biztosítja a megadott adatok megjelenítését és szerkesztését
- JUnit tesztek

## Szakterületi fogalomjegyzék
| Fogalom | Magyarázat |
| ------ | ------ |
| Szerver | Egy programot, ami egy, vagy több számítógépen fut, és kezeli a hálózat rendelkezésre álló erőforrásait és szolgáltatásait, miközben fogadja a különböző számítógépek hozzáférési kérelmeit az említett erőforrásokhoz. |
| Kliens | Egy program, amely hozzáfér egy szolgáltatáshoz, melyet a szerver nyújt.|
| * [h2] | Java SQL adatbáziskezelő. |
| * [JPA] | Keretrendszer a JAVA programozási nyelvhez, fő feladata a relációs adatok kezelése. |
| * [MVC] | (Model-View-Controller) Szerkezeti minta a felhasználói felület, az alkalmazás logikájának és a vezérlés szétválasztásához. |
| * [JUnit] | Egységteszt keretrendszer a JAVA nyelvhez. |
## Szerepkörök
### Nézők:
- Moziműsor megtekintése
- Filmek leírásának megtekintése
- Jegy(ek) rendelése
- Jegy tulajdonságainak testreszabása (Felnőtt/Diák)
- Tetszőleges hely kiválasztása (az adott moziterem kapacitásának, és az addig lefoglalt helyek figyelembe vételével)
- Foglalás véglegesítése (név és e-mail cím megadásával)
### Alkalmazottak:
 - Előadások meghirdetése
 - Foglalások megtekintése és kezelése
- Új film felvitele az adatai megadásával
- Filmek módosítása, törlése
- Új vetítés meghirdetése
## A fejlesztői környezet és eszközök bemutatása:

A project a NetBeans nevű fejlesztői környezetben készült a Maven Project, mely egy olyan fejlesztői eszköz, amivel könnyen lehet felhasználni más modulokat/plug-in-eket, és leszedi az ehhez szükséges dependencyket(függőségeket), valamint a Spring Boot felhasználásával, mely egy olyan eszköz, amellyel könnyen és gyorsan lehet prototípusokat létrehozni. Továbbá felhasználtuk a h2 adatbázis motort is a projectben, mely Java SQL adatbázist vezényel, illetve a Lombok nevű plug-in-t, aminek köszönhetően nem kell gettereket, settereket írni, valamint összehasonlító(equals) metódusokat.

## Adatbázis terv:
![alt text](http://url/to/img.png)
## Alkalmazott könyvtárstruktúra bemutatása:
![alt text](http://url/to/img.png)

A forrás fájlok a cinema nevű főkönyvtárban találhatók, mely több alkönyvtárra ágazik szét:
 - controllers
 - security
 - entities
 - repositories
 
A fő könyvtárban található a CinemaApplication.java fájl mely a program belépési pontja (itt található a main metódus).
## Végpont-tervek és leírások:
### ChairController:
| Végpont | Leírás |
| ------ | ------ |
| /chairs | Le lehet kérni az összes széket az adatbázisban, illetve új széket adhatunk hozzá. Ha a User admin, akkor az összeset, ha felhasználó, akkor pedig a hozzá tartozó székeket. |
| /chairs/{id} | Azonosító szerint lehet lekérni az adott széket , lehet módosítani, illetve törölni. |
### MovieController:
| Végpont | Leírás |
| ------ | ------ |
| /movies | Le lehet kérni az összes filmet az adatbázisban, illetve új filmet lehet hozzáaadni. |
| /movies/{id} | Azonosító szerint lehet lekérni az adott filmet, lehet módosítani, illetve törölni. |
| /movies/{id}/screenings | Le lehet kérni az adott filmhez tartozó összes vetítést, illetve hozzá lehet adni új vetítést az adott filmhez. |
| /movies/{id}/chairs | Le lehet kérni az adott filmhez tartozó összes lefoglalt széket (tehát más szóval az összes foglalást az összes vetítésre), illetve hozzá lehet adni új széket (=foglalást) az adott filmhez, továbbá módosítani lehet a székeket (pl.: foglalt-ból eladott-at csinálni). |
### RoomController:
| Végpont | Leírás |
| ------ | ------ |
| /rooms | Le lehet kérni az összes termet az adatbázisban, illetve hozzá lehet új termet adni. |
| /rooms/{id} | Az adott azonosítójú termet kérhetjük le, módosíthatjuk, illetve törölhetjük. |
| /rooms/{id}/chairs | Az adott azonosítójú teremnek kérhetjük le az összes székét (hogy foglalt-e/eladott és, hogy ki foglalta le stb.), illetve, ha lefoglalnak új széket, akkor itt is hozzá lehet adni. |
| /rooms/{id}/screenings | Megkaphatjuk az összes vetítést az adott azonosítójú teremhez, illetve újabb vetítést adhatunk hozzá. |
### ScreeningController:
| Végpont | Leírás |
| ------ | ------ |
| /screenings | Le lehet kérni az összes vetítést az adatbázisban, illetve hozzá lehet új vetítést adni. |
| /screenings/{id} | Az adott azonosítójú vetítést kérhetjük le, módosíthatjuk, illetve törölhetjük. |
| /screenings/{id}/chairs | Az adott azonosítójú vetÍtéshez kérhetjük le a székeket (foglalási adatok), illetve adhatunk hozzá székeket (új foglalást). |
| /screenings/{id}/rooms | Az adott azonosítójú vetÍtéshez kérhetjük le a hozzá tartozó termet. |
### UserController:
| Végpont | Leírás |
| ------ | ------ |
| /users/register | Új felhasználót tudunk hozzáadni. |
| /users/login | Bejelentkezéssel azonosítani tudjuk a felhasználót. |

## 1db végpont működésének leírása:

Vegyük például a MovieController osztályt, és az abban található „movies/{id}/screenings” végpontot. Ehhez 2 metódus tartozik a screenings (a vetítések listázása) és az insertScreening metódus.
A „movies/{id]/screenings” végpontra érkezik a kérés, ezt a Controller elkapja, és a paraméterek alapján beazonosítja, hogy a screenings vagy az insertScreening metódust kell-e használnia.

### screenings metódus:
Megkeresi a filmet a film azonosítója (id) szerint, ha talált az adott azonosítóval filmet, akkor, a ResponseEntity ok metódusának segítségével visszaküldi a filmhez tartozó vetítéseket, ha nem, akkor pedig egy nem talált válasz entitást fog buildelni, amit visszaküld a ResponseEntity notFound metódusával.

![alt text](http://url/to/img.png)

### insertScreening metódus:
Megkeresi a filmet a film azonosítója (id) szerint, ha talált az adott azonosítóval filmet, akkor a paraméterben kapott Screening objekutmnak beállítja az adott adott azonosítójú filmet, és a ResponseEntity ok metódusának segítségével elmenti a screeningRepository-ba (tehát a Screenings táblába) az adott vetítést, ha nincs az adott azonosítóval film, akkor pedig a ResponseEntity notFound metódusával egy nem talált válasz entitást fog buildelni.

![alt text](http://url/to/img.png)

## Fontosabb Specifikumok:
A chairs táblában az összes adatot csak az admin tudja megnézni, movies táblába adatot felvinni, törölni és módosítani is csak az admin tud, illetve a screenings és a rooms táblába felvinni, módosítani és törölni is csak az admin tud. A guest csak meg tudja nézni a vetítések, illetve a filmek listáját, a user foglalni is tud, és le tudja kérni a saját foglalásainak adatait.

   [h2]: <http://www.h2database.com/html/main.html>
   [JPA]: <https://www.tutorialspoint.com/jpa/>
   [MVC]: <http://web.progtanulo.hu/web-programozas-alapismeretek/3-szerver-oldali-mukodes/310-tervezesi-mintak/3103-mvc>
   [JUnit]: <https://junit.org/junit4/>
	
 
