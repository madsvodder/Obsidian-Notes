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

## 4. Dark-Light Mode funktion i JavaFX CSS

En af de nyeste funktioner i JavaFX's CSS-opdatering er understøttelsen af **dark** og **light** mode, som giver udviklere mulighed for at tilpasse applikationens udseende baseret på brugerens præferencer for lys eller mørkt tema. Denne funktion gør det muligt at skabe dynamiske brugergrænseflader, der tilpasser sig forskellige miljøer uden behov for at ændre selve koden.

### Eksempel på Dark/Light Mode CSS:
```css title:dark-light.css
/* Standard lys tema */
.root {
    -fx-background-color: #ffffff;
    -fx-text-fill: #000000;
}

/* Mørk tema */
:root {
    -fx-base: #121212;
    -fx-background-color: #212121;
    -fx-text-fill: #ffffff;
}

.button {
    -fx-background-color: linear-gradient(to bottom, #4CAF50, #388E3C);
    -fx-text-fill: white;
    -fx-font-size: 16px;
    -fx-padding: 10px 15px;
    -fx-border-radius: 5px;
    -fx-background-radius: 5px;
    -fx-border-color: #2E7D32;
}

/* Tilføj et CSS media query for at skifte mellem temaer */
@media (prefers-color-scheme: dark) {
    .root {
        -fx-background-color: #212121;
        -fx-text-fill: #ffffff;
    }
}

@media (prefers-color-scheme: light) {
    .root {
        -fx-background-color: #ffffff;
        -fx-text-fill: #000000;
    }
}
```

Med denne opdatering kan applikationen automatisk skifte mellem et lyst og et mørkt tema afhængigt af systemets præferencer, hvilket giver en mere tilpasset og behagelig brugeroplevelse.

**Fordele ved Dark/Light Mode:**

- **Automatisk tilpasning:** Brugeren behøver ikke selv at vælge et tema; det tilpasses baseret på systemindstillinger.
- **Bedre brugeroplevelse:** Giver et mere komfortabelt og moderne design, især om natten (mørkt tema).
- **Konsistens med systemindstillinger:** Applikationen følger brugerens præferencer for mørkt eller lyst tema uden ekstra input.

### JavaFX og `prefers-color-scheme`

Selvom JavaFX ikke understøtter `prefers-color-scheme` media query direkte som i standard CSS, kan vi stadig anvende systemets farveskema i JavaFX ved hjælp af Java-kode.

JavaFX tilbyder ikke automatisk understøttelse af den nye CSS funktionalitet, men vi kan selv håndtere temaer baseret på systemindstillinger. For at gøre dette, kan vi bruge Java til at detektere brugerens præference og anvende passende stilarter dynamisk.

### Eksempel på JavaFX med Detektion af Systemtema

JavaFX har ikke indbygget funktionalitet til at detektere mørk/løst tema automatisk som CSS, men vi kan bruge en simpel metode til at vælge temaet baseret på platformens systemindstillinger.

```java title:DarkModeExample.java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.StackPane;
import javafx.scene.text.Text;
import javafx.stage.Stage;

public class DarkModeExample extends Application {
    @Override
    public void start(Stage primaryStage) {
        StackPane root = new StackPane();
        Text text = new Text("Hello, JavaFX!");
        root.getChildren().add(text);

        // Detekter systemets farveskema og anvend korrekt stylesheet
        String theme = System.getProperty("os.name").toLowerCase().contains("mac") ? "light" : "dark"; // Eksempel på platformbaseret logik

        Scene scene = new Scene(root, 300, 200);

        if (theme.equals("dark")) {
            scene.getStylesheets().add(getClass().getResource("dark-theme.css").toExternalForm());
        } else {
            scene.getStylesheets().add(getClass().getResource("light-theme.css").toExternalForm());
        }

        primaryStage.setTitle("Dark Mode Example");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

I dette eksempel anvender applikationen et mørkt eller lyst tema baseret på systemets platform, som for eksempel macOS i dette tilfælde. Du kan udvide logikken til at tage højde for andre systemer og deres specifikke farvepræferencer.

### Manuelt Skift af Tema

Du kan også give brugeren kontrol over skiftet mellem lys og mørk mode ved at tilføje en toggle-knap, som ændrer temaet dynamisk.
```java title:ToggleButton
ToggleButton darkModeToggle = new ToggleButton("Dark Mode");
darkModeToggle.setOnAction(event -> {
    if (darkModeToggle.isSelected()) {
        scene.getStylesheets().clear();
        scene.getStylesheets().add(getClass().getResource("dark-theme.css").toExternalForm());
    } else {
        scene.getStylesheets().clear();
        scene.getStylesheets().add(getClass().getResource("light-theme.css").toExternalForm());
    }
});

```

Med denne tilgang kan brugeren selv vælge, om de vil bruge mørk eller lys mode i applikationen.
## Konklusion
CSS understøttelsen af dark/light mode i JavaFX gør det muligt at skabe en dynamisk og brugervenlig oplevelse, hvor temaet tilpasses automatisk til systemets indstillinger. Ved at bruge `prefers-color-scheme` i CSS eller ved at detektere systemets tema via Java, kan du hurtigt implementere et moderne design, der følger brugerens præferencer. Kombinationen af automatisk temaindstilling og brugerdefinerede toggles giver maksimal fleksibilitet og kontrol.
## 5. Fordele ved CSS i JavaFX
- **Adskillelse af design og logik:** CSS holder layout og styling adskilt fra Java-koden.
- **Genbrug:** En CSS-fil kan bruges på tværs af flere scener eller projekter for konsistens.
- **Fleksibilitet:** Designændringer kræver kun opdatering af CSS-filen, ikke Java-koden.
- **Avanceret styling:** CSS gør det muligt at lave komplekse designs, som ville være besværlige at kode direkte i JavaFX.