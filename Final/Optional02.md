`Optional` în Java este o clasă introdusă în Java 8, care face parte din pachetul `java.util`. `Optional` este utilizat pentru a reprezenta o valoare care poate fi prezentă sau absentă. Este un container pentru un obiect ne-null și ajută la evitarea erorilor legate de utilizarea `null`.

### Crearea unui Optional

1. **Crearea unui `Optional` gol**:
   - Un `Optional` care nu conține nicio valoare poate fi creat folosind metoda statică `empty()`:
   ```java
   Optional<String> emptyOptional = Optional.empty();
   ```

2. **Crearea unui `Optional` cu o valoare**:
   - Un `Optional` care conține o valoare poate fi creat folosind metoda statică `of()`:
   ```java
   Optional<String> optionalWithValue = Optional.of("Hello");
   ```
   - Dacă valoarea poate fi `null`, folosește metoda `ofNullable()`:
   ```java
   Optional<String> optionalWithNullableValue = Optional.ofNullable(null);
   ```

### Verificarea valorii în Optional

1. **Verificarea dacă un `Optional` conține o valoare**:
   - Metoda `isPresent()` returnează `true` dacă `Optional` conține o valoare, și `false` dacă este gol:
   ```java
   if (optionalWithValue.isPresent()) {
       System.out.println("Value is present");
   }
   ```

2. **Executarea unui cod dacă valoarea este prezentă**:
   - Metoda `ifPresent()` primește un `Consumer` și execută codul doar dacă valoarea este prezentă:
   ```java
   optionalWithValue.ifPresent(value -> System.out.println("Value: " + value));
   ```

### Obținerea valorii din Optional

1. **Obținerea valorii cu `get()`**:
   - Metoda `get()` returnează valoarea dacă este prezentă, dar aruncă `NoSuchElementException` dacă `Optional` este gol:
   ```java
   String value = optionalWithValue.get();
   ```

2. **Obținerea valorii cu o valoare implicită**:
   - Metoda `orElse()` returnează valoarea dacă este prezentă, altfel returnează valoarea implicită specificată:
   ```java
   String valueOrDefault = emptyOptional.orElse("Default Value");
   ```

3. **Obținerea valorii cu un supplier**:
   - Metoda `orElseGet()` returnează valoarea dacă este prezentă, altfel execută supplier-ul pentru a obține valoarea:
   ```java
   String valueOrElseGet = emptyOptional.orElseGet(() -> "Default Value from Supplier");
   ```

4. **Aruncarea unei excepții dacă valoarea nu este prezentă**:
   - Metoda `orElseThrow()` aruncă o excepție specificată dacă valoarea nu este prezentă:
   ```java
   String valueOrElseThrow = emptyOptional.orElseThrow(() -> new IllegalArgumentException("No value present"));
   ```

### Transformarea valorii din Optional

1. **Transformarea valorii cu `map()`**:
   - Metoda `map()` aplică o funcție asupra valorii dacă aceasta este prezentă și returnează un `Optional` al rezultatului:
   ```java
   Optional<Integer> length = optionalWithValue.map(String::length);
   ```

2. **Transformarea valorii cu `flatMap()`**:
   - Metoda `flatMap()` este similară cu `map()`, dar funcția trebuie să returneze un `Optional`:
   ```java
   Optional<String> upperCaseValue = optionalWithValue.flatMap(value -> Optional.of(value.toUpperCase()));
   ```

### Filtrarea valorii din Optional

1. **Filtrarea valorii cu `filter()`**:
   - Metoda `filter()` aplică un `Predicate` asupra valorii și returnează un `Optional` gol dacă valoarea nu îndeplinește condiția:
   ```java
   Optional<String> filteredValue = optionalWithValue.filter(value -> value.startsWith("H"));
   ```

### Exemplu Complet

Să combinăm toate aceste concepte într-un exemplu complet:

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        // Crearea unui Optional gol
        Optional<String> emptyOptional = Optional.empty();
        
        // Crearea unui Optional cu o valoare
        Optional<String> optionalWithValue = Optional.of("Hello");

        // Crearea unui Optional care poate conține o valoare null
        Optional<String> optionalWithNullableValue = Optional.ofNullable(null);

        // Verificarea dacă un Optional conține o valoare
        if (optionalWithValue.isPresent()) {
            System.out.println("Value is present");
        }

        // Executarea unui cod dacă valoarea este prezentă
        optionalWithValue.ifPresent(value -> System.out.println("Value: " + value));

        // Obținerea valorii cu get()
        String value = optionalWithValue.get();
        System.out.println("Value obtained with get(): " + value);

        // Obținerea valorii cu o valoare implicită
        String valueOrDefault = emptyOptional.orElse("Default Value");
        System.out.println("Value with orElse: " + valueOrDefault);

        // Obținerea valorii cu un supplier
        String valueOrElseGet = emptyOptional.orElseGet(() -> "Default Value from Supplier");
        System.out.println("Value with orElseGet: " + valueOrElseGet);

        // Aruncarea unei excepții dacă valoarea nu este prezentă
        try {
            String valueOrElseThrow = emptyOptional.orElseThrow(() -> new IllegalArgumentException("No value present"));
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }

        // Transformarea valorii cu map()
        Optional<Integer> length = optionalWithValue.map(String::length);
        System.out.println("Length of value: " + length.orElse(0));

        // Transformarea valorii cu flatMap()
        Optional<String> upperCaseValue = optionalWithValue.flatMap(value -> Optional.of(value.toUpperCase()));
        System.out.println("Uppercase value: " + upperCaseValue.orElse("No value"));

        // Filtrarea valorii cu filter()
        Optional<String> filteredValue = optionalWithValue.filter(value -> value.startsWith("H"));
        System.out.println("Filtered value: " + filteredValue.orElse("No value"));
    }
}
```

### Concluzie

`Optional` este o clasă utilă în Java pentru a reprezenta valorile care pot fi prezente sau absente, ajutând la evitarea erorilor legate de `null` și oferind un API clar și fluent pentru manipularea acestor valori. Este deosebit de util în codurile care implică operațiuni care pot să nu returneze o valoare (de exemplu, căutările într-o colecție) și în API-uri publice pentru a semnala că o valoare poate fi absentă.
