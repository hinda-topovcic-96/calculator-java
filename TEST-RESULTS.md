# Izvještaj o testiranju (Assignment - Testiranje)

## 1. Sistemsko testiranje (Black Box testing)
Testiranje je obavljeno metodom crne kutije unosom različitih aritmetičkih izraza radi provjere funkcionalnosti, prioriteta operacija i rukovanja greškama.

| Test ID | Opis testa | Ulazni podaci | Očekivani izlaz | Stvarni izlaz | Status | Zapažanje / Nedostatak |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Osnovno sabiranje i oduzimanje | `10+5-3` | `12.0` | `12.0` | **PASS** | Radi ispravno. |
| **TC-02** | Prioritet računskih operacija | `4+5*2` | `14.0` | `14.0` | **PASS** | Množenje ima prednost nad sabiranjem. |
| **TC-03** | Dijeljenje sa nulom | `10/0` | `Infinity` ili Poruka o grešci | `Infinity` | **FAIL / WARN** | Program vraća `Infinity` umjesto izuzetka ili poruke o onemogućenom dijeljenju sa nulom. |
| **TC-04** | Prazan unos | ` ` (prazan string) | Poruka o nevažećem unosu | `StringIndexOutOfBoundsException` | **FAIL** | Program se ruši jer ne provjerava dužinu stringa prije pozivanja `.charAt(0)`. |
| **TC-05** | Unos neispravnog znaka | `10+a` | Poruka o grešci | `ERROR` | **PASS** | Program hvata izuzetak pri konverziji i vraća `ERROR`. |
| **TC-06** | Negativan broj na početku | `-5+10` | `5.0` | `5.0` | **PASS** | Program uspješno dodaje `0` na početak i računa tačno. |

---

## 2. Jedinični test (Unit Test)

Sljedeći Java test primjer koristi JUnit okvir za provjeru funkcionisanja metode `Calculator.Run()` (odnosno interne metode za računanje):

```java
import org.junit.jupiter.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    public void testCalculatePriorityAndOperations() {
        // Testiranje prioriteta operacija (množenje i sabiranje)
        String expression = "10+5*2";
        String expected = "20.0";
        String actual = Calculator.Run(expression);
        
        assertEquals(expected, actual, "Izraz 10+5*2 bi trebao vratiti 20.0 zbog prioriteta množenja");
    }

    @Test
    public void testInvalidInput() {
        // Testiranje neispravnog unosa
        String expression = "abc";
        String expected = "ERROR";
        String actual = Calculator.Run(expression);
        
        assertEquals(expected, actual, "Neispravan unos bi trebao vratiti ERROR");
    }
}
