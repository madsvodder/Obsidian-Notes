## 1. Adskil UI og logik
Det er vigtigt at holde UI-komponenter og forretningslogik adskilt. Eksempel: En _Controller_-klasse styrer visningen af playlisten i UI'et, men bør ikke have ansvar for at tilføje nye sange til playlisten. I stedet bør den sende en besked til _Playlist_-klassen, som håndterer oprettelsen og vedligeholdelsen af playlisten. _Controller_-klassen skal kun opdatere UI'et med de nødvendige ændringer, uden at inddrage logikken bag playlistens indhold.

## 2. Brug .equals til at sammenligne objekter, ikke ==
Brug `equals`-metoden til at sammenligne indholdet af objekter, ikke `==`, da `==` sammenligner referencer i stedet for værdier. `equals` sammenligner objektets indhold, mens `==` kun sammenligner, om de to referencer peger på det samme objekt.

**Eksempel:**
```java
// Dårlig praksis
String a = "hello";
String b = new String("hello");
if (a == b) {  // Dette vil returnere false, fordi de ikke er samme objekt
    System.out.println("Strings are equal");
}

// Bedre praksis
String a = "hello";
String b = new String("hello");
if (a.equals(b)) {  // Dette vil returnere true, fordi de har samme værdi
    System.out.println("Strings are equal");
}

```

## 3. Brug StringBuilder i loops
**Tommelfingerregel:** Brug `StringBuilder` når du skal sammenkæde mange strenge i en loop eller gentagne operationer. Det er mere effektivt end at bruge `+` til strenge i loops, fordi det undgår at oprette nye objekter hver gang. 
`StringBuilder` ændrer eksisterende objekt i stedet for at skabe nye objekter hver gang, hvilket gør det mere effektivt i tilfælde med mange string-sammenkædninger.

**Eksempel:**
```java
// Dårlig praksis
String result = "";
for (int i = 0; i < 1000; i++) {
    result += "Item " + i + "\n";
}

// Bedre praksis
StringBuilder result = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    result.append("Item ").append(i).append("\n");
}

```
## 4. Brug tidlige return-er i metoder
Brug tidlige `return`-er for at gøre koden lettere at læse og undgå unødvendige indrykninger. Hvis en betingelse er opfyldt, kan du straks afslutte metoden. Denne tilgang gør koden fladere og nemmere at følge.

**Eksempel:**
```java
// Dårlig praksis - mange indrykninger
public void processOrder(Order order) {
    if (order != null) {
        if (order.isValid()) {
            // Behandle ordre
        }
    }
}

// Bedre praksis - tidlige return
public void processOrder(Order order) {
    if (order == null) {
        return;
    }
    if (!order.isValid()) {
        return;
    }
    // Behandle ordre
}

```

## 5. Skriv små metoder
Del din kode op i små metoder, der hver især har ét ansvar. Det gør koden lettere at teste, genbruge og vedligeholde.

**Eksempel:**
```java
// Dårlig praksis - stor metode
public void processUserData(String name, int age) {
    // Validering af navn
    if (name == null || name.isEmpty()) {
        System.out.println("Ugyldigt navn");
    }
    // Validering af alder
    if (age < 0) {
        System.out.println("Ugyldig alder");
    }
    // Oprettelse af bruger
    createUser(name, age);
}

// Bedre praksis - små metoder
public void validateName(String name) {
    if (name == null || name.isEmpty()) {
        System.out.println("Ugyldigt navn");
    }
}

public void validateAge(int age) {
    if (age < 0) {
        System.out.println("Ugyldig alder");
    }
}

public void processUserData(String name, int age) {
    validateName(name);
    validateAge(age);
    createUser(name, age);
}

```
## 6. Stop loopet tidligt, når du har fundet det ønskede element
Hvis du kun er interesseret i at finde én værdi i et array, kan du bruge `break` for at afslutte loopet, så snart du har fundet det ønskede element. Dette optimerer din kode ved at forhindre unødvendige iterationer.

**Eksempel:**
```java
for (Song s : Playlist) {
    if (s.equals(søgtSong)) {
        // Sangen blev fundet, gør noget med s
        System.out.println("Sangen blev fundet!");
        break;  // Stopper løkken, når sangen er fundet
    }
}
```
## 7. Undgå magic numbers – brug konstanter
Brug konstanter i stedet for at hardkode værdier direkte i koden. Det gør din kode mere læsbar og lettere at vedligeholde. 
Dette gør det lettere at ændre værdien et enkelt sted i koden (hvis du for eksempel senere vil ændre minimumsalderen) og gør koden lettere at forstå.

**Eksempel:**
```java
// Dårlig praksis - magic number
if (age > 18) {
    // gør noget
}

// Bedre praksis - brug konstant
final int MINIMUM_AGE = 18;
if (age > MINIMUM_AGE) {
    // gør noget
}

```

# 8. Lav kobling og Høj Cohesion
**Kobling (Coupling)** refererer til, hvor tæt forbundet forskellige klasser eller moduler er. Lav kobling er ønskværdig, da det gør systemet mere fleksibelt og nemmere at vedligeholde. **Cohesion** handler om, hvor veldefineret og fokuseret en klasses ansvar er. Høj cohesion betyder, at en klasse kun har ét veldefineret formål, hvilket gør koden mere læsbar og genbrugelig.

**Eksempel:**
```java title:Order.java
class Order {
    private List<Item> items;

    public void addItem(Item item) {
        items.add(item);
    }

    public double calculateTotal() {
        double total = 0;
        for (Item item : items) {
            total += item.getPrice();
        }
        return total;
    }
}
```

```java title:item.java
class Item {
    private String name;
    private double price;

    public Item(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public double getPrice() {
        return price;
    }
}
```

Her har **`Order` høj cohesion**, fordi dens metoder alle fokuserer på ordrelogik. Samtidig er **koblingen lav** mellem `Order` og `Item`, da de kun kommunikerer gennem en enkel metode (`getPrice`), uden at `Order` kender til `Item`'s interne detaljer.