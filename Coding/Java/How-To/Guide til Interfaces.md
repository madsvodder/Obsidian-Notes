Et **interface** er en kontrakt, der definerer, hvad en klasse kan gøre, uden at specificere hvordan. Det bruges til at skabe en fælles adfærd på tværs af klasser og muliggør flerarv. Interfaces kan indeholde abstrakte metoder, standardmetoder og statiske metoder. Fra Java 9 kan de også have private metoder. Klasser, der implementerer et interface, skal opfylde alle dets krav.

En konvention er at starte navnet på et interface med `I`, fx `IDrawable`, for at tydeliggøre, at det er et interface.

## 1. Hvad er et interface?
- Et **interface** er en samling af metode-signaturer, der beskriver, hvad en klasse kan gøre, uden at definere hvordan det gøres.
- Et interface bruges til at specificere en **kontrakt**, som klasser skal opfylde.

## 2. Kendetegn ved interfaces
- Deklareres med nøgleordet `interface`.
- Kan kun indeholde:
    - **Abstrakte metoder** (før Java 8).
    - **Standardmetoder** og **statisk metoder** (fra Java 8 og frem).
    - **Konstanter** (implicit `public static final`).
- En klasse, der implementerer et interface, **skal** give en implementering af alle dets metoder, medmindre klassen er abstrakt.

## 3. Syntaks for et interface
```java
interface InterfaceName {
    // Konstanter
    int CONSTANT = 100; // Implicit public static final

    // Abstrakt metode
    void methodName();

    // Standardmetode (fra Java 8)
    default void defaultMethod() {
        System.out.println("Dette er en standardmetode.");
    }

    // Statisk metode (fra Java 8)
    static void staticMethod() {
        System.out.println("Dette er en statisk metode.");
    }
}
```

## 4. Eksempel på interface
```java title:Drawable.java
interface Drawable {
    void draw(); // Abstrakt metode
}
```

En klasse, der implementerer et interface:

```java title:Circle.java
class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Tegner en cirkel");
    }
}
```

## 5. Vigtige regler for interfaces
- Alle metoder i et interface er implicit:
    - `public`.
    - `abstract` (før Java 8, medmindre de er `default` eller `static`).
- En klasse kan implementere flere interfaces.
- Interfaces kan ikke have konstruktører.
- Fra Java 9 kan interfaces også indeholde **private metoder** til brug internt i `default`- eller `static`-metoder.

## 6. Interface vs. Abstrakt Klasse

| **Egenskab**                        | **Interface**                                                           | **Abstrakt Klasse**                       |
| ----------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------- |
| **Kan have felter**                 | Nej (undtagen konstanter)                                               | Ja                                        |
| **Kan have implementerede metoder** | Ja (kun med `default` eller `static` metoder efter Java 8)              | Ja                                        |
| **Arv**                             | En klasse kan implementere flere interfaces.                            | En klasse kan kun arve én abstrakt klasse |
| **Konstruktører**                   | Nej                                                                     | Ja                                        |

## 7. Hvornår skal du bruge interfaces?

- Når du ønsker at definere **hvad en klasse kan gøre** uden at specificere, hvordan det skal gøres.
- Når du vil opnå **flerarv**, da en klasse kan implementere flere interfaces.
- Når du vil skabe en kontrakt, der kan deles på tværs af uafhængige klasser.

## 8. Avancerede funktioner i interfaces
- **Standardmetoder**: Gør det muligt at tilføje nye funktioner til eksisterende interfaces uden at bryde allerede implementerede klasser.
- **Statisk metoder**: Hjælper med at implementere utility-funktioner direkte i interfacet.
- **Private metoder** (fra Java 9): Bruges til at undgå kode-duplikation i `default`-metoder.

## 9. Eksempel på flere interfaces
```java title:iFlyable.java
interface Flyable {
    void fly();
}
```

```java title:iSwimmable.java
interface Swimmable {
    void swim();
}
```

```java title:Duck.java
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Anden flyver.");
    }

    @Override
    public void swim() {
        System.out.println("Anden svømmer.");
    }
}
```
## 10. Tips til brug af interfaces
- Brug interfaces til at skabe fleksible og genanvendelige designs.
- Hvis du har brug for at dele både implementering og adfærd, kan en **abstrakt klasse** være mere passende.
- Kombinér interfaces med standardmetoder for at give en balance mellem fleksibilitet og genbrug.
