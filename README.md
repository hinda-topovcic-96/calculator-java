# Izvještaj: Metrika, pregled i statička analiza koda

## 1. Softverska metrika
* **Calculator.java:** 134 LOC (od ukupno 188 linija)
* **Start.java:** 19 LOC (od ukupno 26 linija)
* **Zbirni LOC (za kompletan projekat):** 153 linije koda

---

## 2. Statička analiza i zapažanja (Code Smells)
Format izvještaja: `fajl - broj linije koda - zapažanje`

* `Calculator.java - linija 6` - Korištenje globalne statičke promenljive `static float finalResult;` za čuvanje rezultata izračunavanja može prouzrokovati probleme sa stanjem i višenitnošću (thread safety).
* `Calculator.java - linija 32-35` - Upotreba `expression.charAt(0)` bez provjere da li je uneseni string prazan može dovesti do `StringIndexOutOfBoundsException` izuzetka.
* `Calculator.java - linija 64` - Hvatanje opšteg izuzetka `catch (Exception exc)` i vraćanje generičkog stringa `"ERROR"` umjesto specifičnog rukovanja greškama.
* `Calculator.java - linija 76` - Rekurzivni pozivi funkcije `Calculate` za obradu operacija u listi povećavaju složenost i rizik od `StackOverflowError` kod složenijih izraza.
* `Start.java - linija 12` - Instanciranje `new Scanner(System.in)` unutar `while` petlje umjesto jednom prije petlje, što je nepotrebno trošenje resursa i može uticati na tok unosa.
