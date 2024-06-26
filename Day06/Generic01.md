Genericitatea în Java este o funcționalitate care permite clasei sau metodei să opereze pe obiecte de diferite tipuri, asigurând totodată securitatea tipurilor la compilare. Aceasta a fost introdusă pentru a îmbunătăți flexibilitatea și reutilizabilitatea codului. Aici sunt câteva puncte cheie despre genericitate în Java:

1. **Tipuri generice**: Clasele, interfețele și metodele pot fi definite cu unul sau mai multe tipuri de parametri. Acești parametri de tip permit crearea de instanțe de clase cu diferite tipuri de date fără a compromite siguranța tipului. De exemplu, clasa `ArrayList<T>` poate fi utilizată pentru a crea liste de orice tip de date, cum ar fi `ArrayList<Integer>` sau `ArrayList<String>`.

2. **Metode generice**: Similar cu clasele generice, metodele generice sunt metode care introduc proprii lor parametri de tip. Aceasta înseamnă că aceleași metode pot fi utilizate pe diferite tipuri de date. Exemplu:
   ```java
   public <T> void printArray(T[] array) {
       for (T element : array) {
           System.out.println(element);
       }
   }
   ```

3. **Bounded Type Parameters**: Uneori este necesar să limităm tipurile care pot fi folosite ca argumente pentru tipurile generice. Acest lucru se realizează prin utilizarea parametrilor de tip delimitat. De exemplu, `public <T extends Number> void process(T value)` permite metodei să accepte doar argumente care sunt subtipuri ale clasei `Number`.

4. **Wildcard-uri**: Caracterele wildcard (simbolul `?`) sunt folosite pentru a reprezenta un tip necunoscut. Wildcards pot fi de trei tipuri: 
   - Unbounded wildcard (`?`), care poate reprezenta orice tip.
   - Upper bounded wildcard (`? extends Type`), care poate reprezenta orice clasă care este o subclasă a `Type` sau `Type` însuși.
   - Lower bounded wildcard (`? super Type`), care poate reprezenta orice clasă care este o superclasă a `Type` sau `Type` însuși.

5. **Type Erasure**: Java folosește un mecanism numit ștergere de tip (type erasure) pentru a asigura compatibilitatea cu versiunile mai vechi de Java care nu suportă genericitatea. Acesta transformă toate parametrii de tip în limitele lor respective sau în `Object` dacă nu sunt specificate limite, în timpul compilării.

6. **Avantajele genericității**: Utilizarea genericității ajută la reducerea duplicării codului și la creșterea clarității și robusteții programelor. Prin forțarea tipurilor la compilare, se reduce riscul de erori la rulare.

Genericitatea face codul mai flexibil și mai sigur, permițând dezvoltatorilor să scrie coduri mai clar și mai ușor de înțeles, fără a compromite performanța sau siguranța tipurilor.

Wildcards în Java sunt o modalitate de a spori flexibilitatea și reutilizabilitatea codului atunci când lucrezi cu tipuri generice. Acestea pot fi limitate superior sau inferior, permițându-ți să controlezi tipurile de obiecte pe care le poți folosi într-un context generic. Iată o explicație detaliată a fiecăruia:

### Wildcard Limitat Superior (`<? extends T>`)

Wildcard-ul limitat superior este folosit atunci când vrei să lucrezi cu date dintr-o clasă specifică sau din oricare dintre subclasele acesteia. Prin utilizarea `<? extends T>`, specifici că parametrul generic poate fi orice tip care este `T` sau o subclasă a lui `T`.

**Utilizări Comune:**
- **Citire dintr-o colecție**: Este ideal pentru metodele care doar citesc dintr-o colecție și nu modifică obiectele pe care le conțin. De exemplu, poți utiliza `<? extends T>` pentru a parcurge o listă de obiecte `T` și a accesa metodele definite în `T` sau subclasele lui.

**Exemplu:**
```java
public void printList(List<? extends Number> list) {
    for (Number n : list) {
        System.out.println(n);
    }
}
```
Această metodă poate fi apelată cu o listă de `Integer`, `Float`, `Double`, etc., deoarece toate sunt subclase ale clasei `Number`.

### Wildcard Limitat Inferior (`<? super T>`)

Wildcard-ul limitat inferior este folosit atunci când vrei să scrii într-o colecție obiecte de un anumit tip sau de tipurile sale superioare. Prin utilizarea `<? super T>`, specifici că parametrul generic poate fi orice tip care este `T` sau o superclasă a lui `T`.

**Utilizări Comune:**
- **Scriere într-o colecție**: Această formă de wildcard este ideală pentru metodele care plasează obiecte într-o colecție. Asigură că toate obiectele pe care le adaugi sunt compatibile cu tipul specificat.

**Exemplu:**
```java
public void addToCollection(List<? super Integer> list) {
    list.add(123);
}
```
Această metodă poate fi apelată cu o listă de `Integer` sau orice tip de superclasă a lui `Integer` (cum ar fi `Number` sau `Object`), permițând adăugarea de întregi în colecție.

### Când să Folosești Fiecare

- **`<? extends T>`** este cel mai bine folosit atunci când intenționezi să preiei date dintr-o structură de date generica fără a modifica conținutul acesteia. Acest lucru asigură că nu încerci să adaugi obiecte incompatibile în colecție.
- **`<? super T>`** este util atunci când adaugi obiecte într-o structură de date și nu este nevoie să preiei obiecte specifice din aceasta.

Prin alegerea corectă între wildcard limitat superior și inferior, poți scrie cod care este atât sigur cât și flexibil, maximizând reutilizabilitatea și interoperabilitatea componentelor tale generice.
