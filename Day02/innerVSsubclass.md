În Java, clasele interne și subclasele sunt concepte distincte care servesc scopuri diferite în programare. Iată principalele diferențe între o clasă internă și o subclasă:

### Clasă Internă (Inner Class)
1. **Definiție**: O clasă internă este o clasă definită în interiorul unei alte clase.
2. **Acces**: Clasele interne pot accesa membrii (inclusiv membrii privați) ai clasei exterioare.
3. **Instanțiere**: Pentru a crea o instanță a unei clase interne, trebuie mai întâi să aveți o instanță a clasei exterioare (cu excepția claselor interne statice).
4. **Tipuri**:
   - **Non-static inner class**: Depinde de o instanță a clasei exterioare.
   - **Static inner class**: Nu depinde de o instanță a clasei exterioare.
   - **Anonymous inner class**: O clasă internă fără nume, utilizată pentru a suprascrie metode sau a implementa interfețe la fața locului.
   - **Local inner class**: O clasă definită într-un bloc de cod (de exemplu, într-o metodă).

Exemplu:
```java
class OuterClass {
    private int outerField;

    class InnerClass {
        void display() {
            System.out.println("Outer field: " + outerField);
        }
    }
}
```

### Subclasă (Subclass)
1. **Definiție**: O subclasă este o clasă care extinde (moștenește) o altă clasă (clasa părinte sau superclasa).
2. **Acces**: Subclasele moștenesc membrii publici și protejați ai superclasei, dar nu au acces direct la membrii privați ai acesteia.
3. **Instanțiere**: Puteți crea o instanță a unei subclase fără a avea nevoie de o instanță a superclasei.
4. **Tipuri**: Subclasele sunt clasice în moștenirea clasei de bază și pot suprascrie metodele superclasei pentru a oferi implementări specifice.

Exemplu:
```java
class SuperClass {
    protected void display() {
        System.out.println("Display from SuperClass");
    }
}

class SubClass extends SuperClass {
    @Override
    protected void display() {
        System.out.println("Display from SubClass");
    }
}
```

### Rezumat
- **Clasă Internă**: Este definită în interiorul unei alte clase și are acces direct la membrii acesteia. Este utilizată pentru a grupa clase care sunt utilizate împreună și pentru a ascunde clasele de implementare.
- **Subclasă**: Extinde o altă clasă și moștenește membrii acesteia. Este utilizată pentru a modela o relație "este un" și pentru a reutiliza codul prin moștenire.

Aceste două concepte sunt utile în diferite scenarii și alegerea între ele depinde de structura și cerințele aplicației tale Java.
