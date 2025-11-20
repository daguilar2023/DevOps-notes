# Lab Exercise: Building "PawMates" - A Pet Shelter App

## 1. The Mission

You have been hired to build a management application for a local animal shelter called "PawMates." They need a modern, clean desktop app to:

- View a list of pets currently up for adoption
- Add new pets to the system, including their photo, name, and breed
- View detailed information about each pet

**Technologies:** JavaFX, Scene Builder, CSS

---

## 2. Project Setup

1. **Create a new JavaFX project** in your IDE (IntelliJ IDEA or Eclipse)
2. **Create a package** named `com.pawmates`
3. **Create resource folders** (if not present):
   ```
   src/main/resources/
   ├── views/      (for FXML files)
   └── styles/     (for CSS files)
   ```
4. **Configure your `pom.xml`** with JavaFX dependencies:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>PawMates</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>PawMates</name>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-controls</artifactId>
            <version>18.0.2</version>
        </dependency>
        <dependency>
            <groupId>org.openjfx</groupId>
            <artifactId>javafx-fxml</artifactId>
            <version>18.0.2</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.13.0</version>
                <configuration>
                    <source>18</source>
                    <target>18</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.8</version>
                <executions>
                    <execution>
                        <id>default-cli</id>
                        <configuration>
                            <mainClass>com.pawmates/com.pawmates.Main</mainClass>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

---

## 3. Phase 1: The Dashboard (Scene Builder)

We will build the first page: a list of pets.

### Open Scene Builder

### Create the Layout

1. Drag an **AnchorPane** from the Library (top left) to the middle canvas
2. Resize it to approximately **600x400**

> **Why?** The AnchorPane allows us to anchor children to specific edges (top, bottom, left, right) of the layout area.

### Add the Title

1. Drag a **Label** to the top-left
2. In the Inspector Panel (right side), click **Properties**. Change text to `"PawMates Dashboard"`
3. In the Inspector Panel, click **Style Class** (under Properties) and type `title-label`

> **Why?** This tag links to the `.title-label` entry in our CSS file to apply custom fonts and colors.

### Add the Data Table

1. Drag a **TableView** onto the AnchorPane. Position it in the center
2. Resize it so it takes up most of the space, but leave room at the top and bottom
3. Double-click the TableView in the **Hierarchy** (bottom left) to see its columns
4. Rename **Column C1** to `"Name"` and **C2** to `"Breed"`
5. **Crucial Step:** In the Inspector (**Code** section):
   - Set the `fx:id` of the TableView to `petTable`
   - Set the Name column to `nameColumn`
   - Set the Breed column to `breedColumn`

> **Why?** The `fx:id` acts as a variable name. It injects this specific UI element into your Java Controller so your code can populate it with data.

### Add Buttons

1. Drag a **Button** to the bottom-right corner
2. Change text to `"Add New Pet"`
3. Set `fx:id` to `btnAdd`
4. In the **On Action** field (Code section), type `switchToForm`

> **Why?** On Action specifies the exact method name in your Java Controller that will run when the user clicks this button.

### Link the Controller and CSS

1. Click the root **AnchorPane** in Hierarchy
2. In **Controller** section (bottom of Inspector), set Controller class to: `com.pawmates.DashboardController`
3. In **Properties -> Stylesheets**, click the `+` button and add: `@../styles/styles.css`

> **Why?** The `fx:controller` attribute tells JavaFX which Java class handles this view's logic. The `@` prefix in stylesheets indicates a relative path.

### Save

Save the file as `dashboard.fxml` inside your `views` folder.

### Complete FXML Code

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.control.TableColumn?>
<?import javafx.scene.control.TableView?>
<?import javafx.scene.layout.AnchorPane?>

<AnchorPane maxHeight="-Infinity" maxWidth="-Infinity" minHeight="-Infinity" minWidth="-Infinity" prefHeight="401.0" prefWidth="600.0" stylesheets="@../styles/styles.css" xmlns="http://javafx.com/javafx/18" xmlns:fx="http://javafx.com/fxml/1" fx:controller="com.pawmates.DashboardController">
   <children>
      <Label layoutX="38.0" layoutY="31.0" styleClass="title-label" text="PawMates Dashboard" />
      <TableView fx:id="petTable" layoutX="57.0" layoutY="72.0" prefHeight="237.0" prefWidth="451.0">
        <columns>
          <TableColumn fx:id="nameColumn" prefWidth="75.0" text="Name" />
          <TableColumn fx:id="breedColumn" prefWidth="75.0" text="Breed" />
        </columns>
      </TableView>
      <Button fx:id="btnAdd" layoutX="464.0" layoutY="337.0" mnemonicParsing="false" onAction="#switchToForm" text="Add New Pet" />
   </children>
