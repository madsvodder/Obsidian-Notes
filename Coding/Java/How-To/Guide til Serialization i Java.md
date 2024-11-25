Serialization i Java er processen med at konvertere et objekt til en byte-strøm, så det kan gemmes på disk eller sendes over et netværk. Den modsatte proces, deserialization, gendanner objektet fra byte-strømmen. Dette er nyttigt for at gemme objekter, dele dem mellem forskellige applikationer eller transportere dem via netværk.

## 1. Krav til Serialization
- Klassen skal implementere `java.io.Serializable` interfacet.
- Alle objekter i klassen (herunder felter) skal også være serializable. Hvis et felt ikke er det, skal det markeres som `transient`.
- Husk også at give klassen et `serialVersionUID`
## 2. Simpelt eksempel af serialization
**Serialization eksempel:** En klasse som skal serialiseres
```java
import java.io.Serializable;

public class Person implements Serializable {
    private static final long serialVersionUID = 1L; // God praksis til versionskontrol
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + '}';
    }
}

```

**Serialization eksempel:*** Gem et objekt til en fil
```java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;

public class SerializeExample {
    public static void main(String[] args) {
        Person person = new Person("Alice", 30);

        try (FileOutputStream fileOut = new FileOutputStream("person.ser");
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
            out.writeObject(person);
            System.out.println("Object serialized and saved in person.ser");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

**Deserialization eksempel:** Læs et objekt fra en fil
```java
import java.io.FileInputStream;
import java.io.ObjectInputStream;

public class DeserializeExample {
    public static void main(String[] args) {
        try (FileInputStream fileIn = new FileInputStream("person.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            Person person = (Person) in.readObject();
            System.out.println("Deserialized Object: " + person);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## 3. Håndtering af `transient`
- Felter markeret som `transient` bliver ikke inkluderet i serialization. Dette er nyttigt til data, der enten er midlertidige eller følsomme, som passwords eller sessionsdata.
- Under serialization springer Java `transient` felter over, og når objektet deserialiseres, vil disse felter få deres standardværdier:
    - `null` for objektreferencer,
    - `0` for primitive numeriske typer,
    - `false` for `boolean`.

**Eksempel med transient-felt**
```java
import java.io.Serializable;

public class SecurePerson implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private transient String password; // Bliver ikke serialiseret

    public SecurePerson(String name, String password) {
        this.name = name;
        this.password = password;
    }

    @Override
    public String toString() {
        return "SecurePerson{name='" + name + "', password='" + password + "'}";
    }
}
```
Ved serialization vil feltet `password` ikke blive gemt og vil være `null` efter deserialization.

## 4. Kontrollér `serialVersionUID`
- `serialVersionUID` bruges til at sikre, at en serialiseret klasse matcher dens deserializerede version. Hvis en klasse ændres (f.eks. ved tilføjelse af et nyt felt), kan dette føre til `InvalidClassException`, medmindre det samme `serialVersionUID` bruges.

```java
private static final long serialVersionUID = 1L;
```

## 5. Håndtering af fejl 
- Sørg for at håndtere exceptions som `IOException` og `ClassNotFoundException`.
- Check filens placering og tilladelser.
#### **Problemer med `transient` og UI-relaterede variabler:**
- I JavaFX og andre UI-frameworks bruges ofte "simple" variabler som `SimpleStringProperty` eller `ObservableList`, der ikke er direkte serializable. Hvis disse variabler erklæres som `transient`, kan de ikke gemmes under serialization, og deres værdier vil være utilgængelige efter deserialization.
- For at omgå dette problem kan du:
    1. **Konvertere dem til standard variabler før serialization:** Gem værdien som en almindelig streng eller liste.
    2. **Gendanne dem som "simple" variabler efter deserialization:** Rekonstruer objekterne manuelt eller gennem en metode.

Dette sikrer, at UI-relaterede data håndteres korrekt uden at miste deres funktionalitet i applikationen.
## 7. Yderligere tips
- Krypter objekter før lagring, hvis de indeholder følsomme data.
- Overvej at bruge biblioteker som Gson eller Jackson til mere fleksibel serialization til JSON-format.