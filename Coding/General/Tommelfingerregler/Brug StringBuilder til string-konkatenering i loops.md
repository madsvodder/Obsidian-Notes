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