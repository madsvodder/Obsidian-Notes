JavaFX understøtter brugen af CSS (Cascading Style Sheets) til at tilpasse udseendet og stilen af brugergrænsefladen. Dette giver dig mulighed for at adskille applikationens design fra dens logik, hvilket gør det nemmere at vedligeholde og ændre udseendet uden at skulle ændre Java-koden. 
Ved at bruge CSS kan du genbruge temaet i forskellige projekter. Dette gør det til et kraftfuldt værktøj for JavaFX-udviklere.

## 1. Tilføj en CSS-fil til din scene:

```java title:styling
scene.getStylesheets().add("style.css");
```

## 2. Eksempel på en CSS-fil (`style.css`):
```css title:style.css
/* Generelle styling-regler */
.root {
    -fx-font-family: "Arial";
    -fx-background-color: #f0f0f0;
}

/* Styling af labels */
.label {
    -fx-font-size: 14px;
    -fx-text-fill: #333333;
    -fx-padding: 5px;
}

/* Styling af knapper */
.button {
    -fx-background-color: linear-gradient(to bottom, #4CAF50, #388E3C);
    -fx-text-fill: white;
    -fx-font-size: 16px;
    -fx-padding: 10px 15px;
    -fx-border-radius: 5px;
    -fx-background-radius: 5px;
    -fx-border-color: #2E7D32;
}

/* ID-selektor */ 
#mainButton { -fx-border-color: black; -fx-border-width: 2px; -fx-border-radius: 5px; }

.button:hover {
    -fx-background-color: linear-gradient(to bottom, #66BB6A, #43A047);
    -fx-cursor: hand;
}

.button:pressed {
    -fx-background-color: linear-gradient(to bottom, #388E3C, #2E7D32);
}

/* Styling af tekstfelter */
.text-field {
    -fx-border-color: #9E9E9E;
    -fx-border-width: 1px;
    -fx-border-radius: 3px;
    -fx-padding: 5px;
    -fx-background-color: #ffffff;
}

.text-field:focused {
    -fx-border-color: #4CAF50;
    -fx-background-color: #f9fff9;
}

/* Styling af layouts */
.vbox {
    -fx-spacing: 10px;
    -fx-padding: 15px;
    -fx-background-color: #ffffff;
    -fx-border-color: #BDBDBD;
    -fx-border-width: 1px;
    -fx-border-radius: 5px;
}

/* Styling af overskrifter */
.h1 {
    -fx-font-size: 24px;
    -fx-text-fill: #212121;
    -fx-font-weight: bold;
}

.h2 {
    -fx-font-size: 20px;
    -fx-text-fill: #424242;
}

/* Styling af fokus */
.focused {
    -fx-effect: dropshadow(three-pass-box, rgba(0, 128, 0, 0.5), 5, 0.3, 0, 0);
}

```
#### **Forklaring:**
- Knapper (`.button`): Knapper er designet med en gradient og forskellige effekter til hover og tryk.
- Tekstfelter (`.text-field`): Har dynamisk styling, der ændrer sig ved fokus.
- Layouts (`.vbox`): En simpel boks med kant og baggrundsfarve.
- Labels og overskrifter (`.label`, `.h1`, `.h2`): Forskellig størrelse og farve.
- Den specifikke knap med `id="mainButton"` vil også have en sort kant.
## 3. Anvend en CSS-fil som tema
For at tilpasse udseendet af din JavaFX-applikation kan du tilføje en CSS-fil som et tema. Dette gøres ved at linke CSS-filen til scenen i din `main`-klasse. Når filen er tilknyttet, vil den style alle relevante komponenter i dit JavaFX-projekt.

```java
scene.getStylesheets().add(getClass().getResource("style.css").toExternalForm());
```

Dette eksempel tilføjer en CSS-fil kaldet `style.css`, som skal placeres i projektets ressourcemappe (samme mappe som din `main`-klasse eller `resources` afhængigt af din opsætning).

**Resultat:**  
CSS-filen vil automatisk ændre udseendet på alle UI-elementer, der matcher de definerede CSS-selektorer. Dette gør det nemt at holde din applikations design konsekvent og let at opdatere.

## 4. Fordele ved CSS i JavaFX
- **Adskillelse af design og logik:** CSS holder layout og styling adskilt fra Java-koden.
- **Genbrug:** En CSS-fil kan bruges på tværs af flere scener eller projekter for konsistens.
- **Fleksibilitet:** Designændringer kræver kun opdatering af CSS-filen, ikke Java-koden.
- **Avanceret styling:** CSS gør det muligt at lave komplekse designs, som ville være besværlige at kode direkte i JavaFX.