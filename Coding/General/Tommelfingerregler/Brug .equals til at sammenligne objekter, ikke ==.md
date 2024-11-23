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