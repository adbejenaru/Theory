
### 3. Blocuri Sincronizate

Blocurile sincronizate permit sincronizarea unei secțiuni de cod, în loc de o metodă întreagă. Acest lucru se face folosind un bloc `synchronized` care primește un obiect ca monitor (sau lock). Doar un thread poate deține lock-ul unui obiect la un moment dat.

Exemplu de bloc sincronizat:
```java
class SharedResource {
    void method() {
        // Cod care nu necesită sincronizare
        synchronized(this) {
            // Cod care accesează resurse partajate
        }
        // Mai mult cod care nu necesită sincronizare
    }
}
```

În acest exemplu, doar secțiunea din interiorul blocului `synchronized` este sincronizată. Dacă un thread este în interiorul acestui bloc, orice alt thread care încearcă să intre în orice bloc `synchronized` pe aceeași instanță va trebui să aștepte până când primul thread părăsește blocul.

### Sfaturi Importante

- Utilizarea excesivă a sincronizării poate duce la probleme cum ar fi interblocajele (deadlocks) și poate reduce performanța.
- Este important să sincronizezi doar secțiunile de cod care au nevoie absolută de aceasta (accesul la resurse partajate).
- Este bine să păstrezi secțiunile sincronizate cât mai scurte posibil. 

Aceste concepte sunt esențiale în programarea multi-thread în Java și ajută la crearea de aplicații care gestionează mai eficient resursele și thread-urile.

Sigur, pentru a ilustra mai bine diferența, voi crea un exemplu în care sincronizăm doar o parte specifică a unei metode folosind un bloc sincronizat. Să presupunem că avem o clasă care reprezintă o bancă și dorește să proceseze tranzacții. În exemplul nostru, vom sincroniza doar secțiunea care actualizează balanța, permițând alte părți ale metodei să rămână nesincronizate.

```java
class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public void processTransaction(double amount, String transactionType) {
        System.out.println("Procesarea tranzacției: " + transactionType);

        synchronized(this) {
            // Doar actualizarea balanței este sincronizată
            if (transactionType.equals("deposit")) {
                balance += amount;
            } else if (transactionType.equals("withdrawal") && balance >= amount) {
                balance -= amount;
            }
            System.out.println("Tranzacție " + transactionType + " de " + amount + " lei. Balanță actuală: " + balance);
        }

        // Aici pot fi alte operații care nu necesită sincronizare
        // De exemplu, logarea tranzacției, trimis notificări etc.
    }
}

class TransactionThread extends Thread {
    private BankAccount account;
    private double amount;
    private String transactionType;

    public TransactionThread(BankAccount account, double amount, String transactionType) {
        this.account = account;
        this.amount = amount;
        this.transactionType = transactionType;
    }

    public void run() {
        account.processTransaction(amount, transactionType);
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount(1000);

        TransactionThread t1 = new TransactionThread(account, 500, "withdrawal");
        TransactionThread t2 = new TransactionThread(account, 200, "deposit");

        t1.start();
        t2.start();
    }
}
```

### Explicația Codului
- `BankAccount` este o clasă care reprezintă un cont bancar și conține o metodă `processTransaction` pentru procesarea tranzacțiilor.
- Blocul `synchronized` este folosit doar în jurul codului care actualizează balanța contului (`balance`). Aceasta este partea critică care trebuie să fie protejată de accesul concurent din partea mai multor thread-uri.
- Alte părți ale metodei `processTransaction`, cum ar fi afișarea mesajelor, nu sunt sincronizate, deoarece aceste operații nu modifică starea partajată (în acest caz, balanța contului).

### Beneficiul Acestui Abord
Acest model permite ca alte operații din metoda `processTransaction` să se execute fără a aștepta blocarea sincronizării. Acest lucru este benefic atunci când avem cod care nu necesită sincronizare și nu dorim să-l încetinim inutil prin sincronizarea întregii metode.

__________________________________________________________________________________________________________________________________________________________-

În Java, metodele `wait()`, `notify()` și `notifyAll()` sunt folosite în contextul programării multi-thread pentru a permite thread-urilor să comunice între ele și să coordoneze acțiunile lor. Aceste metode sunt utilizate în contextul sincronizării și sunt disponibile în orice obiect, deoarece fac parte din clasa `Object`. Sunt esențiale pentru rezolvarea problemelor de tip producer-consumer, blocare și așteptare condițională.

### 1. `wait()`
Metoda `wait()` este folosită pentru a face un thread să aștepte până când un alt thread îl notifică. Când un thread apelează `wait()`, acesta eliberează lock-ul pe obiectul pe care îl deține și trece în starea de așteptare. Thread-ul rămâne în această stare până când un alt thread apelează `notify()` sau `notifyAll()` pe același obiect.

- Utilizare:
    ```java
    synchronized (obiect) {
        while (/* condiție nu este îndeplinită */) {
            obiect.wait();
        }
        // Continuă executarea când este notificat
    }
    ```

### 2. `notify()`
Metoda `notify()` este utilizată pentru a notifica un singur thread care așteaptă pe același obiect. Dacă există mai multe thread-uri care așteaptă, `notify()` va trezi doar unul dintre ele (alegerea thread-ului nu este garantată și depinde de implementarea JVM).

- Utilizare:
    ```java
    synchronized (obiect) {
        // Modifică starea obiectului
        obiect.notify();
    }
    ```

### 3. `notifyAll()`
Metoda `notifyAll()` funcționează similar cu `notify()`, dar trezește toate thread-urile care așteaptă pe obiectul respectiv. Acest lucru este util când există mai multe thread-uri care așteaptă pe diferite condiții și fiecare trebuie să verifice dacă condiția sa particulară a fost îndeplinită.

- Utilizare:
    ```java
    synchronized (obiect) {
        // Modifică starea obiectului
        obiect.notifyAll();
    }
    ```

### Considerații Importante
- Aceste metode trebuie să fie apelate dintr-un bloc sincronizat (`synchronized`). Încercarea de a apela `wait()`, `notify()`, sau `notifyAll()` fără sincronizare va rezulta într-o excepție de tip `IllegalMonitorStateException`.
- `wait()` trebuie de obicei să fie utilizat într-un loop care verifică o anumită condiție. Aceasta se datorează faptului că thread-ul poate fi trezit (printr-un `notify()` sau `notifyAll()`) înainte ca condiția dorită să fie îndeplinită sau din cauza unui "false alarm" (cunoscut sub numele de "spurious wakeup").
- Este important să alegeți între `notify()` și `notifyAll()` în funcție de situație. `notifyAll()` este mai sigur în cazul în care există mai multe condiții de așteptare, dar poate fi mai puțin eficient din punct de vedere al performanței, deoarece trezește toate thread-urile așteptând.

Aceste metode sunt cruciale pentru gestionarea corectă și eficientă a thread-urilor în Java, permițând sincronizarea complexă și comunicația între thread-uri.