</AnchorPane>
```

---

## 4. Phase 2: The Intake Form (Scene Builder)

Now the page to add a new animal.

### New File

**File -> New** in Scene Builder

### The Layout

1. Drag a **VBox** (Vertical Box) to the canvas. This automatically stacks items
2. In **Layout** properties, set **Spacing** to `15` and **Padding** (all sides) to `20`
3. In **Properties**, set **Alignment** to `CENTER`

> **Why?** A VBox automatically arranges elements in a vertical column, saving us from manually dragging items into place.

### Image Upload Section

1. Drag an **ImageView**. Set **Fit Width/Height** to `150`. Set `fx:id` to `petImageView`
2. Drag a **Button** below it. Text: `"Upload Photo"`. `fx:id`: `btnUpload`. **On Action**: `handleUpload`

> **Why?** We need the `fx:id` on the ImageView so our Java code can swap the placeholder image with the photo the user selects.

### Input Fields

1. Drag a **TextField**. **Prompt Text**: `"Pet Name"`. `fx:id`: `nameField`
2. Drag a **TextField**. **Prompt Text**: `"Breed"`. `fx:id`: `breedField`

> **Why?** These IDs allow the Java code to extract the text the user types (`nameField.getText()`).

### Action Buttons

1. Drag an **HBox** (Horizontal Box) to put buttons side-by-side
2. Set HBox **Alignment** to `CENTER` and **Spacing** to `10`
3. Inside the HBox, add two **Buttons**:
   - Text: `"Save Pet"`. **On Action**: `handleSave`
   - Text: `"Cancel"`. **On Action**: `handleCancel`

### Link Controller and CSS

1. Set **Controller class** to: `com.pawmates.AddPetController`
2. Add stylesheet: `@../styles/styles.css` to the root VBox

### Save

Save as `addpet.fxml` in the `views` folder.

### Complete FXML Code

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.geometry.Insets?>
<?import javafx.scene.control.Button?>
<?import javafx.scene.control.TextField?>
<?import javafx.scene.image.ImageView?>
<?import javafx.scene.layout.HBox?>
<?import javafx.scene.layout.VBox?>

<VBox alignment="CENTER" maxHeight="-Infinity" maxWidth="-Infinity" minHeight="-Infinity" minWidth="-Infinity" prefHeight="400.0" prefWidth="600.0" spacing="15.0" stylesheets="@../styles/styles.css" xmlns="http://javafx.com/javafx/18" xmlns:fx="http://javafx.com/fxml/1" fx:controller="com.pawmates.AddPetController">
   <padding>
      <Insets bottom="20.0" left="20.0" right="20.0" top="20.0" />
   </padding>
   <children>
      <ImageView fx:id="petImageView" fitHeight="150.0" fitWidth="150.0" pickOnBounds="true" preserveRatio="true" />
      <Button fx:id="btnUpload" mnemonicParsing="false" onAction="#handleUpload" text="Upload Photo" />
      <TextField fx:id="nameField" prefHeight="26.0" prefWidth="312.0" promptText="Pet Name" />
      <TextField fx:id="breedField" promptText="Breed" />
      <HBox alignment="CENTER" prefHeight="100.0" prefWidth="200.0" spacing="10.0">
         <children>
            <Button mnemonicParsing="false" onAction="#handleSave" text="Save Pet" />
            <Button mnemonicParsing="false" onAction="#handleCancel" text="Cancel" />
         </children>
      </HBox>
   </children>
</VBox>
```

---

## 5. Phase 3: Pet Details Page (Scene Builder)

A page to view individual pet details when clicking on a table row.

### Create the Layout

1. Create a new file in Scene Builder
2. Drag a **VBox** to the canvas
3. Set **Spacing** to `15`, **Padding** to `20`, **Alignment** to `CENTER`

