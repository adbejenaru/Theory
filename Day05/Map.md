
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

### Cum Funcționează `HashMap` în Java

**1. Introducerea unei Perechi Cheie-Valoare:**
- **Generarea Codului Hash:**
  - Când adaugi o pereche cheie-valoare folosind `hashMap.put("hello", "world");`, Java invocă metoda `hashCode()` definită pentru obiectul cheie pentru a obține un cod hash. Această metodă trebuie să returneze un număr întreg, indiferent de tipul de date al cheii.
- **Determinarea Indexului în Array:**
  - Codul hash obținut este apoi folosit pentru a calcula indexul în array-ul intern al `HashMap`. Acest index este calculat de obicei prin aplicarea unei funcții de reducere a hashului, cum ar fi `(hashCode ^ (hashCode >>> 16)) & (capacitate - 1)`, unde capacitatea este mărimea internă a array-ului, de obicei o putere a lui 2.

**2. Gestionarea Coliziunilor:**
- **Structura de Date pentru Coliziuni:**
  - Dacă două chei diferite produc același index de array sau același cod hash după procesarea funcției de hash, acestea sunt plasate în același "bucket". Inițial, `HashMap` folosea liste înlănțuite pentru a gestiona aceste coliziuni. Cu toate acestea, începând cu Java 8, dacă un bucket depășește un anumit prag de ocupare (de obicei 8 elemente), lista înlănțuită este transformată într-un arbore roșu-negru pentru a îmbunătăți performanța căutării.
- **Căutarea Valoarei:**
  - Atunci când se execută o operație de căutare, cum ar fi `hashMap.get("key")`, `HashMap` utilizează hash-ul cheii pentru a identifica rapid bucket-ul corect, iar apoi parcurge structura de date asociată bucket-ului (fie listă, fie arbore) utilizând metoda `equals()` pentru a găsi și returna valoarea asociată cheii.

**3. Importanța Metodelor `equals()` și `hashCode()`:**
- **Corectitudinea Implementării:**
  - Pentru ca `HashMap` să funcționeze corect și eficient, este esențial ca obiectele utilizate ca chei să implementeze adecvat metodele `equals()` și `hashCode()`. Metoda `equals()` trebuie să asigure că două obiecte considerate egale generează același cod hash.
- **Consistența:**
  - Consistența dintre `equals()` și `hashCode()` asigură că cheile egale vor fi întotdeauna mapate în același bucket, iar `HashMap` va putea găsi corect elementele chiar și după multiple inserții și ștergeri, oferind acces rapid și predictibil.

**4. Performanța `HashMap`:**
- **Complexitate Temporală:**
  - `HashMap` oferă, în cazul ideal, o complexitate temporală medie \(O(1)\) pentru operațiile de adăugare, ștergere și accesare. Aceasta este una dintre principalele sale avantaje, făcând-o extrem de utilă pentru aplicații care necesită acces rapid la date bazate pe chei. 

În concluzie, `HashMap` este un instrument puternic și versatil în Java, fiind adecvat pentru gestionarea eficientă a seturilor de date mari unde accesul rapid la elemente este esențial. Implementările corecte ale metodelor `hashCode()` și `equals()` sunt fundamentale pentru a asigura performanța optimă a acestei structuri de date.

