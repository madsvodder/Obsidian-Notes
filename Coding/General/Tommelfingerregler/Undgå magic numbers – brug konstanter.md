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