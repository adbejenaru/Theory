
Prima imagine, intitulată "Înainte de 2004: un computer cu un singur nucleu", descrie componentele unui procesor cu un singur nucleu. Iată punctele cheie și diagrama:

1. **Nucleu (Core)**: Se referă la partea hardware a unui computer care execută o serie de instrucțiuni ale mașinii.
2. **Unitate de Instrucțiune (Instruction Unit)**: Aceasta este responsabilă pentru citirea, decodarea și executarea instrucțiunilor mașinii dintr-un program.
3. **Unități Funcționale (Functional Units)**: Acestea efectuează operațiuni reale pe date, cum ar fi shiftarea, adunarea și înmulțirea.
4. **Registre (Registers)**: Acestea sunt memorii de mare viteză utilizate pentru a păstra rezultatele intermediare.
5. **Cache L1 și L2**: Sunt niveluri de memorie cache care stochează temporar datele pentru a reduce timpul de acces la memoria principală.
6. **Memoria Principală (Main Memory)**: Este memoria de bază a computerului unde se stochează datele și instrucțiunile programelor.

A doua imagine, intitulată "2004 înainte: Computere Multi-core...", compară strategiile de creștere a puterii de procesare înainte și după 2004.

- **Înainte de 2004 (single-core)**: Puterea de procesare era crescută prin mărirea frecvențelor ceasului, ceea ce ducea la probleme de disipare a energiei și genera căldură excesivă.
- **După 2004 (multi-core)**: Procesoarele multi-core cresc puterea de procesare prin adăugarea mai multor nuclee, în loc să crească frecvența unui singur nucleu, ceea ce ajută la gestionarea mai eficientă a căldurii și a consumului de energie.

Diagrama din a doua imagine arată două nuclee separate, fiecare cu propria unitate de instrucțiune, unități funcționale și registre, indicând cum procesorii multi-core pot executa mai multe instrucțiuni simultan.
__________________________________________________________________________________________________________________

Termenul "proces" în informatică se referă la o instanță a unui program care este în execuție pe un computer. În momentul în care un program este lansat pentru a rula, sistemul de operare creează un proces pentru a gestiona execuția acestuia. Iată ce implică un proces:

1. **Imaginea codului mașină executabil**: Aceasta este codul binar al programului care poate fi executat direct de către procesor.

2. **Memoria**: Un proces are alocată propria sa zonă de memorie, care include:
   - **Cod**: Segmentul de memorie unde este stocat codul executabil al procesului.
   - **Date**: Segmentul de memorie care stochează variabilele și structurile de date folosite de proces.
   - **Call Stack (Stiva de apeluri)**: Aceasta este o structură de date care ține evidența apelurilor de funcții, parametrilor lor și variabilelor locale.
   - **Heap (Grămada)**: Partea de memorie utilizată pentru alocarea dinamică a memoriei, adică pentru obiecte și date care au nevoie de o durată de viață variabilă, nu doar pentru durata unei funcții.

3. **Descriptorii de Resurse**: Aceștia sunt identificatori folosiți de un proces pentru a accesa resursele sistemului, cum ar fi fișierele, conexiunile de rețea etc.

4. **Atribute de Securitate**: Acestea definesc permisiunile procesului, cum ar fi drepturile de a citi sau scrie în fișiere sau de a accesa anumite resurse ale sistemului.

5. **Starea Procesorului (Context)**: Include informații despre starea curentă a procesorului pentru procesul respectiv, cum ar fi conținutul registrelor. Aceasta este esențială pentru a putea opri temporar execuția unui proces și a-l relua mai târziu fără a pierde informații (de exemplu, în multitasking).

În esență, un proces este o "bucată" de software care se execută, având alocate resurse și un context propriu, ceea ce îi permite să ruleze ca și cum ar avea controlul asupra întregului sistem, chiar dacă, în realitate, sistemul de operare gestionează executarea simultană a mai multor procese.
___________________________________________________________________________________________________________________________________

Termenul "thread" se referă la cea mai mică secvență de instrucțiuni programate care poate fi gestionată în mod independent de un sistem de operare. Iată o explicație detaliată:

1. **Există în cadrul unui proces**: Un thread nu funcționează singur; el este o parte a unui proces. Un proces poate avea mai multe thread-uri, care execută diferite părți ale programului în paralel.

