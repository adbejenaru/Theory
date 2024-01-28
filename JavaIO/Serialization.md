Serializarea și deserializarea în Java sunt concepte utilizate pentru a scrie starea unui obiect într-un flux de date și, respectiv, pentru a reconstitui acel obiect din fluxul de date. Aceste procese sunt folositoare în diverse scenarii, cum ar fi salvarea stării obiectului pe disc, transmiterea obiectului peste rețea sau stocarea în baze de date.

### Serializarea

Serializarea este procesul prin care starea unui obiect este transformată într-o secvență de biți, astfel încât această secvență poate fi salvată într-un fișier, transmisă printr-o rețea sau stocată pentru utilizare ulterioară. În Java, acest lucru se realizează prin implementarea interfeței `java.io.Serializable`.

Un exemplu simplu de serializare în Java:

```java
import java.io.*;

public class ExempluSerializare implements Serializable {
    private int id;
    private String nume;

    public ExempluSerializare(int id, String nume) {
        this.id = id;
        this.nume = nume;
    }

    public static void main(String[] args) {
        ExempluSerializare obiect = new ExempluSerializare(1, "Test");

        try {
            FileOutputStream fileOut = new FileOutputStream("obiect.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(obiect);
            out.close();
            fileOut.close();
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

### Deserializarea

Deserializarea este procesul invers, unde secvența de biți este transformată înapoi într-un obiect Java. Acest lucru este util pentru a reconstrui obiectul într-un alt moment sau într-un alt context (de exemplu, pe un alt sistem sau într-un alt proces).

Un exemplu simplu de deserializare în Java:

```java
import java.io.*;

public class ExempluDeserializare {

    public static void main(String[] args) {
        ExempluSerializare obiect = null;

        try {
            FileInputStream fileIn = new FileInputStream("obiect.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            obiect = (ExempluSerializare) in.readObject();
            in.close();
            fileIn.close();
        } catch (IOException i) {
            i.printStackTrace();
            return;
        } catch (ClassNotFoundException c) {
            System.out.println("Clasa ExempluSerializare nu a fost găsită");
            c.printStackTrace();
            return;
        }

        System.out.println("Deserializat: " + obiect);
    }
}
```

### Lucruri de reținut

- Nu toate obiectele pot fi serializate. Doar obiectele a căror clase implementează interfața `Serializable` pot fi serializate.
- Serializarea salvează starea curentă a obiectului, nu codul obiectului în sine.
- Atunci când un obiect este deserializat, nu se apelează constructorul său.
- Trebuie să fii conștient de problemele de securitate asociate cu serializarea și deserializarea, în special atunci când sunt utilizate pentru comunicarea prin rețea.
