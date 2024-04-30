

### Metoda `sortStudentsByName()`

Această metodă este folosită pentru a sorta studenții din clasă în ordine alfabetică după nume. Iată cum funcționează:

- **`students.sort(Comparator.comparing(Student::getName));`**: Aceasta este linia cheie unde se întâmplă sortarea. Lista `students` conține obiecte de tip `Student`, iar fiecare `Student` are un atribut `name`. Funcția `Comparator.comparing(Student::getName)` creează un comparator care compară studenții pe baza numelor lor. Acest comparator este folosit de metoda `sort` a listei pentru a aranja studenții în ordine alfabetică.
- **`System.out.println("Students have been sorted by name.");`**: După ce lista a fost sortată, se afișează un mesaj în consolă pentru a indica faptul că sortarea a fost efectuată.

### Metoda `isStudentPresent(String name)`

Această metodă verifică dacă există un student cu un anumit nume în lista de studenți. Iată componentele cheie:

- **`students.stream()`**: Această expresie transformă lista de studenți într-un flux (`stream`), care este o secvență de elemente (în acest caz, studenți) ce suportă operații secvențiale și paralele. Folosirea fluxurilor facilitează procesarea colecțiilor de date într-o manieră funcțională.
- **`.anyMatch(student -> student.getName().equals(name))`**: Metoda `anyMatch` este o operație terminală care primește un predicat (o funcție care returnează un boolean) și verifică dacă oricare dintre elementele fluxului îndeplinește condiția specificată. În acest caz, predicatul verifică dacă numele oricărui student este egal cu `name` (numele primit ca parametru). Dacă găsește cel puțin un student cu numele respectiv, `anyMatch` returnează `true`; altfel, returnează `false`.
- **Return value**: Valoarea returnată de metoda `isStudentPresent` este rezultatul apelului `anyMatch`, adică `true` dacă studentul este prezent în clasă sau `false` dacă nu este.

Desigur, hai să detaliem funcționarea metodei `isStudentPresent(String name)` în contextul gestionării unei clase de studenți în Java:

### Metoda `isStudentPresent(String name)`

Această metodă verifică dacă există un student cu un anumit nume în lista de studenți a clasei. Iată cum funcționează:

1. **`students.stream()`**: Această linie transformă lista `students` într-un flux (`stream`). Fluxurile în Java permit o serie de operații de procesare a datelor, cum ar fi filtrarea, sortarea sau alte transformări, care sunt executate într-o manieră eficientă și adesea expresivă. Fluxul generat conține toate obiectele `Student` din lista `students`.

2. **`.anyMatch(student -> student.getName().equals(name))`**: Aceasta este o operație de agregare care verifică dacă oricare dintre elementele fluxului îndeplinește condiția specificată în predicatul dat. Predicatul este o expresie lambda:
   - `student -> student.getName().equals(name)`: Aici, pentru fiecare `student` din flux, se apelează metoda `getName()` care returnează numele studentului. Apoi, acest nume este comparat cu șirul de caractere `name` primit ca argument al metodei `isStudentPresent`. 
   - `equals(name)`: Aceasta este metoda de comparare standard a două șiruri de caractere în Java, care returnează `true` dacă șirurile sunt identice.

3. **Valoarea de retur**: Operația `anyMatch` returnează `true` dacă predicatul este adevărat pentru cel puțin un element al fluxului (adică dacă există cel puțin un student cu numele dat în listă). Dacă nu există niciun student cu acel nume, returnează `false`.

În rezumat, metoda `isStudentPresent` folosește fluxuri pentru a verifica într-o manieră eficientă și concisă prezența unui student cu un nume specific într-o listă. Aceasta exemplifică puterea fluxurilor în Java pentru efectuarea de interogări și verificări asupra colecțiilor de date.
