
Interfața `Map` din Java nu este parte a Java Collections Framework în sensul tradițional în care fac parte interfețele precum `List`, `Set`, sau `Queue`. Aceasta pentru că `Map` nu derivă din interfața `Collection`. Totuși, `Map` este adesea considerată parte a "Collections Framework" din punct de vedere conceptual, deoarece este o structură de date fundamentală care se ocupă cu stocarea și gestionarea datelor în formă de perechi cheie-valoare, similar cu celelalte structuri de date din framework.

### Despre Interfața `Map`

Interfața `Map` în Java este folosită pentru a stoca perechi de obiecte sub forma cheie-valoare, unde fiecare cheie este unică. Să aruncăm o privire la unele dintre caracteristicile și metodele fundamentale ale interfeței `Map`:

1. **Unicitatea Cheilor**: Într-un `Map`, fiecare cheie trebuie să fie unică, și fiecare cheie este asociată cu o valoare specifică. Dacă adaugi o valoare nouă folosind o cheie care există deja, valoarea existentă va fi înlocuită cu cea nouă.

2. **Operații Principale**:
   - **`put(K key, V value)`**: Adaugă o pereche cheie-valoare în map. Dacă cheia există deja, valoarea ei este înlocuită.
   - **`get(Object key)`**: Returnează valoarea asociată cu cheia specificată, sau `null` dacă cheia nu este găsită.
   - **`remove(Object key)`**: Elimină perechea cheie-valoare asociată cu cheia specificată și returnează valoarea, sau `null` dacă cheia nu este găsită.
   - **`containsKey(Object key)`**: Verifică dacă mapul conține cheia specificată.
   - **`containsValue(Object value)`**: Verifică dacă mapul conține una sau mai multe chei asociate cu valoarea specificată.
   - **`keySet()`**: Returnează un `Set` de toate cheile din map.
   - **`values()`**: Returnează o colecție de toate valorile din map.
   - **`entrySet()`**: Returnează un set de perechi cheie-valoare, fiecare fiind reprezentată de `Map.Entry<K, V>`.

3. **Iterație**: Poți itera printr-un map prin cheile sale, valorile sale, sau perechile cheie-valoare direct. Fiecare abordare este utilă în diferite contexte de programare.

4. **Implementări Comune**:
   - **`HashMap`**: O implementare bazată pe tabelă hash care oferă performanțe constante în timp pentru operațiile de bază (get și put), nesincronizată.
   - **`TreeMap`**: O implementare bazată pe tree map (red-black tree) care menține cheile în ordine sortată. Este utilă când este nevoie de un ordin sortat natural sau personalizat.
   - **`LinkedHashMap`**: Păstrează ordinea de inserție sau ordinea de acces a elementelor, fiind utilă când această ordine este importantă.

5. **Utilizare**:
   - `Map`-urile sunt extrem de utile pentru cazuri de utilizare care implică asocierea unor identificatori unici cu obiecte, cum ar fi un index de cărți într-o bibliotecă, unde fiecare carte poate fi accesată rapid utilizând un identificator specific.

Interfața `Map` oferă o flexibilitate remarcabilă și putere în gestionarea seturilor de date unde accesul rapid și eficient la elemente pe baza cheilor este esențial.

![image](https://github.com/adbejenaru/Theory/assets/128550128/0404ea41-c2e0-425b-bdc6-9aa8e543d147)

### Explicarea Funcționării `HashMap` în Java

`HashMap` în Java este o structură de date care stochează perechi de cheie-valoare și permite accesul rapid la valoare folosind cheia. Acesta este cum funcționează:

1. **Introducerea unei Perechi Cheie-Valoare**:
   - Când introduci o pereche cheie-valoare (de exemplu, `hashMap.put("hello", "world");`), Java folosește cheia pentru a genera un cod hash.
   - Codul hash este calculat folosind metoda `hashCode()` care este definită pe obiectul cheie.

2. **Determinarea Indexului în Array**:
   - Codul hash este folosit pentru a determina un index în array-ul intern al `HashMap`.
   - Calculul indexului ajută la plasarea eficientă a valorii în array pentru a minimiza căutările.

3. **Gestionarea Coliziunilor**:
   - Dacă două sau mai multe chei generează același index (cunoscute ca coliziuni), `HashMap` le gestionează stocând perechile cheie-valoare într-o listă înlănțuită (sau în structuri mai complexe, cum ar fi arborii roșu-negru, în versiunile mai recente de Java) la acel index.
   - Atunci când se caută o valoare, `HashMap` parcurge această listă folosind metoda `equals()` pentru a găsi cheia corectă și a returna valoarea asociată.

4. **Importanța `equals()` și `hashCode()`**:
   - Corectitudinea implementărilor `equals()` și `hashCode()` este crucială pentru performanța și acuratețea `HashMap`.
   - `equals()` trebuie să asigure că două obiecte considerate egale primesc același cod hash.
   - Consistența dintre `equals()` și `hashCode()` asigură că elementele sunt găsite corect chiar și după multe inserții și ștergeri.

Această structură permite `HashMap` să ofere inserții, ștergeri și accesări cu o complexitate temporală medie foarte rapidă, ideală pentru utilizare în aplicații care necesită acces rapid la date bazate pe chei.