### Add Components

1. Add a **Label** for the title. `fx:id`: `titleLabel`. **Style Class**: `title-label`
2. Add an **ImageView**. `fx:id`: `petImageView`. **Fit Width/Height**: `180`
3. Add two **HBox** containers for name and breed labels:
   - First HBox: Label with text `"Name:"` (bold) + Label with `fx:id`: `nameLabel`
   - Second HBox: Label with text `"Breed:"` (bold) + Label with `fx:id`: `breedLabel`
4. Add a **Button**. Text: `"Back to Dashboard"`. **On Action**: `handleBack`

### Link Controller and CSS

1. Set **Controller class** to: `com.pawmates.PetDetailsController`
2. Add stylesheet: `@../styles/styles.css`

### Save

Save as `pet_details.fxml` in the `views` folder.

### Complete FXML Code

```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.geometry.Insets?>
<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.image.ImageView?>
<?import javafx.scene.layout.HBox?>
<?import javafx.scene.layout.VBox?>

<VBox alignment="CENTER" maxHeight="-Infinity" maxWidth="-Infinity" minHeight="-Infinity" minWidth="-Infinity" prefHeight="400.0" prefWidth="600.0" spacing="15.0" stylesheets="@../styles/styles.css" xmlns="http://javafx.com/javafx/18" xmlns:fx="http://javafx.com/fxml/1" fx:controller="com.pawmates.PetDetailsController">
   <padding>
      <Insets bottom="20.0" left="20.0" right="20.0" top="20.0" />
   </padding>
   <children>
      <Label fx:id="titleLabel" styleClass="title-label" text="Pet Details" />
      <ImageView fx:id="petImageView" fitHeight="180.0" fitWidth="180.0" pickOnBounds="true" preserveRatio="true" />
      <HBox alignment="CENTER" spacing="10.0">
         <children>
            <Label text="Name:" style="-fx-font-weight: bold;" />
            <Label fx:id="nameLabel" />
         </children>
      </HBox>
      <HBox alignment="CENTER" spacing="10.0">
         <children>
            <Label text="Breed:" style="-fx-font-weight: bold;" />
            <Label fx:id="breedLabel" />
         </children>
      </HBox>
      <Button mnemonicParsing="false" onAction="#handleBack" text="Back to Dashboard" />
   </children>
</VBox>
```

---

## 6. Phase 4: Styling with CSS

Create a file named `styles.css` in your `styles` folder.

### Complete CSS Code

```css
/* PawMates Application Styles */

/* Root styling */
.root {
    -fx-font-family: "Segoe UI", Arial, sans-serif;
    -fx-background-color: #f5f5f5;
}

/* Title label styling */
.title-label {
    -fx-font-size: 24px;
    -fx-font-weight: bold;
    -fx-text-fill: #4a6741;
}

/* Button styling */
.button {
    -fx-background-color: #5d8a4b;
    -fx-text-fill: white;
    -fx-font-size: 14px;
    -fx-padding: 8px 16px;
    -fx-background-radius: 5px;
    -fx-cursor: hand;
}

.button:hover {
    -fx-background-color: #4a6741;
}

.button:pressed {
    -fx-background-color: #3d5636;
}

/* TextField styling */
.text-field {
    -fx-background-color: white;
    -fx-border-color: #cccccc;
    -fx-border-radius: 4px;
    -fx-background-radius: 4px;
    -fx-padding: 8px;
    -fx-font-size: 14px;
}

.text-field:focused {
    -fx-border-color: #5d8a4b;
    -fx-border-width: 2px;
}

/* TableView styling */
.table-view {
    -fx-background-color: white;
    -fx-border-color: #cccccc;
    -fx-border-radius: 4px;
}

.table-view .column-header {
    -fx-background-color: #5d8a4b;
    -fx-text-fill: white;
    -fx-font-weight: bold;
    -fx-padding: 8px;
}

.table-view .column-header .label {
    -fx-text-fill: white;
    -fx-font-weight: bold;
}

.table-row-cell {
    -fx-background-color: white;
    -fx-border-color: transparent transparent #eeeeee transparent;
}

.table-row-cell:odd {
    -fx-background-color: #f9f9f9;
}

.table-row-cell:selected {
    -fx-background-color: #d4e5cd;
}

.table-row-cell:hover {
    -fx-background-color: #e8f0e4;
}

/* Label styling */
.label {
    -fx-text-fill: #333333;
    -fx-font-size: 14px;
}
```

