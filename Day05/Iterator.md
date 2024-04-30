În Java, un `Iterator` este o interfață care furnizează o modalitate de a parcurge elementele dintr-o colecție. Este parte a Java Collections Framework și oferă metode pentru a accesa secvențial elementele din orice colecție, fără a expune structura internă a acesteia. Folosirea unui iterator este metoda preferată de a parcurge colecții care nu oferă acces direct la elemente printr-un index, cum ar fi seturile (`Set`) și colecțiile bazate pe liste (`List`).

### Caracteristici Principale ale Iteratorului
- **Acces Secvențial**: Iteratorul permite accesul secvențial la elementele colecției, unul câte unul.
- **Operații de Modificare Opționale**: Pe lângă metodele de bază pentru iterare, iteratorii pot suporta operații de eliminare sau modificare a elementelor din colecție în timpul iterației.
- **Gestionare a Concurenței**: În timpul iterației, dacă structura colecției este modificată de către un alt thread sau chiar de către același thread dar în afara iteratorului, se va arunca o excepție de tip `ConcurrentModificationException`, indicând modificări nepermise în timpul iterației.

### Metode Cheie ale Interfeței `Iterator`
1. **hasNext()**
   - Returnează `true` dacă iteratorul are mai multe elemente de parcurs.
   - Aceasta este prima metodă verificată înainte de a încerca să accesăm următorul element cu `next()`.

2. **next()**
   - Returnează următorul element din iterație.
   - Aruncă o excepție de tip `NoSuchElementException` dacă nu mai sunt elemente de parcurs.

3. **remove()**
   - Elimină din colecție elementul returnat ultima dată de `next()`.
   - Această metodă poate fi apelată doar o dată pentru fiecare apel al metodei `next()`.
   - Aruncă o excepție de tip `IllegalStateException` dacă este apelată înainte de `next()` sau dacă a fost apelată deja după ultimul `next()`.

### Utilizarea Iteratorului
```java
List<String> list = new ArrayList<>();
list.add("apple");
list.add("banana");
list.add("cherry");

Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String item = it.next();
    System.out.println(item);
    if (item.equals("banana")) {
        it.remove(); // Elimină elementul "banana" din listă
    }
}
```

În acest exemplu, `Iterator` este folosit pentru a parcurge și eventual modifica o listă de șiruri de caractere. Metoda `remove()` este folosită pentru a elimina un element din listă în timpul iterației, ceea ce este sigur de făcut prin intermediul iteratorului, dar ar putea cauza probleme de concurență dacă s-ar încerca direct pe colecție.

`Iterator` este un instrument extrem de util în Java, permițând manipularea și accesarea flexibilă a elementelor din diverse tipuri de colecții.
