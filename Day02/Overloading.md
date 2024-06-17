Method overloading (suprasarcinarea metodelor) este un concept în programarea orientată pe obiecte care permite unei clase să aibă mai multe metode cu același nume, dar cu semnături diferite. Semnătura unei metode include numele metodei și lista tipurilor de parametri.

### Când apare suprasarcinarea metodelor (method overloading)

Suprasarcinarea metodelor apare atunci când:
1. **Numărul parametrilor este diferit**:
   - O metodă poate avea un număr diferit de parametri.

2. **Tipurile parametrilor sunt diferite**:
   - O metodă poate avea parametri de tipuri diferite.

3. **Ordinea parametrilor este diferită**:
   - O metodă poate avea parametri în ordine diferită, atâta timp cât tipurile parametrilor diferă.

Tipul de returnare al metodei **nu** este considerat parte din semnătură în contextul suprasarcinării metodelor. De aceea, schimbarea doar a tipului de returnare nu este suficientă pentru suprasarcinarea metodelor.

### Exemple de suprasarcinare a metodelor

#### 1. Număr diferit de parametri

```java
class Calculator {
    // Metodă pentru adunare cu doi parametri
    public int add(int a, int b) {
        return a + b;
    }

    // Suprasarcinare cu trei parametri
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

#### 2. Tipuri diferite de parametri

```java
class Printer {
    // Metodă pentru printare text
    public void print(String text) {
        System.out.println(text);
    }

    // Suprasarcinare pentru printare număr
    public void print(int number) {
        System.out.println(number);
    }
}
```

#### 3. Ordinea parametrilor este diferită

```java
class Display {
    // Metodă pentru afișarea unui număr și apoi un text
    public void show(int number, String text) {
        System.out.println(number + " " + text);
    }

    // Suprasarcinare pentru afișarea unui text și apoi un număr
    public void show(String text, int number) {
        System.out.println(text + " " + number);
    }
}
```

### Exemplu complet de suprasarcinare a metodelor

```java
class Example {
    // Metodă fără parametri
    public void display() {
        System.out.println("Display without parameters");
    }

    // Metodă cu un parametru int
    public void display(int a) {
        System.out.println("Display with int: " + a);
    }

    // Metodă cu doi parametri int
    public void display(int a, int b) {
        System.out.println("Display with two ints: " + a + ", " + b);
    }

    // Metodă cu un parametru String
    public void display(String s) {
        System.out.println("Display with String: " + s);
    }

    // Metodă cu doi parametri, un String și un int
    public void display(String s, int a) {
        System.out.println("Display with String and int: " + s + ", " + a);
    }

    public static void main(String[] args) {
        Example example = new Example();

        example.display(); // Output: Display without parameters
        example.display(10); // Output: Display with int: 10
        example.display(10, 20); // Output: Display with two ints: 10, 20
        example.display("Hello"); // Output: Display with String: Hello
        example.display("Hello", 10); // Output: Display with String and int: Hello, 10
    }
}
```

### Rezumat

- **Suprasarcinarea metodelor** permite mai multe metode cu același nume în aceeași clasă.
- Metodele suprasarcinate trebuie să aibă semnături diferite (număr, tip și/sau ordine a parametrilor).
- Tipul de returnare nu este considerat parte din semnătură în contextul suprasarcinării metodelor.
- Suprasarcinarea este un exemplu de polimorfism la compilare, deoarece decizia de a apela o metodă specifică este făcută de compilator pe baza semnăturii metodei.