### CSS Explanation

- **`.root`**: Applies to the entire application window
- **`-fx-` prefix**: JavaFX CSS properties use this prefix instead of standard CSS
- **Pseudo-classes**: `:hover`, `:pressed`, `:focused` work similarly to web CSS
- **Color scheme**: Uses earthy greens (#5d8a4b, #4a6741) to match the pet/nature theme

---

## 7. Phase 5: Coding the Logic

In this phase, we will write the Java code to make our beautiful UI functional.

### Step 1: The Model (Pet.java)

First, we need a plain Java class to represent a "Pet."

```java
package com.pawmates;

public class Pet {
    private String name;
    private String breed;
    private String imagePath;

    public Pet(String name, String breed, String imagePath) {
        this.name = name;
        this.breed = breed;
        this.imagePath = imagePath;
    }

    // Getters
    public String getName() { return name; }
    public String getBreed() { return breed; }
    public String getImagePath() { return imagePath; }

    // Setters
    public void setName(String name) { this.name = name; }
    public void setBreed(String breed) { this.breed = breed; }
    public void setImagePath(String imagePath) { this.imagePath = imagePath; }
}
```

> **Note:** This is a standard POJO (Plain Old Java Object). The getter names (`getName`, `getBreed`) must match the property names used in `PropertyValueFactory`.

---

### Step 2: The Dashboard Controller (DashboardController.java)

This controller manages the list of pets and handles navigation. Let's break it down piece by piece.

#### Part A: Imports

```java
package com.pawmates;

import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.fxml.Initializable;
import javafx.scene.Node;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.input.MouseEvent;
import javafx.stage.Stage;
import java.io.IOException;
import java.net.URL;
import java.util.ResourceBundle;
```

**What each import does:**

| Import | Purpose |
|--------|---------|
| `FXCollections` | Factory class to create JavaFX collections like `ObservableList` |
| `ObservableList` | A list that automatically notifies UI components when data changes |
| `ActionEvent` | Event object passed when buttons are clicked |
| `@FXML` | Annotation that marks fields/methods to be injected from FXML |
| `FXMLLoader` | Loads FXML files and creates the UI objects |
| `Initializable` | Interface that provides the `initialize()` method |
| `Node`, `Parent`, `Scene`, `Stage` | Core JavaFX classes for building the UI hierarchy |
| `TableView`, `TableColumn` | Components for displaying tabular data |
| `PropertyValueFactory` | Maps table columns to object properties |
| `MouseEvent` | Event object for mouse interactions (clicks, moves, etc.) |

---

#### Part B: Class Declaration and Field Injection

```java
public class DashboardController implements Initializable {

    @FXML private TableView<Pet> petTable;
    @FXML private TableColumn<Pet, String> nameColumn;
    @FXML private TableColumn<Pet, String> breedColumn;
```

**How this works:**

1. **`implements Initializable`**: This interface requires us to implement an `initialize()` method that runs automatically after the FXML is loaded.

2. **`@FXML` annotation**: This is the magic that connects your FXML to Java!
   - When `FXMLLoader` loads the FXML file, it scans the controller class for fields marked with `@FXML`
   - It matches each field name to an `fx:id` in the FXML
   - It then **injects** the actual UI object into that field

   For example: `@FXML private TableView<Pet> petTable;` gets linked to `<TableView fx:id="petTable" ...>` in the FXML.

3. **Generic types**: `TableView<Pet>` means this table will hold `Pet` objects. `TableColumn<Pet, String>` means this column displays a `String` value from a `Pet` object.

---

#### Part C: The Shared Data List

```java
    public static ObservableList<Pet> petList = FXCollections.observableArrayList();
```

**Why this matters:**

1. **`ObservableList`**: Unlike a regular `ArrayList`, an `ObservableList` automatically notifies any listeners when items are added, removed, or changed. The `TableView` listens to this list, so it updates automatically!

2. **`public static`**: We make this static so it's shared across all screens. When `AddPetController` adds a new pet to this list, the `DashboardController` will see it too.

3. **`FXCollections.observableArrayList()`**: Factory method that creates an empty `ObservableList`.

---

#### Part D: The Initialize Method

```java
    @Override
    public void initialize(URL location, ResourceBundle resources) {
        // Link columns to Pet properties
        nameColumn.setCellValueFactory(new PropertyValueFactory<>("name"));
        breedColumn.setCellValueFactory(new PropertyValueFactory<>("breed"));

        // Connect the list to the table
        petTable.setItems(petList);

        // Set up double-click handler
        petTable.setOnMouseClicked(this::handleRowClick);
    }
```

**Line-by-line breakdown:**

1. **`setCellValueFactory(new PropertyValueFactory<>("name"))`**:
   - Tells the column HOW to get data from each `Pet` object
   - `"name"` refers to the property name, which means it will call `pet.getName()`
   - Uses Java reflection to find and call the getter method

2. **`petTable.setItems(petList)`**:
   - Binds the `ObservableList` to the `TableView`
   - The table will now display all items in `petList`
   - Any changes to `petList` automatically appear in the table

3. **`petTable.setOnMouseClicked(this::handleRowClick)`**:
   - Registers an event handler for mouse clicks on the table
   - `this::handleRowClick` is a **method reference** - it points to our `handleRowClick` method
   - Every time the user clicks the table, `handleRowClick` will be called

---

#### Part E: Handling Row Clicks

```java
    private void handleRowClick(MouseEvent event) {
        if (event.getClickCount() == 2) {
            Pet selectedPet = petTable.getSelectionModel().getSelectedItem();
            if (selectedPet != null) {
                try {
                    openPetDetails(selectedPet, event);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

**How this works:**

1. **`event.getClickCount() == 2`**: Checks if user double-clicked (not single-click)

2. **`petTable.getSelectionModel().getSelectedItem()`**:
   - `getSelectionModel()` returns the object that tracks which row is selected
   - `getSelectedItem()` returns the actual `Pet` object from that row

3. **Null check**: If user double-clicks empty space, `selectedPet` will be null

4. **Try-catch**: `openPetDetails` throws `IOException` (file loading can fail), so we must handle it

---

#### Part F: Opening Pet Details (Passing Data Between Controllers)

```java
    private void openPetDetails(Pet pet, MouseEvent event) throws IOException {
        FXMLLoader loader = new FXMLLoader(getClass().getResource("/views/pet_details.fxml"));
        Parent root = loader.load();

        PetDetailsController controller = loader.getController();
        controller.setPet(pet);

        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }
```

**This is important - passing data between screens!**

1. **Create the loader**: `new FXMLLoader(...)` - we need to keep a reference to it

2. **Load the FXML**: `loader.load()` creates all the UI objects and returns the root node

3. **Get the controller**: `loader.getController()` returns the controller instance that was created during loading

4. **Pass the data**: `controller.setPet(pet)` calls our custom method to send the pet data to the new screen

5. **Switch scenes**: Get the current window (`Stage`) and replace its scene with the new one

**Why not use `FXMLLoader.load()` static method?**
Because then we can't access the controller! We need the loader instance to call `getController()`.

---

#### Part G: Navigation to Add Pet Form

```java
    @FXML
    void switchToForm(ActionEvent event) throws IOException {
        Parent root = FXMLLoader.load(getClass().getResource("/views/addpet.fxml"));
        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }
}
```

**The navigation pattern:**

1. **`@FXML`**: This method is called from FXML (via `onAction="#switchToForm"` on the button)

2. **`FXMLLoader.load(...)`**: Static method that loads FXML and returns the root node
   - `/views/addpet.fxml` - the leading `/` means "from the root of resources folder"

3. **Getting the Stage**:
   - `event.getSource()` → returns the Button that was clicked
   - `.getScene()` → returns the Scene the button is in
   - `.getWindow()` → returns the Window (which is actually a Stage)
   - Cast to `Stage` because `getWindow()` returns the parent type `Window`

4. **`stage.setScene(new Scene(root))`**: Replace the current scene with a new one containing our loaded FXML

5. **`stage.show()`**: Display the updated stage

---

### Complete DashboardController.java

Here's the complete controller with all parts together:

```java
package com.pawmates;

