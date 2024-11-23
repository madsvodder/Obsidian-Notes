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