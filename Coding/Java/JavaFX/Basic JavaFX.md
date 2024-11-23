## 1. Grundstruktur i JavaFX
JavaFX er baseret på en arkitektur, hvor UI-elementer (nodes) er arrangeret i en hierarkisk struktur. Grundlæggende består en JavaFX-applikation af følgende dele:

1. **`Stage`**:
    - Vinduesrammen, som applikationen vises i.
    - Oprettes som standard i `Application.start()`.
2. **`Scene`**:
    - Repræsenterer indholdet i vinduet.
    - Kan skiftes dynamisk på et `Stage`.
3. **`Node`**:
    - Hver enkelt visuel komponent (f.eks. knapper, tekstfelter, layouts).
## 2. Layouts i JavaFX
JavaFX tilbyder forskellige layout-containere til at arrangere dine UI-elementer:
- **`VBox`**: Vertikal liste af elementer.
- **`HBox`**: Horisontal liste af elementer.
- **`GridPane`**: Et gitter med rækker og kolonner.
- **`BorderPane`**: Layout med områder som `top`, `left`, `center`, `right`, og `bottom`.
- **`StackPane`**: Lægger elementer ovenpå hinanden.
## 3. Scene Builder og FXML
Scene Builder bruges til visuelt at designe brugergrænseflader. Det genererer en `.fxml`-fil, der kan bruges i din JavaFX-applikation.

1. **Integrering af `.fxml` i Java-kode**:
    - Importer filen ved hjælp af `FXMLLoader`.
    - Bind UI-elementer til controlleren med `@FXML`.
```java
import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class MainApp extends Application {
    @Override
    public void start(Stage primaryStage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("layout.fxml"));
        Scene scene = new Scene(root);
        primaryStage.setScene(scene);
        primaryStage.setTitle("FXML Eksempel");
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}

```

2. **Controller-klasse og FXML:**
	- Forbindes med `fx:controller`-attributten i `.fxml`.
	- Brug `@FXML` til at referere til UI-elementer.
	
```XML title:FXML-fil
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.Button?>
<?import javafx.scene.layout.VBox?>

<VBox xmlns:fx="http://javafx.com/fxml/1" fx:controller="com.example.Controller">
    <Button text="Klik mig!" onAction="#handleButtonClick"/>
</VBox>

```

```java title:Controller
import javafx.fxml.FXML;
import javafx.scene.control.Button;

public class Controller {
    @FXML
    private Button myButton;

    @FXML
    private void handleButtonClick() {
        myButton.setText("Klikket!");
    }
}
```

## 4. Events og Bindinger
JavaFX understøtter en række mekanismer til at reagere på brugerinteraktion.

1. **Event Handlers**:
    - Brug `setOnAction` til at tilføje en event-handler direkte i kode.
```java title:ButtonActionEvent
button.setOnAction(event -> { System.out.println("Knap klikket!"); });
```
2. **Bindinger**:
- Dynamisk opdatering af UI baseret på dataændringer.
- Brug af `Property`-klasser som `StringProperty`.
```java title:BindingExample
import javafx.beans.property.SimpleStringProperty;
import javafx.beans.property.StringProperty;

public class BindingExample {
    private StringProperty text = new SimpleStringProperty("Start tekst");

    public StringProperty textProperty() {
        return text;
    }

    public String getText() {
        return text.get();
    }

    public void setText(String value) {
        text.set(value);
    }
}

```