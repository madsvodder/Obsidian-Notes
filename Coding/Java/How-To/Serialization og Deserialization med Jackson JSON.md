## Introduktion
Jackson JSON er et kraftfuldt bibliotek til at konvertere Java-objekter til JSON og vice versa. Denne guide forklarer, hvordan man bruger Jackson til at gemme (serialize) og hente (deserialize) data ved hjælp af klasserne `DataSaver` og `Controller`.

---

## Opsætning

### ObjectMapper
Jacksons **ObjectMapper** er central for arbejdet med JSON. I `DataSaver` initialiseres en `ObjectMapper`, der kan bruges til både serialization og deserialization. For at gøre JSON mere læsevenlig, aktiveres **pretty-printing** med `SerializationFeature.INDENT_OUTPUT`.

```java
// Opret ObjectMapper og aktiver pretty-printing
public DataSaver() {
    // Initialiser ObjectMapper - Jacksons kerneklasse
    objectMapper = new ObjectMapper();
    // Gør JSON output lettere at læse med indrykninger
    objectMapper.enable(SerializationFeature.INDENT_OUTPUT);
}
```

---

## Serialization: Gem data i JSON

### Eksempel: Gem Ordre til en JSON-fil
For at gemme en liste af `Ordre`-objekter til en JSON-fil bruges `writeValue()` metoden fra `ObjectMapper`. Her er et eksempel på en metode fra `DataSaver` klassen:

```java
public void saveAllOrdre(ArrayList<Ordre> ordreList) {
    try {
        // Opret filen, hvor JSON-data skal gemmes
        File file = new File("all_orders.json");

        // Konverter ordreList til JSON og skriv det til filen
        objectMapper.writeValue(file, ordreList);

        // Log en succesmeddelelse
        logger.info("All Ordre objects saved to all_orders.json");
    } catch (IOException e) {
        // Håndter fejl ved skrivning til filen
        System.err.println("Error writing to file: " + e.getMessage());
    }
}
```

**Trin:**
1. Konverter data til en `ArrayList` (f.eks. fra en `ObservableList`).
2. Kald `saveAllOrdre()` for at gemme data til filen.

#### I `Controller` bliver denne metode kørt. Det kan f.eks være efter brugeren trykker på "Save"
```java
@FXML
public void saveAllToJSON() {
    // Opret en instans af DataSaver
    DataSaver dataSaver = new DataSaver();

    // Ordre //
    // Konverter ObservableList til ArrayList
    ArrayList<Ordre> ordreList = new ArrayList<>(ordreTabelData);

    // Gem listen af ordre til JSON-filen
    dataSaver.saveAllOrdre(ordreList);

    // Varer //
    // Konverter ObservableList til ArrayList
    ArrayList<Vare> vareList = new ArrayList<>(lagerTabelData);

    // Gem listen af varer til JSON-filen
    dataSaver.saveLager(vareList);
}
```

---

## Deserialization: Hent data fra JSON

### Eksempel: Hent Ordre fra en JSON-fil
For at hente data fra en JSON-fil bruges `readValue()` metoden fra `ObjectMapper`. Her kan du konvertere JSON direkte til en `ArrayList` af `Ordre`.

```java
public ArrayList<Ordre> loadAllOrdre() {
    try {
        // Angiv filen, der indeholder JSON-data
        File file = new File("all_orders.json");

        // Læs JSON og konverter det til en ArrayList af Ordre-objekter
        return objectMapper.readValue(file, new TypeReference<ArrayList<Ordre>>() {});
    } catch (IOException e) {
        // Håndter fejl ved læsning af filen
        System.err.println("Error reading file: " + e.getMessage());

        // Returner en tom liste, hvis der opstår en fejl
        return new ArrayList<>();
    }
}
```

**Trin:**
1. Hent data fra JSON-filen.
2. Opdater UI-komponenter som `TableView`.

#### I `Controller` klassen bliver metoden "loadAllFromJson" kørt. Det sker når brugeren gerne vil loade data fra JSON filen.
```java
@FXML
public void loadAllFromJSON() {
    // Opret en instans af DataSaver
    DataSaver dataSaver = new DataSaver();

    // Ordre //
    // Hent data fra JSON-filen
    ArrayList<Ordre> ordreList = dataSaver.loadAllOrdre();

    // Opdater tabeldata for ordre
    ordreTabelData.clear(); // Ryd eksisterende data
    ordreTabelData.addAll(ordreList); // Tilføj de hentede ordre

    // Lager Vare //
    // Hent data fra JSON-filen
    ArrayList<Vare> vareList = dataSaver.loadLager();

    // Opdater tabeldata for lager varer
    lagerTabelData.clear(); // Ryd eksisterende data
    lagerTabelData.addAll(vareList); // Tilføj de hentede varer
}
```

---

## Eksempel på JSON-fil

Hvis `Ordre`-klassen ser sådan ud:

```java
public class Ordre {
    private int id;
    private String kundeNavn;
    private String dato;

    // Getters and Setters...
}
```

Så kunne JSON-filen se sådan ud:

```json
[
  {
    "id": 1,
    "kundeNavn": "John Doe",
    "dato": "2024-11-25"
  },
  {
    "id": 2,
    "kundeNavn": "Jane Smith",
    "dato": "2024-11-24"
  }
]
```

---

## Fordele ved Jackson
1. **Simpelt API**: Enkelt at bruge til både læsning og skrivning af JSON.
2. **Fleksibilitet**: Kan håndtere komplekse datatyper som lister og kort.
3. **Udvidelse**: Understøtter avancerede funktioner som custom serializers/deserializers.

---

## Typiske fejl
- **Fil ikke fundet**: Sørg for, at filnavne og stier er korrekte.
- **TypeReference kræves**: Brug `TypeReference` for komplekse datatyper som lister.

---

## Ekstra: Debugging
Hvis du ønsker at se JSON-strukturen under debugging, kan du printe det serialiserede JSON-output til konsollen:

```java
String jsonString = objectMapper.writeValueAsString(ordreList);
System.out.println(jsonString);
```

---

### Konklusion
Jackson JSON gør serialization og deserialization effektiv og enkel. Med din opsætning kan du hurtigt gemme og hente data til og fra JSON-filer, hvilket gør det nemt at arbejde med vedvarende data i dine applikationer.
