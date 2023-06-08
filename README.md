# Tagesaufgabe

Willkommen zurück aus den Ferien! Wir hoffen ihr habt euch gut erholt und konntet die Feiertage genießen.
Heute wollen wir uns entspannt ins Coding wieder einarbeiten. Aus diesem Grund ist die heutige Tagesaufgabe ziemlich ähnlich zu der letzten Praxisaufgabe, damit ihr locker flockig wieder reinkommt.

Diesmal ist es keine KontakteApp, sondern ein Rezept Organizer, mit der ihr eure Lieblingsrezepte in euerer eigenen App organisieren und speichern könnt.

Ihr könnt euch sehr stark an der letzten Praxisaufgabe am Donnerstag Contacts orientieren.

Ihr könnt das Design so wie folgt gestalten oder wie ihr es wollt. 

<img src="https://user-images.githubusercontent.com/113107143/231763614-7f7bca4c-13cb-4168-b350-1b960f18c8c9.png" width="214" height="460"> <img src="https://user-images.githubusercontent.com/113107143/231764765-8e63bc1f-5675-493d-9d7d-aaa331b6b479.png" width="214" height="460"><img src="https://user-images.githubusercontent.com/113107143/231764814-934ba405-ee92-489e-8618-da1c0c4b825b.png" width="214" height="460"><img src="https://user-images.githubusercontent.com/113107143/231764817-2c964c27-3da1-4f8c-91fa-826d05480e22.png" width="214" height="460"><img src="https://user-images.githubusercontent.com/113107143/231764832-f8b3ce73-6992-403c-8f4a-4920f21a742a.png" width="214" height="460">

<details><summary>

## Projektvorbereitung

</summary>

1. Erstelle ein iOS Projekt.
2. Erstelle eine SwiftUI-Datei namens: `HomeView`
3. Erstelle eine SwiftUI-Datei namens: `RezeptDetailView`
4. Erstelle eine SwiftUI-Datei namens: `AddRezeptView`
5. Erstelle eine Swift-Datei namens: `RezeptViewModel`

6. Erstelle jeweils einen `View`, `ViewModel` und `Model` Ordner und verschiebe die Dateien in die richtigen Ordner.

