Comunicarea între threaduri în Java utilizând metodele `wait()`, `notify()` și `notifyAll()` se bazează pe mecanismele de sincronizare oferite de limbajul Java pentru a gestiona accesul la resurse comune și a coordona execuția threadurilor.

### Metodele `wait()`, `notify()` și `notifyAll()`

1. **`wait()`**: Oprește execuția threadului curent și îl plasează în stare de așteptare (waiting) până când un alt thread apelează `notify()` sau `notifyAll()` pe același obiect de blocare (lock). `wait()` trebuie apelată din interiorul unui bloc sincronizat.

2. **`notify()`**: Trezește un singur thread aflat în așteptare pe același obiect de blocare. Alegerea threadului care va fi trezit este nedeterminată.

3. **`notifyAll()`**: Trezește toate threadurile aflate în așteptare pe același obiect de blocare. Fiecare dintre acestea va trebui să recâștige blocarea obiectului înainte de a continua execuția.

### Exemplu Practic

Vom crea un exemplu simplu în care un thread produce date și alt thread consumă datele produse, folosind metodele `wait()`, `notify()` și `notifyAll()` pentru a coordona accesul la o resursă comună.

```java
class SharedResource {
    private int data;
    private boolean available = false;

    public synchronized void produce(int value) {
        while (available) {
            try {
                wait();
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Thread interrupted");
            }
        }
        data = value;
        available = true;
        System.out.println("Produced: " + data);
        notify();
    }

    public synchronized void consume() {
        while (!available) {
            try {
                wait();
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Thread interrupted");
            }
        }
        available = false;
        System.out.println("Consumed: " + data);
        notify();
    }
}

class Producer extends Thread {
    private final SharedResource resource;

    public Producer(SharedResource resource) {
        this.resource = resource;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            resource.produce(i);
        }
    }
}

class Consumer extends Thread {
    private final SharedResource resource;

    public Consumer(SharedResource resource) {
        this.resource = resource;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            resource.consume();
        }
    }
}

public class WaitNotifyExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        Producer producer = new Producer(resource);
        Consumer consumer = new Consumer(resource);

        producer.start();
        consumer.start();
    }
}
```

### Explicația Codului

1. **Clasa `SharedResource`**:
    - `produce(int value)`: Metoda folosită de threadul producător pentru a genera și seta o valoare în resursa partajată.
        - Dacă resursa este deja disponibilă (`available` este `true`), threadul intră în stare de așteptare (`wait()`).
        - Setează valoarea, marchează resursa ca disponibilă și notifică un thread aflat în așteptare (`notify()`).
    - `consume()`: Metoda folosită de threadul consumator pentru a prelua și consuma valoarea din resursa partajată.
        - Dacă resursa nu este disponibilă (`available` este `false`), threadul intră în stare de așteptare (`wait()`).
        - Marchează resursa ca indisponibilă și notifică un thread aflat în așteptare (`notify()`).

2. **Clasele `Producer` și `Consumer`**:
    - `Producer` apelează metoda `produce` de 10 ori, generând valori de la 0 la 9.
    - `Consumer` apelează metoda `consume` de 10 ori pentru a consuma valorile generate de `Producer`.

3. **Clasa `WaitNotifyExample`**:
    - Inițializează resursa partajată și pornește threadurile `Producer` și `Consumer`.

Acest exemplu arată cum `wait()`, `notify()`, și `notifyAll()` sunt folosite pentru a sincroniza și coordona comunicarea între threaduri într-un mod eficient și sigur în Java.
