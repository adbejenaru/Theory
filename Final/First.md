Interfața funcțională în Java este un concept introdus în Java 8. Aceasta este o interfață care conține exact o metodă abstractă. Aceste interfețe sunt folosite ca baza pentru lambda expressions în Java, permițând o programare mai funcțională și mai concisă. Iată câteva puncte cheie despre interfețele funcționale:

1. **O Singură Metodă Abstractă (SAM - Single Abstract Method):** Interfața trebuie să aibă exact o metodă abstractă. Poate avea și alte metode, dar acestea trebuie să fie metode default sau static.

2. **Lambda Expressions:** O interfață funcțională poate fi implementată printr-o expresie lambda. Asta înseamnă că poți scrie implementări ale interfeței într-un stil mai concis și mai expresiv.

3. **Annotația `@FunctionalInterface`:** Deși nu este obligatorie, este o practică bună să marchezi o interfață funcțională cu annotația `@FunctionalInterface`. Aceasta ajută în clarificarea intenției și asigură că interfața respectă regulile interfețelor funcționale.

4. **Exemple Comune:** Interfețe funcționale comune în Java sunt `Runnable`, `Callable`, `Comparator`, și interfețele din pachetul `java.util.function` cum ar fi `Predicate`, `Function`, `Consumer`, și `Supplier`.

5. **Utilizare:** Sunt foarte utile în contextul programării funcționale, în special atunci când lucrezi cu fluxuri de date (streams) și operații care necesită comportamente parametrizate.

Un exemplu simplu de interfață funcțională ar fi:

```java
@FunctionalInterface
public interface Simplu {
    void execute();
}
```

Și o implementare a acestei interfețe cu o expresie lambda ar putea arăta astfel:

```java
Simplu s = () -> System.out.println("Hello, Functional Interface!");
s.execute();
```

Aceasta este o modalitate foarte puternică și flexibilă de a scrie cod în Java, permițând un stil de programare mai apropiat de paradigma funcțională.

Sigur, să examinăm un exemplu complet care folosește `@FunctionalInterface` în Java. Vom crea o interfață funcțională simplă care reprezintă o operație matematică cu un singur argument și vom folosi această interfață pentru a implementa diferite funcții matematice prin expresii lambda.

Pentru început, definim interfața funcțională:

```java
@FunctionalInterface
public interface OperatieMatematica {
    double apply(double value);
}
```

Această interfață are o singură metodă abstractă, `apply`, care primește un argument de tip `double` și returnează un `double`.

Apoi, într-o clasă principală, implementăm și utilizăm această interfață:

```java
public class ExempluFunctionalInterface {
    public static void main(String[] args) {
        // Implementare cu expresie lambda pentru a calcula pătratul unui număr
        OperatieMatematica patrat = x -> x * x;
        System.out.println("Patratul lui 5 este: " + patrat.apply(5));

        // Implementare pentru a calcula inversul unui număr
        OperatieMatematica invers = x -> 1 / x;
        System.out.println("Inversul lui 4 este: " + invers.apply(4));

        // Implementare pentru a calcula rădăcina pătrată
        OperatieMatematica radacina = Math::sqrt; // Metodă referență
        System.out.println("Rădăcina pătrată a lui 16 este: " + radacina.apply(16));
    }
}
```

În acest exemplu, am creat trei implementări diferite ale interfeței `OperatieMatematica` folosind expresii lambda și o metodă referență. Prima calculă pătratul unui număr, a doua calculează inversul, iar a treia calculează rădăcina pătrată. Aceste implementări sunt apoi folosite pentru a efectua operațiile pe numere specifice.

Acest exemplu arată cum interfețele funcționale și expresiile lambda pot simplifica și face mai expresiv codul care implică comportamente parametrizate sau operații.


`Optional` în Java este o clasă container introdusă în Java 8, găsită în pachetul `java.util`. Aceasta este folosită pentru a reprezenta valori optionale, adică valori care pot fi prezente sau absente. `Optional` ajută la evitarea erorilor `NullPointerException` și la scrierea unui cod mai curat, mai lizibil, care tratează explicit cazurile în care o valoare poate să nu fie disponibilă.

