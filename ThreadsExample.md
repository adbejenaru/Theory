
```java
class MyThread extends Thread {
    private int threadNumber;

    public MyThread(int threadNumber) {
        this.threadNumber = threadNumber;
    }

    @Override
    public void run() {
        System.out.println("Thread #" + threadNumber + " a început.");
        // Simulăm o sarcină care durează un anumit timp
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread #" + threadNumber + ", i=" + i);
            // Dormim pentru 500 de milisecunde
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println("Thread #" + threadNumber + " a fost întrerupt.");
                // Restabilirea statusului de întrerupere
                Thread.currentThread().interrupt();
                // Întrerupem execuția acestui thread
                return;
            }
        }
        System.out.println("Thread #" + threadNumber + " s-a terminat.");
    }
}

public class MainClass {
    public static void main(String[] args) {
        System.out.println("Programul începe.");

        MyThread thread1 = new MyThread(1);
        MyThread thread2 = new MyThread(2);
        MyThread thread3 = new MyThread(3);

        // Pornim thread-urile
        thread1.start();
        thread2.start();
        thread3.start();

        // Așteptăm ca toate thread-urile să se termine
        try {
            thread1.join();
            thread2.join();
            thread3.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread a fost întrerupt.");
        }

        System.out.println("Toate thread-urile s-au terminat. Programul se termină.");
    }
}
```

În acest cod, am adăugat o buclă for în metoda `run()` pentru a simula o sarcină repetitivă și am folosit `Thread.sleep(500)` pentru a introduce o întârziere de 500 milisecunde între iterații, simulând astfel o procesare care durează ceva timp.

Metoda `join()` este folosită pentru a aștepta ca thread-urile să se termine înainte de a continua execuția în thread-ul principal (`main`). Acest lucru este important pentru a asigura că programul principal nu se termină înainte ca toate thread-urile să-și finalizeze execuția. Dacă un thread este întrerupt în timp ce așteaptă (prin `join()`), va arunca o `InterruptedException`, pe care o prindem și o tratăm într-un bloc `try-catch`.

A aștepta ca thread-urile să se termine înainte de a continua execuția în thread-ul principal (main) înseamnă că programul principal va suspenda execuția până când toate thread-urile lansate de acesta își încheie sarcinile. Acest lucru se realizează prin folosirea metodei `join()` pe fiecare thread creat.

Metoda `join()` este o metodă de instanță a clasei `Thread` care blochează execuția curentă a thread-ului până când thread-ul pe care a fost apelată metoda `join()` își termină execuția. Dacă `join()` este apelată în thread-ul principal, thread-ul principal va aștepta până când thread-ul respectiv se termină.

Acest mecanism este important din mai multe motive:

1. **Finalizare ordonată**: Asigură că toate procesele secundare (thread-urile) au terminat sarcinile înainte de a încheia programul. Asta poate fi necesar pentru că thread-urile pot executa sarcini critice ale căror rezultate sunt necesare mai departe.

2. **Prevenirea erorilor de date**: Dacă thread-ul principal ar continua să execute și să termine înainte ca thread-urile secundare să se încheie, aceasta ar putea duce la situații unde resursele folosite de thread-uri (cum ar fi fișiere sau conexiuni la baza de date) ar putea fi închise sau datele ar putea fi incomplete sau incoerente.

3. **Coerența rezultatelor**: În multe cazuri, thread-urile secundare calculează date care trebuie să fie combinate sau verificate de thread-ul principal înainte ca programul să poată termina în mod corespunzător.

4. **Evitarea întreruperii premature**: Dacă thread-ul principal ar termina execuția (de exemplu, dacă ajunge la sfârșitul metodei `main()`), întregul proces ar putea fi terminat de către sistemul de operare, ceea ce ar însemna că toate thread-urile sale ar fi întrerupte brusc, chiar dacă nu și-au completat execuția.

Prin urmare, `join()` este o unealtă esențială în gestionarea execuției ordonate și asincrone în programarea multithreaded.





Sigur, vă voi oferi un exemplu simplu în Java care ilustrează un caz în care un thread intră în starea "Blocked/Waiting". În acest exemplu, vom folosi două thread-uri: unul va aștepta finalizarea celuilalt folosind metoda `join()`, care este o modalitate comună de a pune un thread în starea de așteptare.

### Exemplu de Cod

```java
public class ThreadExample {

    public static void main(String[] args) throws InterruptedException {
        // Crearea primului thread
        Thread thread1 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    // Simulăm o operațiune care durează 2 secunde
                    Thread.sleep(2000);
                    System.out.println("Thread 1 termină execuția.");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        // Crearea celui de-al doilea thread
        Thread thread2 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    // Așteptăm ca thread1 să termine
                    System.out.println("Thread 2 așteaptă finalizarea Thread 1.");
                    thread1.join();
                    System.out.println("Thread 2 începe execuția după finalizarea Thread 1.");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        // Start pentru ambele thread-uri
        thread1.start();
        thread2.start();

        // Așteptăm ca ambele thread-uri să termine pentru a finaliza programul
        thread1.join();
        thread2.join();

        System.out.println("Ambele thread-uri au terminat execuția.");
    }
}
```

### Explicație

- **Thread 1**: Simulează o operațiune care durează 2 secunde.
- **Thread 2**: Așteaptă finalizarea lui Thread 1 folosind `thread1.join()`. Astfel, Thread 2 intră în starea "Waiting" până când Thread 1 își încheie execuția.
- **`main`**: Pornim ambele thread-uri și așteptăm finalizarea lor folosind `join()` pe ambele. Acest lucru asigură că programul principal (`main`) nu se va termina înainte de finalizarea thread-urilor.

Când rulați acest cod, veți observa că Thread 2 va intra în starea de așteptare până când Thread 1 termină execuția, după care va începe propriul său proces de execuție. Acest exemplu este simplificat pentru a ilustra conceptul; în practică, gestionarea thread-urilor poate fi mai complexă și necesită atenție la detalii precum sincronizarea și evitarea condițiilor de blocare.

În exemplul dat, `thread1.join()` este utilizat pentru a face ca thread-ul curent (în acest caz, `thread2`) să aștepte finalizarea lui `thread1` înainte de a continua execuția sa. Deci, când apelăm `thread2.start()`, `thread2` începe execuția, dar ajunge la punctul unde se află `thread1.join()`, ceea ce face ca `thread2` să aștepte ca `thread1` să se termine înainte de a continua.

Simplu spus, `thread1.join()` face ca `thread2` să se aștepte până când `thread1` termină execuția sa, astfel încât ordinea de execuție devine astfel:

1. `thread1` este pornit folosind `thread1.start()`.
2. `thread2` este pornit folosind `thread2.start()`.
3. `thread2` ajunge la `thread1.join()` și așteaptă ca `thread1` să se termine.
4. După ce `thread1` se termină, `thread2` continuă execuția sa și afișează mesajele ulterioare.

Deci, `thread1` se execută înainte de `thread2` în acest scenariu, datorită utilizării `thread1.join()`.
