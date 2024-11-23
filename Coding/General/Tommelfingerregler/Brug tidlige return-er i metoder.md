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