Principalele caracteristici ale `Optional` sunt următoarele:

1. **Evitarea `NullPointerException`**: Prin folosirea `Optional`, poți evita situația în care o variabilă care este așteptată să aibă o valoare este, de fapt, `null`. Asta reduce riscul de erori la runtime.

2. **Cod Mai Expresiv**: `Optional` face ca intenția codului să fie mai clară. De exemplu, dacă o metodă returnează un `Optional<String>`, este clar că ar putea să nu returneze un `String`.

3. **Metode Utile**: Clasa `Optional` vine cu metode utile precum `ifPresent()`, `orElse()`, `orElseGet()`, `orElseThrow()`, care ajută la gestionarea cazurilor în care valoarea este prezentă sau absentă.

4. **Utilizare cu Stream API**: `Optional` se integrează bine cu Stream API din Java 8, permițând operații funcționale și fluide.

Un exemplu simplu de utilizare a `Optional` ar fi:

```java
import java.util.Optional;

public class ExempluOptional {
    public static void main(String[] args) {
        Optional<String> optionalValoare = metodaCarePoateReturnaNull();

        // Verifică dacă o valoare este prezentă și o utilizează
        if (optionalValoare.isPresent()) {
            System.out.println("Valoarea este: " + optionalValoare.get());
        } else {
            System.out.println("Valoarea lipsește.");
        }

        // O abordare mai funcțională
        optionalValoare.ifPresent(valoare -> System.out.println("Valoarea este: " + valoare));
    }

    static Optional<String> metodaCarePoateReturnaNull() {
        // Logică care returnează un String sau null
        String str = ...; // presupunem că aceasta este logica
        return Optional.ofNullable(str);
    }
}
```

În acest exemplu, `metodaCarePoateReturnaNull` returnează un `Optional<String>`. Când folosim această valoare, putem verifica dacă este prezentă sau nu într-un mod mult mai sigur și mai clar decât verificând pur și simplu dacă este `null`.

Modulele în Java, introduse în Java 9 prin JEP 261 ca parte a Proiectului Jigsaw, reprezintă o schimbare majoră în modul de organizare și structurare a codului Java. Scopul principal al sistemului de module este de a oferi o modalitate mai bună de a împacheta și a gestiona librăriile și aplicațiile Java, ajutând astfel la rezolvarea unor probleme precum "Hell-ul JAR" (Jar Hell) și dependențele complexe între pachete.

Principalele caracteristici ale sistemului de module în Java sunt:

1. **Encapsulare Puternică:** Modulele permit o împărțire clară și strictă a codului în unități logice, fiecare cu propriul său set de dependențe și exporturi. Astfel, un modul poate controla explicit ce anume expune altor module și ce anume ascunde.

2. **Gestionarea Dependințelor:** Sistemul de module facilitează o gestionare mai bună a dependențelor, permițând specificarea clară a modulului de care depinde un modul.

3. **Îmbunătățirea Performanței:** Modulele pot îmbunătăți performanța aplicațiilor Java prin reducerea suprafeței de atac a JVM-ului și prin posibilitatea de a optimiza aplicațiile în timpul compilării.

4. **Mai Puține Probleme la Runtime:** Datorită gestionării mai bune a dependențelor și encapsulării, modulele ajută la reducerea problemelor care pot apărea la runtime, cum ar fi conflictele de clasă.

Un modul în Java este definit printr-un fișier special numit `module-info.java`, care descrie numele modulului, dependențele sale, ce pachete expune pentru alte module și ce alte module sunt necesare. De exemplu:

```java
module com.example.myapp {
    requires java.sql;
    exports com.example.myapp.api;
}
```

În acest exemplu, `com.example.myapp` este numele modulului. Acesta necesită `java.sql` (alt modul) și exportă pachetul `com.example.myapp.api` pentru a fi folosit de alte module.

Sistemul de module aduce un nivel suplimentar de
