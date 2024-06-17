Compoziția este un principiu fundamental în programarea orientată pe obiecte (OOP) care presupune construirea unor obiecte complexe prin combinarea altor obiecte mai simple. Aceasta este o relație "are-un" (has-a), spre deosebire de moștenire, care este o relație "este-un" (is-a).

### Diferența dintre Compoziție și Moștenire

1. **Moștenire**:
   - Este utilizată pentru a defini o relație ierarhică între clase.
   - O clasă derivată moștenește atributele și metodele clasei de bază.
   - Este o relație puternică, deoarece clasa derivată depinde direct de clasa de bază.
   - Ex: `Un cerc este o formă geometrică`.

2. **Compoziție**:
   - Este utilizată pentru a construi clase complexe prin includerea instanțelor altor clase.
   - O clasă conține o referință la alte obiecte ca membri.
   - Este o relație flexibilă, deoarece clasele componente sunt independente.
   - Ex: `O mașină are un motor`.

### Avantajele Compoziției

- **Reutilizare**: Permite reutilizarea componentelor fără a fi nevoie de moștenire.
- **Flexibilitate**: Obiectele compuse pot fi schimbate în mod dinamic la runtime.
- **Encapsulare**: Componentele interne sunt ascunse, promovând o separare clară a preocupărilor.
- **Reductibilitate**: Reduce legăturile strânse între clase, ceea ce face codul mai ușor de întreținut și testat.

### Exemplu de Compoziție în Java

Să presupunem că vrem să modelăm o mașină care are un motor și o transmisie. Vom crea clase separate pentru fiecare componentă și le vom compune în clasa `Car`.

```java
// Definirea clasei Engine
class Engine {
    public void start() {
        System.out.println("Engine started");
    }

    public void stop() {
        System.out.println("Engine stopped");
    }
}

// Definirea clasei Transmission
class Transmission {
    public void shiftGear() {
        System.out.println("Gear shifted");
    }
}

// Definirea clasei Car care utilizează compoziția
class Car {
    private Engine engine;
    private Transmission transmission;

    public Car() {
        engine = new Engine();
        transmission = new Transmission();
    }

    public void startCar() {
        engine.start();
        transmission.shiftGear();
        System.out.println("Car started");
    }

    public void stopCar() {
        engine.stop();
        System.out.println("Car stopped");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.startCar(); // Output: Engine started, Gear shifted, Car started
        car.stopCar();  // Output: Engine stopped, Car stopped
    }
}
```

### Explicația codului:

1. **Clasa `Engine`**:
   - Reprezintă un motor cu metode pentru a porni și opri motorul.
2. **Clasa `Transmission`**:
   - Reprezintă o transmisie cu o metodă pentru schimbarea treptelor de viteză.
3. **Clasa `Car`**:
   - Utilizează compoziția pentru a include un motor (`Engine`) și o transmisie (`Transmission`).
   - Are metode pentru a porni și opri mașina, care la rândul lor apelează metodele componentei interne.

Prin utilizarea compoziției, clasa `Car` poate gestiona componentele sale interne (`Engine` și `Transmission`) fără a moșteni direct comportamentul lor, păstrând astfel o separare clară a preocupărilor și făcând codul mai flexibil și ușor de întreținut.
