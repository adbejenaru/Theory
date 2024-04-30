

### Metoda `sortStudentsByName()`

Această metodă este folosită pentru a sorta studenții din clasă în ordine alfabetică după nume. Iată cum funcționează:

- **`students.sort(Comparator.comparing(Student::getName));`**: Aceasta este linia cheie unde se întâmplă sortarea. Lista `students` conține obiecte de tip `Student`, iar fiecare `Student` are un atribut `name`. Funcția `Comparator.comparing(Student::getName)` creează un comparator care compară studenții pe baza numelor lor. Acest comparator este folosit de metoda `sort` a listei pentru a aranja studenții în ordine alfabetică.
- **`System.out.println("Students have been sorted by name.");`**: După ce lista a fost sortată, se afișează un mesaj în consolă pentru a indica faptul că sortarea a fost efectuată.

### Metoda `isStudentPresent(String name)`

Această metodă verifică dacă există un student cu un anumit nume în lista de studenți. Iată componentele cheie:

- **`students.stream()`**: Această expresie transformă lista de studenți într-un flux (`stream`), care este o secvență de elemente (în acest caz, studenți) ce suportă operații secvențiale și paralele. Folosirea fluxurilor facilitează procesarea colecțiilor de date într-o manieră funcțională.
- **`.anyMatch(student -> student.getName().equals(name))`**: Metoda `anyMatch` este o operație terminală care primește un predicat (o funcție care returnează un boolean) și verifică dacă oricare dintre elementele fluxului îndeplinește condiția specificată. În acest caz, predicatul verifică dacă numele oricărui student este egal cu `name` (numele primit ca parametru). Dacă găsește cel puțin un student cu numele respectiv, `anyMatch` returnează `true`; altfel, returnează `false`.
- **Return value**: Valoarea returnată de metoda `isStudentPresent` este rezultatul apelului `anyMatch`, adică `true` dacă studentul este prezent în clasă sau `false` dacă nu este.

Aceste metode ilustrează cum puteți manipula și interoga liste în Java folosind API-ul de colecții și fluxuri, oferindu-vă un control puternic și flexibil asupra datelor.
