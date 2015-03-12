---
layout: article
title: "JavaFX 8 Tutorial - Parte 1: Scene Builder"
date: 2014-04-19 01:00
updated: 2015-03-12 00:00
slug: javafx-8-tutorial-part1
github: https://github.com/marcojakob/code.makery.ch/edit/master/collections/java/javafx-8-tutorial-part1.md
description: "Learn how to set up a JavaFX project. This is part one of a seven-part tutorial about designing, programming and deploying an address application with JavaFX."
image: /assets/library/javafx-8-tutorial/part1/addressapp-part1.png
published: true
prettify: true
comments: true
sidebars:
- header: "Articoli in questa serie"
  body:
  - text: "Introduzione"
    link: /java/javafx-8-tutorial-intro
    paging: Intro
    active: true
  - text: "Parte 1: Scene Builder"
    link: /java/javafx-8-tutorial-part1/
    paging: 1
  - text: "Parte 2: Model and TableView"
    link: /java/javafx-8-tutorial-part2/
    paging: 2
  - text: "Parte 3: Interazione con l'utente"
    link: /java/javafx-8-tutorial-part3/
    paging: 3
  - text: "Parte 4: CSS Styling"
    link: /java/javafx-8-tutorial-part4/
    paging: 4
  - text: "Parte 5: Conservazione dati come XML"
    link: /java/javafx-8-tutorial-part5/
    paging: 5
  - text: "Parte 6: Grafico delle statistiche"
    link: /java/javafx-8-tutorial-part6/
    paging: 6
  - text: "Parte 7: Deployment"
    link: /java/javafx-8-tutorial-part7/
    paging: 7
- header: "Downloa"
  body:
  - text: Parte 1 come progetto Eclipse <em>(requires at least JDK 8u40)</em>
    link: https://github.com/marcojakob/tutorial-javafx-8/releases/download/v1.1/addressapp-jfx8u40-part-1.zip
    icon-css: fa fa-fw fa-download
- header: Languages
  languages: true
  body:
  - text: English
    link: /java/javafx-8-tutorial-part1/
    icon-css: fa fa-fw fa-globe
    active: true
  - text: Português
    link: /library/javafx-8-tutorial/pt/part1/
    icon-css: fa fa-fw fa-globe
  - text: Español
    link: /library/javafx-8-tutorial/es/part1/
    icon-css: fa fa-fw fa-globe
  - text: 中文（简体）
    link: /library/javafx-8-tutorial/zh-cn/part1/
    icon-css: fa fa-fw fa-globe
  - text: Русский
    link: /library/javafx-8-tutorial/ru/part1/
    icon-css: fa fa-fw fa-globe
  - text: Bahasa Indonesia
    link: /library/javafx-8-tutorial/id/part1/
    icon-css: fa fa-fw fa-globe
  - text: Français
    link: /library/javafx-8-tutorial/fr/part1/
    icon-css: fa fa-fw fa-globe
  - text: Italiano
    link: /library/javafx-8-tutorial/it/
    icon-css: fa fa-fw fa-globe
---

![Screenshot AddressApp Part 1](/assets/library/javafx-8-tutorial/part1/addressapp-part1.png)

### Argomenti nella parte 1

* Conoscere JavaFX
* Creare ed eseguire un progetto JavaFX 
* Usare Scene Builder per progettare l'interfaccia utente
* Struttura base dell'applicazione usando il pattern Model-View-Controller (MVC) 


*****


### Prerequisiti

