
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
