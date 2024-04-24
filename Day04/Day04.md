Reflection în Java este un proces prin care un program poate interoga sau modifica structura internă a clasei la runtime. Aceasta înseamnă că un program Java poate analiza sau "reflecta" pe componentele sale, cum ar fi clasele, interfețele, câmpurile și metodele, chiar și dacă la momentul scrierii codului detaliile exacte despre aceste componente nu sunt cunoscute. În continuare voi detalia câteva aspecte importante despre reflection în Java:

1. **Acces la Clase**: Reflection permite programelor să obțină obiectul `Class` asociat cu clasele disponibile în program. Aceasta este punctul de plecare pentru majoritatea operațiilor de reflection. Poți obține un obiect `Class` folosind `Class.forName()` dacă știi numele clasei sau `.getClass()` dacă ai o instanță a clasei.

2. **Inspectarea Claselor**: Odată ce ai un obiect `Class`, poți interoga clasa pentru a afla structura sa, cum ar fi metodele, câmpurile, constructorii, superclasele, interfețele implementate și alte detalii. De exemplu, metodele `getMethods()`, `getFields()`, `getConstructors()`, `getSuperclass()` și `getInterfaces()` sunt utilizate pentru aceste scopuri.

3. **Acces la Membrii**: Poți accesa membrii individuali ai clasei (cum ar fi câmpurile și metodele) utilizând metode specifice, care returnează obiecte de tip `Field`, `Method` sau `Constructor`. Aceste obiecte permit ulterior manipularea și accesul la acești membri, inclusiv accesul la membrii privați care, în mod normal, nu sunt accesibili din afara clasei.

4. **Instantierea Obiectelor**: Reflection poate fi folosit pentru a crea instanțe ale claselor folosind constructorii obținuți. Aceasta este utilă pentru crearea obiectelor atunci când tipul lor exact nu este cunoscut până la runtime.

5. **Apelarea Metodelor**: Poți folosi reflection pentru a invoca metode pe obiecte într-un mod dinamic. Acest lucru înseamnă că metoda poate fi aleasă și apelată la runtime bazându-te pe condiții care nu sunt cunoscute la momentul compilării.

6. **Modificarea Câmpurilor**: Reflection permite modificarea valorilor câmpurilor obiectelor, chiar dacă aceste câmpuri sunt private sau finale, sub rezerva unor restricții de securitate.

Reflection este un instrument puternic, dar vine și cu dezavantaje, cum ar fi performanța scăzută comparativ cu accesul direct la câmpuri sau metode, riscuri de securitate dacă nu este gestionat corespunzător, și poate complica designul aplicației. Este cel mai bine utilizat în cazuri specifice unde flexibilitatea la runtime este esențială, cum ar fi în framework-uri, biblioteci generice, sau pentru interoperabilitatea cu codul care nu a fost disponibil la timpul compilării.

## Exemplul 1.

### 1. Definirea pachetului
```java
package reflectionexample.reflection.example01;
```
Aici, codul este organizat într-un pachet specific, ceea ce este o bună practică pentru organizarea codului în proiecte Java mai mari.

### 2. Importarea clasei necesare
```java
import java.lang.reflect.Method;
```
Se importă clasa `Method` din pachetul `java.lang.reflect`. Aceasta este folosită pentru a reprezenta metodele unei clase la nivel de cod.

### 3. Definirea clasei și metodei principale
```java
public class ReflectionExample {
    public static void main(String[] args) throws ClassNotFoundException {
```
Aici, se definește o clasă publică `ReflectionExample` cu o metodă `main`, care este punctul de intrare într-un program Java. Metoda `main` declară că poate arunca o excepție `ClassNotFoundException`, care se poate întâmpla dacă numele clasei specificat în `Class.forName` nu este găsit.

### 4. Obținerea obiectului Class
```java
        Class<?> clazz = Class.forName("java.util.ArrayList");
```
Această linie de cod obține obiectul `Class` pentru clasa `java.util.ArrayList`. Operatorul `Class<?>` este o modalitate generică de a se referi la orice clasă, iar `Class.forName` încarcă clasa specificată prin numele său complet.

### 5. Extracția și afișarea metodelor
```java
        Method[] methods = clazz.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println("Method is " + method.getName());
        }
    }
}
```
`getDeclaredMethods()` este apelat pe obiectul `Class` pentru a recupera toate metodele declarate de clasa `ArrayList` (incluzând metodele private, protejate și pachetului, dar nu și cele moștenite). Apoi, pentru fiecare metodă obținută, se afișează numele metodei utilizând `System.out.println`.

### Rezumatul funcționalității
Codul utilizează reflection pentru a interoga structura clasei `ArrayList` și a afișa numele fiecărei metode. Aceasta poate fi folosită pentru a înțelege structura internă a unei clase fără a consulta documentația sau codul sursă, sau poate fi utilă în dezvoltarea unor unelte care necesită procesare dinamică a informațiilor despre obiectele de clasă. Această tehnică este des utilizată în dezvoltarea de framework-uri și biblioteci.

## Exemplul 2.

### Clasa `Person`
Clasa `Person` are două proprietăți private: `name` și `age`. Există două constructori, unul fără parametri și unul cu parametri. Clasa include metode getter și setter pentru ambele proprietăți, precum și o metodă `printDetails()` care afișează detaliile despre `Person`.

### Clasa `ReflectionDemo`
Clasa `ReflectionDemo` folosește reflection pentru a manipula și invoca metode pe instanța `Person`.

1. **Crearea Instanței**:
   ```java
   Person person = new Person();
   ```
   Se creează o instanță a clasei `Person` folosind constructorul fără parametri.

2. **Obținerea Clasei**:
   ```java
   Class<?> clazz = person.getClass();
   ```
   Se obține obiectul `Class` asociat instanței `person`. Acesta este folosit pentru a accesa informații despre structura clasei.

3. **Accesul și Modificarea Câmpului `name`**:
   ```java
   Field nameField = clazz.getDeclaredField("name");
   nameField.setAccessible(true);
   nameField.set(person, "Andrei");
   ```
   Se obține obiectul `Field` pentru câmpul `name` și se setează acest câmp ca accesibil (chiar dacă este privat). Apoi, valoarea acestui câmp este modificată în "Andrei".

4. **Accesul și Modificarea Câmpului `age`**:
   ```java
   Field ageField = clazz.getDeclaredField("age");
   ageField.setAccessible(true);
   ageField.setInt(person, 30);
   ```
   Similar cu câmpul `name`, se obține acces la câmpul `age`, se face accesibil și apoi i se atribuie valoarea 30.

5. **Invocarea Metodei `printDetails()`**:
   ```java
   Method printMethod = clazz.getDeclaredMethod("printDetails");
   printMethod.setAccessible(true);
   printMethod.invoke(person);
   ```
   Se obține metoda `printDetails`, se face accesibilă și este invocată pe instanța `person`. Aceasta va afișa "Numele este Andrei iar varsta este 30".

### Utilitatea și Limitările Reflection
Această demonstrație arată cum reflection poate fi folosit pentru a ocoli accesul normal la metode și câmpuri, permițând modificarea și invocarea acestora chiar dacă sunt private. Astfel, reflection poate fi extrem de util pentru testarea, depurarea și dezvoltarea de framework-uri, dar trebuie folosit cu precauție datorită impactului său asupra securității și performanței. Facilitarea accesului la membrii privați poate încălca principiul încapsulării, iar manipularea datelor în acest mod poate duce la comportamente neașteptate ale programului.