2. **Fiecare proces are cel puțin un thread**: Acesta este cunoscut ca thread-ul principal sau "main thread". Este thread-ul inițial de la care pot fi create alte thread-uri.

3. **Thread-urile împărtășesc resursele procesului**: Deoarece toate thread-urile dintr-un proces rulează în același spațiu de memorie, ele pot accesa aceleași date și resurse, cum ar fi memoria (de exemplu, heap-ul) și descriptorii de fișiere. Aceasta le permite să comunice între ele mai eficient, dar, de asemenea, necesită sincronizare pentru a evita conflictele.

4. **Execuția Multithread**: Aceasta permite unui proces să execute mai multe sarcini sau sub-sarcini în mod concomitent. Acest lucru poate îmbunătăți performanța aplicațiilor care execută mai multe operațiuni care pot fi realizate în paralel sau pot aștepta în mod independent (de exemplu, așteptarea răspunsurilor de la rețea sau de la utilizator).

Multithreading-ul este o caracteristică esențială a platformei Java, permițând dezvoltatorilor să creeze aplicații eficiente care pot gestiona multiple fluxuri de lucru simultan. De exemplu, într-o aplicație GUI, un thread poate gestiona interfața utilizatorului, în timp ce alte thread-uri pot procesa datele sau pot efectua operațiuni de intrare/ieșire fără a bloca interfața utilizatorului.
_________________________________________________________________________________________________________________________________-

Programarea multithreaded în Java se referă la abilitatea limbajului Java de a suporta execuția concomitentă, adică execuția simultană a mai multor secvențe de cod. Java oferă un set robust de instrumente și clase care permit dezvoltatorilor să creeze și să gestioneze thread-uri, să sincronizeze codul pentru a evita condițiile de întrecere și să utilizeze modele de execuție paralelă. Iată câteva concepte cheie:

1. **Suport încorporat pentru programarea concurentă**: Java oferă facilități încorporate pentru a permite execuția simultană a mai multor părți ale unei aplicații.

2. **Construcții de concurență de nivel scăzut**:
   - **Thread și Runnable**: Clasa `Thread` și interfața `Runnable` sunt mijloacele de bază pentru a crea thread-uri în Java. Implementezi interfața `Runnable` cu codul pe care vrei să-l execute un thread și apoi creezi o instanță de `Thread` pentru a-l rula.
   - **Cuvântul cheie synchronized și blocări implicite**: Pentru a gestiona accesul concurent la resurse comune, Java folosește cuvântul cheie `synchronized` pentru a bloca un obiect în timp ce un thread îl folosește.

3. **Construcții de concurență de nivel înalt**:
   - **Pachetul java.util.concurrent**: Acesta oferă clase avansate pentru gestionarea concurenței, precum noi tipuri de lock-uri, thread pool-uri și structuri de date concurente.
   - **Clase Synchronizer**: Clase precum `Semaphore` și `Exchanger` sunt folosite pentru a sincroniza thread-uri în situații specifice.
   - **Colecții Thread-safe**: Sunt colecții proiectate să fie utilizate în medii multithread fără a fi nevoie de sincronizare externă.
   - **Variabile Atomice, Lock-uri și condiții**: Acestea oferă un control mai fin al sincronizării, permitând operațiuni atomice pe variabile (adică executate complet fără întrerupere) și modele de lock-uri mai complexe.
   - **Executori și ThreadPool-uri**: Facilități pentru gestionarea unui set de thread-uri pentru execuția task-urilor. ThreadPool-urile reutilizează thread-uri pentru a executa mai multe sarcini, ceea ce este mai eficient decât crearea unui nou thread pentru fiecare sarcină.
   - **Paralelism Fork/Join**: Este un model de programare introdus în Java 7 care ajută la utilizarea eficientă a procesorilor multi-core prin descompunerea sarcinilor în sub-sarcini care pot fi procesate în paralel, apoi combinând rezultatele sub-sarcinilor în rezultatul final.

Prin utilizarea acestor instrumente, programatorii Java pot scrie aplicații care efectuează mai multe operații în paralel, crescând astfel performanța și eficiența aplicațiilor, în special pe mașini cu mai multe nuclee de procesare.
