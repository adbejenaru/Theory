Programarea funcțională este un stil de programare în care computațiile sunt tratate ca evaluări de funcții matematice și evită schimbarea stării și a datelor mutable. În Java, acest stil a devenit mai accesibil odată cu introducerea lui Java 8, care a adăugat suport pentru expresii lambda și interfete funcționale.

### Interfețe Funcționale

O interfață funcțională este o interfață care conține o singură metodă abstractă, dar poate avea și metode implicite sau statice. Aceste interfețe sunt adesea folosite în contextul programării funcționale și permit utilizarea expresiilor lambda.

Exemple de interfețe funcționale predefinite în Java includ:

- `java.util.function.Predicate<T>` - o metodă abstractă `test` care primește un argument de tip T și returnează un boolean.
- `java.util.function.Function<T, R>` - o metodă abstractă `apply` care primește un argument de tip T și returnează un rezultat de tip R.
- `java.util.function.Consumer<T>` - o metodă abstractă `accept` care primește un argument de tip T și nu returnează nimic.
- `java.util.function.Supplier<T>` - o metodă abstractă `get` care nu primește argumente și returnează un rezultat de tip T.

### Expresii Lambda

Expresiile lambda sunt o funcționalitate introdusă în Java 8 care permite scrierea de funcții anonime, adică funcții fără nume. Ele sunt foarte utile în programarea funcțională, deoarece permit utilizarea funcțiilor ca argumente, valori de întoarcere și variabile.

Sintaxa unei expresii lambda este:
```java
(parameters) -> expression
```
sau
```java
(parameters) -> { statements }
```

### Exemple de Interfețe Funcționale și Lambda în Java

#### Predicate
```java
Predicate<String> isEmpty = s -> s.isEmpty();
boolean result = isEmpty.test("");
System.out.println(result); // Afișează true
```

#### Function
```java
Function<String, Integer> stringLength = s -> s.length();
int length = stringLength.apply("Hello");
System.out.println(length); // Afișează 5
```

#### Consumer
```java
Consumer<String> print = s -> System.out.println(s);
print.accept("Hello, World!"); // Afișează Hello, World!
```

#### Supplier
```java
Supplier<Double> randomValue = () -> Math.random();
double value = randomValue.get();
System.out.println(value); // Afișează o valoare aleatorie
```

### Crearea unei Interfețe Funcționale Personalizate

Poți crea și propriile tale interfețe funcționale. De exemplu:
```java
@FunctionalInterface
interface MyFunction {
    int apply(int x, int y);
}

public class Main {
    public static void main(String[] args) {
        MyFunction add = (x, y) -> x + y;
        int result = add.apply(5, 3);
        System.out.println(result); // Afișează 8
    }
}
```

În acest exemplu, `MyFunction` este o interfață funcțională personalizată care definește o metodă `apply`. Expresia lambda `(x, y) -> x + y` implementează această metodă pentru a adăuga două numere.

Programarea funcțională în Java, cu ajutorul interfețelor funcționale și al expresiilor lambda, permite un stil de cod mai concis, flexibil și ușor de citit, promovând în același timp imutabilitatea și evitarea efectelor secundare.
