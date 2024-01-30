
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
