En abstrakt klasse er en skabelon, der ikke kan instantieres direkte, og som bruges til at definere fælles adfærd for relaterede klasser. Den kan indeholde både abstrakte metoder (uden implementering) og konkrete metoder (med implementering). Subklasser skal implementere de abstrakte metoder, medmindre de selv er abstrakte. Abstrakte klasser bruges til at skabe en fælles base for flere klasser og til at sikre, at bestemte metoder bliver implementeret.
## 1. Hvad er en abstrakt klasse?
- En **abstrakt klasse** er en klasse, der ikke kan instantieres direkte. Den bruges som en skabelon for andre klasser.
- Den kan indeholde både:
    - **Abstrakte metoder**: Metoder uden implementering (kun metode-signatur).
    - **Ikke-abstrakte metoder**: Metoder med implementering.
## 2. Kendetegn ved abstrakte klasser
- Deklareres med nøgleordet `abstract`.
- Kan ikke oprettes med `new`.
- En abstrakt klasse kan have felter (variabler), konstruktører og metoder.
- Bruges til at specificere en **fælles adfærd** for en gruppe af klasser.

## 3. Abstrakte metoder
- Deklareres uden krop (dvs. ingen `{}`) og afsluttes med et semikolon.
- Eksempel:
```java
abstract class Shape {
    abstract void draw(); // Abstrakt metode
}
```
Subklasser **skal** implementere alle abstrakte metoder fra den abstrakte klasse, medmindre subklassen selv er abstrakt.

## 4. Syntaks for abstrakte klasser
```java
abstract class ClassName {
    // Felter
    int field;

    // Abstrakt metode
    abstract void methodName();

    // Ikke-abstrakt metode
    void anotherMethod() {
        System.out.println("Denne metode har en implementering.");
    }
}
```
## 5. Eksempel
```java title:Shape.java
// Abstrakt klasse
abstract class Shape {
    String color;

    // Abstrakt metode
    abstract void draw();

    // Ikke-abstrakt metode
    void setColor(String color) {
        this.color = color;
    }
}
```

Subklasse, der implementerer den abstrakte metode

```java title:Cirle.java
class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Tegner en cirkel");
    }
}
```
## 6. Vigtige regler
- En abstrakt klasse kan have både **abstrakte** og **konkrete** (implementerede) metoder.
- Hvis en klasse arver en abstrakt klasse, skal den:
    - Enten implementere alle abstrakte metoder.
    - Eller selv være deklareret som abstrakt.
- En abstrakt klasse kan indeholde felter og konstruktører, som kan bruges af dens subklasser.
- En abstrakt klasse **kan ikke være final**, fordi den er designet til at blive arvet.
## 7. Hvornår skal du bruge abstrakte klasser?

- Når du har fælles funktionalitet, som skal deles mellem flere relaterede klasser.
- Når du vil sikre, at nogle metoder bliver implementeret af subklasser.
## 8. Abstrakt Klasse vs. Interface

| **Egenskab**                        | **Abstrakt Klasse**                       | **Interface**                                                           |
| ----------------------------------- | ----------------------------------------- | ----------------------------------------------------------------------- |
| **Kan have felter**                 | Ja                                        | Nej (før Java 8, dog muligt med `static` eller `default` efter Java 8). |
| **Kan have implementerede metoder** | Ja                                        | Ja (kun med `default` eller `static` metoder efter Java 8).             |
| **Arv**                             | En klasse kan kun arve én abstrakt klasse | En klasse kan implementere flere interfaces.                            |

## 9. Tips til brug af abstrakte klasser
- Overvej **abstrakte klasser**, når du har en naturlig hierarkisk struktur.
- Brug **interfaces**, hvis du skal definere "hvad en klasse kan gøre" uden at specificere "hvordan".
