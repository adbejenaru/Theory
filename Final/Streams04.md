Stream API în Java, introdusă în Java 8, oferă o modalitate modernă și eficientă de a procesa colecții de date. Stream-urile reprezintă o secvență de elemente care suportă diferite tipuri de operații, cum ar fi filtrarea, maparea și reducerea, într-o manieră funcțională și declarativă.

### Concepte Cheie

1. **Streams**:
   - Nu stochează date, ci procesează datele provenite dintr-o colecție.
   - Sunt la fel ca fluxurile de date, permițând procesarea secvențială sau paralelă.
   
2. **Operații Intermediare**:
   - Operațiile intermediare sunt "lazy", adică sunt evaluate doar atunci când o operație terminală este invocată.
   - Exemple: `filter()`, `map()`, `sorted()`.
   
3. **Operații Terminale**:
   - Produc un rezultat din flux și termină fluxul.
   - Exemple: `forEach()`, `collect()`, `reduce()`.

4. **Operații Intermediare vs. Operații Terminale**:
   - Operațiile intermediare returnează un nou Stream, permițând lanțuri de apeluri de metode.
   - Operațiile terminale declanșează procesarea fluxului și returnează un rezultat concret sau efecte secundare.

### Exemple de Utilizare

Iată câteva exemple simple pentru a demonstra utilizarea Stream API:

#### Filtrare și Mapare

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ana", "John", "Alex", "Brian");

        // Filtrare: păstrează doar numele care încep cu 'A'
        List<String> filteredNames = names.stream()
            .filter(name -> name.startsWith("A"))
            .collect(Collectors.toList());

        System.out.println("Nume filtrate: " + filteredNames);

        // Mapare: transformă toate numele în majuscule
        List<String> upperCaseNames = names.stream()
            .map(String::toUpperCase)
            .collect(Collectors.toList());

        System.out.println("Nume cu majuscule: " + upperCaseNames);
    }
}
```

#### Reducere

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Reducere: calcularea sumei numerelor
        int sum = numbers.stream()
            .reduce(0, Integer::sum);

        System.out.println("Suma numerelor: " + sum);
    }
}
```

### Avantajele Utilizării Stream API

- **Cod mai clar și mai concis**: permite scrierea codului într-un mod mai declarativ și ușor de citit.
- **Performanță**: permite procesarea paralelă simplificată, ceea ce poate duce la îmbunătățiri ale performanței pe procesoare multi-core.
- **Flexibilitate**: oferă o gamă largă de operații predefinite care pot fi combinate pentru a realiza operații complexe pe colecții de date.

Stream API aduce un stil de programare mai funcțional în Java, facilitând manipularea și procesarea colecțiilor de date într-un mod eficient și elegant.
