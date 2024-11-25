Filhåndtering i Java giver programmer mulighed for at arbejde med filer på computeren, som f.eks. at læse data fra eller skrive data til filer. Java tilbyder forskellige værktøjer og klasser, som gør det muligt at åbne, læse, ændre og slette filer. De mest anvendte klasser til dette formål er `File`, `BufferedReader`, `BufferedWriter`, og `Scanner`. Java håndterer også fejl, der kan opstå under arbejdet med filer, som f.eks. hvis en fil ikke findes. For at undgå problemer med at glemme at lukke filer efter brug, kan man bruge **try-with-resources**, som automatisk lukker filerne, når de ikke længere er nødvendige.

Det er også en god idé at bruge **relative stier** i stedet for absolutte stier, da relative stier gør programmet mere fleksibelt og lettere at dele, da det ikke afhænger af den præcise placering af filerne på systemet.
## 1. Hvad er filhåndtering i Java?
Filhåndtering i Java gør det muligt at læse fra og skrive til filer ved hjælp af klasser i `java.io` og `java.nio` pakkerne. Det bruges til at håndtere data, der skal gemmes eller læses fra eksterne filer.

## 2. Grundlæggende klasser til filhåndtering
- **File**: Bruges til at repræsentere fil- og mappestier.
- **FileReader** og **BufferedReader**: Bruges til at læse tekst fra filer.
- **FileWriter** og **BufferedWriter**: Bruges til at skrive tekst til filer.
- **Scanner**: Bruges til at læse tekst fra filer med avancerede parsingsmuligheder.
- **Files** (fra `java.nio.file`): Indeholder metoder til avancerede filoperationer.

## 3. Eksempel på at læse fra en fil
```java title:ReadFile.java
import java.io.*;

public class ReadFile {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 4. Eksempel på at skrive til en fil
```java title:WriteFile.java
import java.io.*;

public class WriteFile {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt", true))) {
            writer.write("Dette er en ny linje.");
            writer.newLine();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 5. Scanner til at læse filer
```java title:ScannerExample.java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(new File("example.txt"))) {
            while (scanner.hasNextLine()) {
                System.out.println(scanner.nextLine());
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## 6. Slette eller oprette filer
```java title:FileOperations.java
import java.io.File;
import java.io.IOException;

public class FileOperations {
    public static void main(String[] args) {
        File file = new File("newfile.txt");

        // Opret fil
        try {
            if (file.createNewFile()) {
                System.out.println("Filen blev oprettet: " + file.getName());
            } else {
                System.out.println("Filen findes allerede.");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Slet fil
        if (file.delete()) {
            System.out.println("Filen blev slettet: " + file.getName());
        } else {
            System.out.println("Filen kunne ikke slettes.");
        }
    }
}
```

## 7. Vigtige metoder i File-klassen
| **Metode**           | **Beskrivelse**                                   |
| --------------------- | ------------------------------------------------- |
| `createNewFile()`     | Opretter en ny fil.                               |
| `delete()`            | Sletter en fil.                                   |
| `exists()`            | Tjekker, om en fil eller mappe findes.            |
| `isFile()`            | Tjekker, om det er en fil.                        |
| `isDirectory()`       | Tjekker, om det er en mappe.                      |
| `length()`            | Returnerer filens størrelse i bytes.              |
| `list()`              | Returnerer en liste over filer i en mappe.        |

## 8. Tips til filhåndtering
- Brug **try-with-resources** til automatisk at lukke streams og undgå ressource-lækager.
- Brug **BufferedReader/BufferedWriter** for bedre ydeevne ved læsning og skrivning.
- Tjek altid for undtagelser som `IOException` og `FileNotFoundException`.
- Overvej `java.nio.file` til mere avancerede operationer.

## 9. Advarsler
- Sørg for at have de nødvendige **tilladelser** til at læse eller skrive filer.
- Husk at håndtere undtagelser korrekt for at undgå nedbrud.
- Overvej at bruge relative stier frem for absolutte stier for bedre portabilitet.