7. Commmitet dann euer Projekt. (Hinweis, falls ihr nicht wisst wie, schaut euch das Video von Oscar an https://syntaxinstitut.slack.com/archives/C03K6LX9ELW/p1680776398739009)

</details>

<details><summary>

## Data Model

</summary>

1. Erstelle ein Data Model `rezepte`
2. Geh in die Datei `rezepte` und erstelle eine Entity `Rezept` und füge Attribute `beschreibung`, `rezeptName` und `zutaten` als String und `portionen` als Int16 hinzu.

(Int16 bedeutet, dass nur Integer Werte zwischen  -32768 bis 32767 möglich sind. Passt in diesem Fall, weil niemand mehr als 32767 Portionen kocht.)

3. Verschiebe das Data Model in den richtigen Ordner.

</details>

<details><summary>

## RezeptViewModel

</summary>

  1. Öffne die Datei `RezeptViewModel.swift`
  
  2. Erstelle eine Klasse `RezeptViewModel` die von `ObservableObject` erbt.
  
  3. Füge einen Member `persistentContainer` vom Typ `NSPersistentContainer` hinzu. Füge einen Member
  `savedRezepte` vom Typ Array von `Rezept` hinzu. Dieser Member sollte mit @Published annotiert werden.
  
  4. Schreibe einen Konstruktor `init()`, in dem der Member `persistentContainer` initialisiert wird. Rufe seine
  Memberfunktion `.loadPersistentStores` auf. und fange Fehler ab. Am Ende des Konstruktors soll eine später
  definierte Funktion `fetchContacts` aufgerufen werden.
  
  5. Schreibe eine Memberfunktion `fetchContacts`, welche einen `NSFetchRequest<Rezept>` ausführt, und fange
  Fehler ab.
  
  6. Schreibe Memberfunktionen `createRezept(rezeptName: String, portionen: Int16, zutaten: String, beschreibung:
  String)`, `updateRezept(_ rezept: Rezept, rezeptName: String, portionen: Int16, zutaten: String,beschreibung:
  String)`, `deleteRezept(indexSet: IndexSet)`, die analog zu den Livebeispielen und der KontakteApp, Rezepte in
  die Datenbank einfügen, updaten oder löschen.
  
  7. Schreibe eine Memberfunktion `fetchContactsByRezeptName`, welche einen `NSFetchRequest<Rezept> macht,
  gefiltert nach Rezeptname (siehe CONTAINS[cd] in dem Livebeispiel oder KontakteApp).
  
</details>

 <details><summary>

## HomeView

</summary>
   1. In dieser Datei erstelle ein Struct `HomeView`, welche von `View` erbt.
   
   2. Füge einen Member `viewModel` hinzu, welcher mit dem `RezeptViewModel` initialisiert werden soll. Dieser
   Member soll as `@StateObject` annotiert werden.
   
   3. Füge einen weiteren Member `isDrawerOpen` hinzu, welcher anfangs auf `false` gesetzt ist, und mit `@State`
   annotiert ist.
   
   4. Im `body` des Views, schreibe einen `NavigationStack`, welcher aus einer `List `besteht. In der Liste nutze
   `ForEach`, um die `savedRezepte` aus dem `viewModel` jeweils als `NavigationLink` darzustellen. Innerhalb des
   `NavigationLink` soll ein später definiertes `RezeptDetailView` aufgerufen werden.
   
   5. Die `NavigationLinks` sollen als `label` einen `Text` mit dem Rezeptnamen des behandelten Rezeptes
   haben.
   
   6. An dem `ForEach` füge hinten den Modifier `.onDelete` an, dessen `perform:` Argument die Methode
   `viewModel.deleteRezept` sein soll.
   
   7. An dem `List` füge einen Modifier `.toolbar` an, welcher ein `ToolbarItem` enthalten soll, in dem ein
   `Button` steht, der als `label:` Argument ein `Label` mit Text `Add Recipe` und `systemImage: plus` haben
   soll.
   
   8. Der besagte `Button` soll als `action:` den Member `isDrawerOpen` auf `true` setzen.
   
   9. Letztlich soll der `VStack` einen Modifier `.navigationTitle()` bekommen, mit Titel `Rezepte`.
   
  

Ein weiterer Modifier für den "VStack" geben wir vor:
```
.navigationTitle("Contacts")
.sheet(isPresented: $isDrawerOpen, content: {
    AddContactView(isDrawerOpen: $isDrawerOpen, viewModel: viewModel)
})
```
</details>
  
<details><summary>

## RezeptDetailView

</summary>
  
  1. Öffne die Datei `RezeptDetailView.swift`
  
  2. In dieser Datei erstelle ein Struct `RezeptDetailView`, welche von `View` erbt.
  
  3. Dieses Struct soll mehrere Member (die selben Member 'rezeptName',... wie die Entitity im Core Data) vom Typ
  `String` und eins vom Typ `Int16` haben und jeweils als @State annotiert werden.
  
  4. Im `body` des Views soll innerhalb eines VStacks für jede der Rezeptdaten ein `Text` View enthalten sein
  Empfohlen ist, die Modifier .font() und .padding() zu nutzen.
  
  5. Nutze für die Zutatenanzeige und die Beschreibungsanzeige eine `ScrollView`, da der Text etwas länger werden
  kann.


</details>
  
  <details><summary>

## AddRezeptView

</summary>

  1. Öffne die Datei `AddRezeptView.swift`
    
  2. In dieser Datei erstelle ein Struct `AddRezeptView`, welche von `View` erbt.
    
  3. Dieses Struct soll mehrere Member (die selben Member 'rezeptName',... wie die Entitity im Core Data) vom
    Typ `String` und eins vom Typ `Int16` haben und jeweils als @State annotiert werden.
    
  4. Weiterhin soll sie einen `@Binding` annotierten Member `isDrawerOpen` und einen `@StateObject` annotierten
    Menber `viewModel` haben.
    
  5. Im `body` des Views soll innerhalb eines `VStacks`, in einem darin enthaltenen `Form` für jede der
    Rezeptdatenn eine `Section` View enthalten sein. Nutze in jeder Section ein `TextField` womit ein Feld der
    Rezeptdaten dargestellt wird. (Tipp: Da Zutaten und Beschreibung oftmals mehr als eine Zeile beanspruchen,
    nutze statt ein normales `Textfield` ein `TextEditor` gerne dazu selber recherchieren)
    
  6. Am Ende der `Form` füge eine `Section` ein, in der ein `Button` steht. Der `action:` Parameter soll
    `viewModel.createRezept` aufrufen, und `isDrawerOpen` auf `false` setzen.
    


</details>
  <details><summary>

## ContentView

</summary>
    
    
  1. Öffne die Datei `ContenView.swift`
    
  2. Rufe im `body` `HomeView()` auf
    
  3. Starte die App
    
 </details>