* Ultima versione di [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) (incluso **JavaFX 8**).
* Eclipse 4.4 o superiore con il plugin e(fx)clipse. La via più facile è scaricare una distro preconfigurata dal  [sito di e(fx)clipse](http://efxclipse.bestsolution.at/install.html#all-in-one). Come alternativa puoi usare un [sito di aggiornamento](http://www.eclipse.org/efxclipse/install.html) per la tua installazione di Eclipse.
* [Scene Builder 8.0](http://gluonhq.com/products/downloads/) (fornito da Gluon perchè [Oracle lo rende disponibile solo sotto forma di codice sorgente](http://www.oracle.com/technetwork/java/javase/downloads/sb2download-2177776.html)).


### Configurazione di Eclipse 

Abbiamo bisogno che Eclipse usi JDK 8 e dovremo dirgli dove trovare Scene Builder:

1. Apri le preferenze di Eclipse e vai a *Java | Installed JREs*.

2. Clicca *Add...*, seleziona *Standard VM* e scegli la *Directory* di installazione del tuo JDK 8.

3. Rimuovi gli altri JREs o JDKs così che **JDK 8 vada di default**.   
![Preferences JDK](/assets/library/javafx-8-tutorial/part1/preferences-jdk.png)

4. Vai su *Java | Compiler*. Imposta **Compiler compliance level to 1.8**.   
![Preferences Compliance](/assets/library/javafx-8-tutorial/part1/preferences-compliance.png)

5. Vai sulle preferenze di *JavaFX*. Specifica il percorso dell'eseguibile di Scene Builder.   
![Preferences JavaFX](/assets/library/javafx-8-tutorial/part1/preferences-javafx.png)


### Link di supporto

Potresti voler aggiungere ai tuoi preferiti i seguenti link:

* [Java 8 API](http://docs.oracle.com/javase/8/docs/api/) - JavaDoc for the standard Java classes
* [JavaFX 8 API](http://docs.oracle.com/javase/8/javafx/api/) - JavaDoc for JavaFX classes
* [ControlsFX API](http://controlsfx.bitbucket.org/) - JavaDoc for the [ControlsFX project](http://fxexperience.com/controlsfx/) for additional JavaFX controls
* [Oracle's JavaFX Tutorials](http://docs.oracle.com/javase/8/javafx/get-started-tutorial/get_start_apps.htm) - Official JavaFX Tutorials by Oracle

Adesso, cominciamo!


*****


## Creare un nuovo progetto JavaFX

In Eclipse (con e(fx)clipse installato) andare su *File | New | Other...* e scegliere *JavaFX Project*.   
Specificare il nome del progetto (e.g. *AddressApp*) e cliccare su *Finish*.

Rimuovere il package *application*  e il suo contenuto se questo viene automaticamente creato.


### Creare i Packages

Fin dall'inizio seguiremo i buoni principi della progettazione softaware. Un principio molto importante è qeullo del [**Model-View-Controller** (MVC)](http://en.wikipedia.org/wiki/Model_View_Controller). Segeuendo questo, dividiamo il nostro codice in tre unità e creiamo un package per ognuna di queste (Tasto destro su src-folder, *New... | Package*):

* `ch.makery.address` - contenente *la maggior parte* delle classi controller (=business logic)
* `ch.makery.address.model` - contenente le classi model
* `ch.makery.address.view` - contenente le view 

**Nota:** Il nostro package view conterrà inoltre alcuni controller che sono relativi as una singola view. Gli chiameremo **view-controllers**.


*****


## Creare il file di layout FXML 

Ci sono due strade per creare l'interfaccia utente. O usare un file XML o programmarla tutta in Java. Gurdandovi intorno su internet incontrerete entrambe. Useremo XML (.fxml) per molte parti. IO trovo che questa sia la via più pulita per tenere controller e view saparati gli uni dagli altri. Inoltre, possimao usare Scene Builder per editare i nostri XML. Questo significa che non lavoreremo direttamente con XML.

Tasto destro sul package view e creiamo un nuovo *FXML Document* chiamato `PersonOverview`.   

![New FXML Document](/assets/library/javafx-8-tutorial/part1/new-fxml-document.png)

![New PersonOverview](/assets/library/javafx-8-tutorial/part1/new-person-overview.png)



*****


## Progettare con Scene Builder

<div class="alert alert-warning">
  **Nota:** Se non riuscite a farlo funzionare, scaricate il sorgente di questa parte del tutorial e provate con il file fxml incluso.
</div>

Tasto destro su `PersonOverview.fxml` e click su *Open with Scene Builder*. Adesso dovreste vedere Scene Builder con solo un *AncherPane* (visibile sotto Hierarchy sulla sinistra).

(Se Scene Builder non si apre, andare su *Window | Preferences | JavaFX* e settare il giusto percorso dell'installazione di Scene Builder).

1. Selezionare *Anchor Pane* nella Hierarchy e modificare le dimensioni sotto Layout (lato destro):   
![Anchor Pane Size](/assets/library/javafx-8-tutorial/part1/anchor-pane-size.png)

2. Aggiungere un *Split Pane (Horizontal Flow)* trascinandolo dalla Library nella area principale. Tasto destro su *Split Pane* nella vista *Hierarchy* e selezionare *Fit to Parent*.   
![Fit to Parent](/assets/library/javafx-8-tutorial/part1/fit-to-parent.png)

3. Trascinare una *TableView* (sotto *Controls*) nella parte sinistra dello *SplitPane*. Selezionare la TableView (non la colonna) e impostare il seguente layout constraints per la TableView. All'interno di un *AnchorPane* puoi sempre impostare gli  anchors per i quattro bordi (Più informazioni sui Layouts](http://docs.oracle.com/javase/8/javafx/layout-tutorial/builtin_layouts.htm)).   
![TableView Anchors](/assets/library/javafx-8-tutorial/part1/table-view-anchors.png)

4. Go to the menu *Preview | Show Preview in Window* to see, whether it behaves right. Try resizing the window. The TableView should resize together with the window as it is anchored to the borders.

5. Change the column text (under Properties) to "First Name" and "Last Name".   
![Column Texts](/assets/library/javafx-8-tutorial/part1/column-texts.png)

6. Select the *TableView* and choose *constrained-resize* for the *Column Resize Policy* (under Properties). This ensures that the colums will always take up all available space.   
![Column Resize Policy](/assets/library/javafx-8-tutorial/part1/column-resize-policy.png)

7. Add a *Label* on the right side with the text "Person Details" (hint: use the search to find the *Label*). Adjust it's layout using anchors.   
![Person Details Label](/assets/library/javafx-8-tutorial/part1/person-details-label.png)

8. Add a *GridPane* on the right side, select it and adjust its layout using anchors (top, right and left).    
![GridPane Layout](/assets/library/javafx-8-tutorial/part1/grid-pane-layout.png)

9. Add the following labels to the cells.   
*Note: To add a row to the GridPane select an existing row number (will turn yellow), right-click the row number and choose "Add Row".*   
![Add labels](/assets/library/javafx-8-tutorial/part1/add-labels.png)

10. Add a *ButtonBar* at the bottom. Add three buttons to the bar. Now, set anchors (right and bottom) to the *ButtonBar* so it stays in the right place.   
![Button Group](/assets/library/javafx-8-tutorial/part1/button-group.png)

11. Now you should see something like the following. Use the *Preview* menu to test its resizing behaviour.   
![Preview](/assets/library/javafx-8-tutorial/part1/scene-builder-preview.png)



*****


## Create the Main Application

We need another FXML for our root layout which will contain a menu bar and wraps the just created `PersonOverview.fxml`.

1. Create another *FXML Document* inside the view package called `RootLayout.fxml`. This time, choose *BorderPane* as the root element.   
![New RootLayout](/assets/library/javafx-8-tutorial/part1/new-root-layout.png)

2. Open the `RootLayout.fxml` in Scene Builder.

3. Resize the *BorderPane* with *Pref Width* set to 600 and *Pref Height* set to 400.   
![RootLayout Size](/assets/library/javafx-8-tutorial/part1/root-layout-size.png)

4. Add a *MenuBar* into the TOP Slot. We will not implement the menu functionality at the moment.   
![MenuBar](/assets/library/javafx-8-tutorial/part1/menu-bar.png)


### The JavaFX Main Class 

Now, we need to create the **main java class** that starts up our application with the `RootLayout.fxml` and adds the `PersonOverview.fxml` in the center. 

1. Right-click on your project and choose *New | Other...* and choose *JavaFX Main Class*.   
![New JavaFX Main Class](/assets/library/javafx-8-tutorial/part1/new-main-class.png)

2. We'll call the class `MainApp` and put it in the controller package `ch.makery.address` (note: this is the parent package of the `view` and `model` subpackages).   
![New JavaFX Main Class](/assets/library/javafx-8-tutorial/part1/new-main-class2.png)


The generated `MainApp.java` class extends from `Application` and contains two methods. This is the basic structure that we need to start a JavaFX Application. The most important part for us is the `start(Stage primaryStage)` method. It is automatically called when the application is `launched` from within the `main` method.

As you see, the `start(...)` method receives a `Stage` as parameter. The following graphic illustrates the structure of every JavaFX application:

![New FXML Document](/assets/library/javafx-8-tutorial/part1/javafx-hierarchy.png)   
*Image Source: http://www.oracle.com*

**It's like a theater play**: The `Stage` is the main container which is usually a `Window` with a border and the typical minimize, maximize and close buttons. Inside the `Stage` you add a `Scene` which can, of course, be switched out by another `Scene`. Inside the `Scene` the actual JavaFX nodes like `AnchorPane`, `TextBox`, etc. are added.

For more information on this turn to [Working with the JavaFX Scene Graph](http://docs.oracle.com/javase/8/javafx/scene-graph-tutorial/scenegraph.htm).


*****

Open `MainApp.java` and replace the code with the following:

<pre class="prettyprint lang-java">
package ch.makery.address;

import java.io.IOException;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.scene.layout.AnchorPane;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

public class MainApp extends Application {

    private Stage primaryStage;
    private BorderPane rootLayout;

    @Override
    public void start(Stage primaryStage) {
        this.primaryStage = primaryStage;
        this.primaryStage.setTitle("AddressApp");

        initRootLayout();

        showPersonOverview();
    }
    
    /**
     * Initializes the root layout.
     */
    public void initRootLayout() {
        try {
            // Load root layout from fxml file.
            FXMLLoader loader = new FXMLLoader();
            loader.setLocation(MainApp.class.getResource("view/RootLayout.fxml"));
            rootLayout = (BorderPane) loader.load();
            
            // Show the scene containing the root layout.
            Scene scene = new Scene(rootLayout);
            primaryStage.setScene(scene);
            primaryStage.show();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * Shows the person overview inside the root layout.
     */
    public void showPersonOverview() {
        try {
            // Load person overview.
            FXMLLoader loader = new FXMLLoader();
            loader.setLocation(MainApp.class.getResource("view/PersonOverview.fxml"));
            AnchorPane personOverview = (AnchorPane) loader.load();
            
            // Set person overview into the center of root layout.
            rootLayout.setCenter(personOverview);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
	/**
	 * Returns the main stage.
	 * @return
	 */
	public Stage getPrimaryStage() {
		return primaryStage;
	}

    public static void main(String[] args) {
        launch(args);
    }
}
</pre>

The various comments should give you some hints about what's going on.

If you run the application now, you should see something like the screenshot at the beginning of this post.


### Frequent Problems

If JavaFX can't find the `fxml` file you specified, you might get the following error message: 

`java.lang.IllegalStateException: Location is not set.`

To solve this issue double check if you didn't misspell the name of your `fxml` files!

<div class="alert alert-warning">
  If it still doesn't work, download the source of this tutorial part and try it with the included fxml.
</div>


*****

### What's Next?

In [Tutorial Part 2](/java/javafx-8-tutorial-part2/) we will add some data and functionality to our AddressApp.


##### Some other articles you might find interesting

* [JavaFX Dialogs (official)](/blog/javafx-dialogs-official/)
* [JavaFX Date Picker](/blog/javafx-8-date-picker/)
* [JavaFX Event Handling Examples](/blog/javafx-8-event-handling-examples/)
* [JavaFX TableView Sorting and Filtering](/blog/javafx-8-tableview-sorting-filtering/)
* [JavaFX TableView Cell Renderer](/blog/javafx-8-tableview-cell-renderer/)