import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.fxml.Initializable;
import javafx.scene.Node;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.input.MouseEvent;
import javafx.stage.Stage;
import java.io.IOException;
import java.net.URL;
import java.util.ResourceBundle;

public class DashboardController implements Initializable {

    @FXML private TableView<Pet> petTable;
    @FXML private TableColumn<Pet, String> nameColumn;
    @FXML private TableColumn<Pet, String> breedColumn;

    public static ObservableList<Pet> petList = FXCollections.observableArrayList();

    @Override
    public void initialize(URL location, ResourceBundle resources) {
        nameColumn.setCellValueFactory(new PropertyValueFactory<>("name"));
        breedColumn.setCellValueFactory(new PropertyValueFactory<>("breed"));
        petTable.setItems(petList);
        petTable.setOnMouseClicked(this::handleRowClick);
    }

    private void handleRowClick(MouseEvent event) {
        if (event.getClickCount() == 2) {
            Pet selectedPet = petTable.getSelectionModel().getSelectedItem();
            if (selectedPet != null) {
                try {
                    openPetDetails(selectedPet, event);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    private void openPetDetails(Pet pet, MouseEvent event) throws IOException {
        FXMLLoader loader = new FXMLLoader(getClass().getResource("/views/pet_details.fxml"));
        Parent root = loader.load();

        PetDetailsController controller = loader.getController();
        controller.setPet(pet);

        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }

    @FXML
    void switchToForm(ActionEvent event) throws IOException {
        Parent root = FXMLLoader.load(getClass().getResource("/views/addpet.fxml"));
        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }
}
```

---

### Step 3: The AddPet Controller (AddPetController.java)

This controller handles user input for adding new pets.

```java
package com.pawmates;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Node;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.control.Alert;
import javafx.scene.control.TextField;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.stage.FileChooser;
import javafx.stage.Stage;
import java.io.File;
import java.io.IOException;

public class AddPetController {

    @FXML private TextField nameField;
    @FXML private TextField breedField;
    @FXML private ImageView petImageView;

    private String currentImagePath = null;

    @FXML
    void handleUpload(ActionEvent event) {
        FileChooser fileChooser = new FileChooser();
        fileChooser.setTitle("Select Pet Image");
        fileChooser.getExtensionFilters().add(
                new FileChooser.ExtensionFilter("Image Files", "*.png", "*.jpg", "*.jpeg")
        );

        File selectedFile = fileChooser.showOpenDialog(null);

        if (selectedFile != null) {
            currentImagePath = selectedFile.toURI().toString();
            petImageView.setImage(new Image(currentImagePath));
        }
    }

    @FXML
    void handleSave(ActionEvent event) throws IOException {
        if(nameField.getText().isEmpty() || breedField.getText().isEmpty()) {
            showAlert("Error", "Please fill in all fields!");
            return;
        }

        Pet newPet = new Pet(nameField.getText(), breedField.getText(), currentImagePath);
        DashboardController.petList.add(newPet);
        goBack(event);
    }

    @FXML
    void handleCancel(ActionEvent event) throws IOException {
        goBack(event);
    }

    private void goBack(ActionEvent event) throws IOException {
        Parent root = FXMLLoader.load(getClass().getResource("/views/dashboard.fxml"));
        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }

    private void showAlert(String title, String content) {
        Alert alert = new Alert(Alert.AlertType.ERROR);
        alert.setTitle(title);
        alert.setContentText(content);
        alert.showAndWait();
    }
}
```

---

### Step 4: The Pet Details Controller (PetDetailsController.java)

This controller displays detailed information about a selected pet.

```java
package com.pawmates;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Node;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.stage.Stage;
import java.io.IOException;

public class PetDetailsController {

    @FXML private Label titleLabel;
    @FXML private Label nameLabel;
    @FXML private Label breedLabel;
    @FXML private ImageView petImageView;

    private Pet currentPet;

    public void setPet(Pet pet) {
        this.currentPet = pet;

        nameLabel.setText(pet.getName());
        breedLabel.setText(pet.getBreed());
        titleLabel.setText(pet.getName() + "'s Details");

        if (pet.getImagePath() != null && !pet.getImagePath().isEmpty()) {
            try {
                petImageView.setImage(new Image(pet.getImagePath()));
            } catch (Exception e) {
                System.err.println("Failed to load image: " + e.getMessage());
            }
        }
    }

    @FXML
    void handleBack(ActionEvent event) throws IOException {
        Parent root = FXMLLoader.load(getClass().getResource("/views/dashboard.fxml"));
        Stage stage = (Stage) ((Node) event.getSource()).getScene().getWindow();
        stage.setScene(new Scene(root));
        stage.show();
    }
}
```

---

### Step 5: The Main Entry Point (Main.java)

This is the standard launcher class required for every JavaFX application.

```java
package com.pawmates;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {

    @Override
    public void start(Stage primaryStage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("/views/dashboard.fxml"));

        primaryStage.setTitle("PawMates Shelter Admin");
        primaryStage.setScene(new Scene(root, 600, 400));
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

---

### Step 6: Module Configuration (module-info.java)

If you are using Java 9+, you must create a `module-info.java` file in your `src/main/java` folder (outside of the package folders). This grants permission for JavaFX to access your code.

```java
module com.pawmates {
    requires javafx.controls;
    requires javafx.fxml;

    opens com.pawmates to javafx.fxml;
    exports com.pawmates;
}
```

**Key Explanations:**

- **`opens ... to javafx.fxml`**: This is critical! By default, your private fields (like `@FXML private TableView`) are hidden. This line tells Java that the `javafx.fxml` module is allowed to "break in" and inject data into your private fields. Without this, you will get `NullPointerExceptions`.

- **`exports com.pawmates`**: This allows the JavaFX Runtime to see your `Main` class and call the `start()` method.

---

## 8. Project Structure

Your final project structure should look like this:

```
src/
├── main/
│   ├── java/
│   │   ├── module-info.java
│   │   └── com/
│   │       └── pawmates/
│   │           ├── Main.java
│   │           ├── Pet.java
│   │           ├── DashboardController.java
│   │           ├── AddPetController.java
│   │           └── PetDetailsController.java
│   └── resources/
│       ├── views/
│       │   ├── dashboard.fxml
│       │   ├── addpet.fxml
│       │   └── pet_details.fxml
│       └── styles/
│           └── styles.css
└── pom.xml
```

---

## 9. Running the Application

### Using Maven (Command Line)

```bash
mvn clean javafx:run
```

### Using IDE

1. Right-click on `Main.java`
2. Select "Run 'Main.main()'"

---

## 10. Application Workflow

1. **Dashboard** loads showing empty pet table
2. Click **"Add New Pet"** → navigates to intake form
3. Upload a photo, enter name and breed, click **"Save Pet"**
4. Returns to dashboard with new pet in table
5. **Double-click** any row → opens pet details page
6. Click **"Back to Dashboard"** → returns to main list

---

## 11. Challenge Extensions

Once you've completed the basic app, try these enhancements:

1. **Add validation**: Require an image before saving
2. **Add more fields**: Age, weight, description, adoption status
3. **Delete functionality**: Add a button to remove pets from the list
4. **Edit functionality**: Allow editing existing pet information
5. **Data persistence**: Save pets to a JSON file so they persist between sessions
6. **Search/Filter**: Add a search box to filter pets by name or breed

---

## 12. Common Errors and Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| `NullPointerException` on `@FXML` field | `fx:id` doesn't match field name | Check spelling matches exactly |
| `LoadException: No controller specified` | Missing `fx:controller` in FXML | Add controller attribute to root element |
| `Invalid resource: ... not found` | Wrong path to FXML or CSS | Check path starts with `/` for absolute, `@` for stylesheets |
| Table columns don't show data | `PropertyValueFactory` name wrong | Must match getter name (e.g., "name" for `getName()`) |
| CSS not applying | Wrong stylesheet path | Use `@../styles/styles.css` for relative path from views |

---

## 13. Resources

- [JavaFX Documentation](https://openjfx.io/javadoc/18/)
- [Scene Builder Download](https://gluonhq.com/products/scene-builder/)
- [JavaFX CSS Reference](https://openjfx.io/javadoc/18/javafx.graphics/javafx/scene/doc-files/cssref.html)

---

You've built a complete JavaFX application with multiple screens, data binding, styling, and user interaction. These patterns form the foundation for building more complex desktop applications.
