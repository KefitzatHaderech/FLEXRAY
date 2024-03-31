<!-- TOC -->

- [Flexray](#flexray)
    - [Hinführung](#hinf%C3%BChrung)
        - [Elektronische Assistenten](#elektronische-assistenten)
        - [Brake-by-Wire](#brake-by-wire)
        - [Steer-by-Wire](#steer-by-wire)
        - [Sicherheit und Fehlertoleranz](#sicherheit-und-fehlertoleranz)
        - [Zusammensetzbarkeit](#zusammensetzbarkeit)
        - [Motivation für FlexRay](#motivation-f%C3%BCr-flexray)
        - [Anfänge von FlexRay](#anf%C3%A4nge-von-flexray)
        - [FlexRay Konsortium](#flexray-konsortium)
                - [Webseite der ISO - International Organization for Standardization](#webseite-der-iso---international-organization-for-standardization)
    - [FlexRay Kommunikation](#flexray-kommunikation)
        - [Kommunikationsarchitektur](#kommunikationsarchitektur)
        - [Passive Topologien](#passive-topologien)
        - [Aktive Topologien](#aktive-topologien)
        - [FlexRay Knoten](#flexray-knoten)
        - [FlexRay Controller](#flexray-controller)
        - [FlexRay Bus](#flexray-bus)
        - [FlexRay Buspegel](#flexray-buspegel)
        - [FlexRay Busankopplung](#flexray-busankopplung)
        - [Busguardian BG](#busguardian-bg)
    - [FlexRay Buszugriff](#flexray-buszugriff)
        - [Prinzip des Buszugriffs](#prinzip-des-buszugriffs)
        - [Kommunikationszyklus](#kommunikationszyklus)
        - [Statisches Segment](#statisches-segment)
        - [Statischer Slot](#statischer-slot)
        - [Dynamisches Segment](#dynamisches-segment)
        - [Dynamischer Slot](#dynamischer-slot)
        - [Demonstration](#demonstration)
    - [FlexRay Framing](#flexray-framing)
        - [Frame Header](#frame-header)
        - [Frame Payload](#frame-payload)
        - [Codierung](#codierung)
    - [FlexRay Synchronisation](#flexray-synchronisation)
        - [Synchronisationsprinzip](#synchronisationsprinzip)
        - [Phasen- und Frequenzkorrektur](#phasen--und-frequenzkorrektur)
        - [Synchronisationsmethode](#synchronisationsmethode)

<!-- /TOC --># Flexray



## Hinführung

Steigender Funktionsumfang
An die Tatsache, dass die an das Automobil gestellten Anforderungen an den Verbrauch, den Komfort und die Sicherheit nur noch mit elektronischen Funktionen erfüllt werden können, hat man sich längst gewöhnt. Zum Beispiel an den Komfortzugang, bei dem das Fahrzeug den elektronischen Schlüssel automatisch erkennt und sich bequem öffnen und starten lässt, ohne dass man den Schlüssel in die Hand nehmen muss. Oder an die Geschwindigkeitsregelung, bei der Fahrgeschwindigkeiten ab 30 km/h konstant gehalten werden und die so mehr Komfort auf langen Strecken bietet.

Es sind aber auch die versteckten Funktionen zu nennen, wie beispielsweise die elektronische Dämpferkontrolle, die die Radlastschwankungen reduziert und eine gute Verbindung zwischen Fahrbahn und Reifen gewährleistet. So wird ein optimales Schwingungsverhalten des Fahrzeugaufbaus, unabhängig vom Straßenzustand und bei jeder Beladung, geboten.

Hat man sich anfangs vor allem mit elektronischen Funktionen, die die Fahrsicherheit erhöhen, schwer getan, so stoßen diese mittlerweile auf große Akzeptanz. Gerade deshalb, weil die aktiven Sicherheitssysteme wie ABS und ESP einen maßgeblichen Anteil daran haben, dass trotz beträchtlichem Zuwachs des Kraftfahrzeugbestands und der Autofahrten, die Zahl der Unfälle rückläufig ist. Mit dem Ziel, das Autofahren noch sicherer zu machen, forciert die Kfz-Branche vor allem die Weiter- und Neuentwicklung von innovativen aktiven Sicherheits- und Fahrerassistenzfunktionen.

So sorgt beispielsweise ein elektronischer Assistent für die automatische Anpassung der Fahrgeschwindigkeit an den Verkehrsfluss. Ein anderer elektronischer Assistent beobachtet permanent die Nachbarspuren bis zu 50 m Reichweite und warnt den Fahrer bei Überhol- und Spurwechselvorgängen, wenn ein Fahrzeug in der Nachbarspur erkannt wurde. Ein weiterer elektronischer Assistent ermöglicht zum Beispiel sicheres Einparken.


![1706353913176](image/1706353913176.png)

Verteilte Systeme
Hinter diesen ganzen aktiven Sicherheits- und Fahrerassistenzsystemen stehen hoch dynamische Regelungsapplikationen, die kaum noch innerhalb eines Steuergerätes geschlossen werden, sondern mithilfe eines Kommunikationssystems über mehrere Steuergeräte hinweg. Nicht mehr autonome Steuergeräte, sondern verteilte Systeme bilden zunehmend das Rückgrat moderner Sicherheits- und Fahrerassistenzsysteme.


![1706353937404](image/1706353937404.png)

Trotz Einbezug eines Kommunikationssystems muss die Einhaltung einer streng festgelegten zeitlichen Wirkungskette sichergestellt werden. In den Fokus geraten Kommunikationssysteme, die idealerweise eine buslastunabhängige deterministische Datenkommunikation, also eine äquidistante Signalübertragung garantieren. Die Rede ist von Echtzeitkommunikationssystemen mit zeitgesteuertem Ansatz.

Elektronifizierung
Die Elektronifizierung des Automobils macht auch nicht vor Domänen Halt, in denen traditionell die Mechanik und Hydraulik dominieren. Um Fahrerassistenzfunktionen mit noch höherem Nutzen realisieren zu können, benötigt man elektronische Schnittstellen zum Fahrwerk vor allem zur Bremsanlage und zur Lenkung.

Solche elektronische Schnittstellen stellen beispielsweise die elektrohydraulische und die elektromechanische Bremse - EMB dar. Werden bei der elektrohydraulischen Bremse die Bremssättel noch hydraulisch betätigt, so erzeugen bei der elektromechanischen Bremse Elektromotoren die Bremskräfte direkt an den Rädern, gesteuert von einer elektronischen Regeleinheit, die ihren Input wiederum über ein elektronisches Bremspedal mit Pedalgefühlsimulator (Force Feedback) erhält. Die Übertragung der Steuer- und Sensorsignale erfolgt über Kommunikationsleitungen.

Brake-by-Wire
Durch ein solches Brake-by-Wire-System sind nicht nur individuelle Bremseingriffe an den einzelnen Rädern möglich, was die Bremsstabilität wesentlich verbessert. Möglich wird auch das Anpassen der Pedalcharakteristik und der Bremswirkung an den Fahrer einfach durch die bloße Änderung der Software. Schließlich erlaubt die Elektronik vor Ort eine verbesserte Diagnosefähigkeit und führt so zu einer erhöhten Betriebssicherheit. Ein sehr großes Potenzial eines Brake-by-Wire-Systems ist die Einbeziehung der Bremse in die Fahrdynamikregelung um die aktive Sicherheit erhöhen zu können.

So vielfältig das Potenzial von Brake-by-Wire-Systemen auch ist - sie stellen ein großes Sicherheitsrisiko dar. Schon die Störung oder der Ausfall einer einzelnen Systemkomponente kann schwerwiegende Folgen haben. Deshalb müssen Brake-by-Wire-Systeme fehlertolerant ausgelegt sein: nur so kann gewährleistet werden, dass bei Auftreten eines beliebigen Fehlers die gesetzlich vorgeschriebene Grundbremsfunktionalität erfüllt wird.

Mechanische Lenkung
Die Lenksysteme heutiger Kraftfahrzeuge werden abhängig von den erforderlichen Lenkkräften mit hydraulischen, elektrohydraulischen oder elektrischen Lenkhilfen ausgerüstet. Unabhängig von der Art der Lenkunterstützung besitzen diese Systeme über die Lenksäule eine mechanische Verbindung zwischen Lenkrad und gelenkten Rädern, so dass auch bei Ausfall der Servounterstützung der mechanische Durchgriff weiter besteht.

Elektrische Lenkung
Beim in der Grafik dargestellten elektrischen Lenksystem wird der Lenkeingriff des Autofahrers über eine Steuerleitung von einem Steuergerät entgegengenommen, verarbeitet und wieder über eine Steuerleitung als Stellbefehl an den Aktor übertragen und dort in eine Bewegung umgesetzt. An die Stelle der mechanischen Kopplung treten ein Aktor zur Positionierung der Räder (Radwinkelsteller) sowie ein Motor zur Simulation der Rückstellkräfte am Lenkrad (Handkraftaktor). Die Koordination zwischen Handkraftaktor und Radwinkelsteller übernimmt der Lenkungsregler. Die Lenksäule wird quasi durch Kommunikationsleitungen ersetzt, der Fahrer lenkt „by wire“.

Steer-by-Wire
Neben der Realisierung einer variablen Lenkunterstützung und Lenkübersetzung, die Möglichkeit einer individuellen Einstellung der Lenkcharakteristik steckt das größte Potenzial einer solchen Lenkung nach dem Steer-by-Wire-Prinzip in der Einbeziehung der Lenkung in die Fahrdynamikregelung um die aktive Sicherheit erhöhen zu können. Als konsequente Erweiterung des heutigen ESP eröffnet ESP II durch aktive Lenkregelfunktionen neue Dimensionen der Fahrdynamik und Fahrstabilität.

Weil der Ausfall der Lenkung den Verlust der Kontrolle über das Fahrzeug bedeutet, zählt die Lenkung ohnehin schon zu den sicherheitskritischsten Systemen im Kfz. Durch den Verzicht auf die mechanische Rückfallebene beim Lenksystem wird die Diskussion um die Zuverlässigkeit sicherheitskritischer, elektronischer Systeme im Kfz noch intensiver. Auf dem Weg zum Steer-by-Wire-System ist noch eine Reihe von komplexen Aufgaben, vor allem bezüglich der Fehlertoleranz, zu lösen.

### Elektronische Assistenten

### Brake-by-Wire


Elektronifizierung

Die Elektronifizierung des Automobils macht auch nicht vor Domänen Halt, in denen traditionell die Mechanik und Hydraulik dominieren. Um Fahrerassistenzfunktionen mit noch höherem Nutzen realisieren zu können, benötigt man **elektronische Schnittstellen zum Fahrwerk** vor allem zur Bremsanlage und zur Lenkung.

Solche elektronische Schnittstellen stellen beispielsweise die elektrohydraulische und die **elektromechanische Bremse** - EMB dar. Werden bei der elektrohydraulischen Bremse die Bremssättel noch hydraulisch betätigt, so erzeugen bei der elektromechanischen Bremse Elektromotoren die Bremskräfte direkt an den Rädern, gesteuert von einer elektronischen Regeleinheit, die ihren Input wiederum über ein elektronisches Bremspedal mit Pedalgefühlsimulator (Force Feedback) erhält. Die Übertragung der Steuer- und Sensorsignale erfolgt über Kommunikationsleitungen.

Brake-by-Wire

Durch ein solches **Brake-by-Wire-System** sind nicht nur individuelle Bremseingriffe an den einzelnen Rädern möglich, was die Bremsstabilität wesentlich verbessert. Möglich wird auch das Anpassen der Pedalcharakteristik und der Bremswirkung an den Fahrer einfach durch die bloße Änderung der Software. Schließlich erlaubt die Elektronik vor Ort eine verbesserte Diagnosefähigkeit und führt so zu einer erhöhten Betriebssicherheit. Ein sehr großes Potenzial eines Brake-by-Wire-Systems ist die Einbeziehung der Bremse in die Fahrdynamikregelung um die aktive Sicherheit erhöhen zu können.


![1706354006954](image/1706354006954.png)

So vielfältig das Potenzial von Brake-by-Wire-Systemen auch ist - sie stellen ein großes **Sicherheitsrisiko** dar. Schon die Störung oder der Ausfall einer einzelnen Systemkomponente kann schwerwiegende Folgen haben. Deshalb müssen Brake-by-Wire-Systeme **fehlertolerant** ausgelegt sein: nur so kann gewährleistet werden, dass bei Auftreten eines beliebigen Fehlers die gesetzlich vorgeschriebene Grundbremsfunktionalität erfüllt wird.

### Steer-by-Wire


Mechanische Lenkung

Die Lenksysteme heutiger Kraftfahrzeuge werden abhängig von den erforderlichen Lenkkräften mit hydraulischen, elektrohydraulischen oder elektrischen Lenkhilfen ausgerüstet. Unabhängig von der Art der Lenkunterstützung besitzen diese Systeme über die Lenksäule eine mechanische Verbindung zwischen Lenkrad und gelenkten Rädern, so dass auch bei Ausfall der Servounterstützung der mechanische Durchgriff weiter besteht.Elektrische Lenkung

Beim in der Grafik dargestellten elektrischen Lenksystem wird der Lenkeingriff des Autofahrers über eine Steuerleitung von einem Steuergerät entgegengenommen, verarbeitet und wieder über eine Steuerleitung als Stellbefehl an den Aktor übertragen und dort in eine Bewegung umgesetzt. An die Stelle der mechanischen Kopplung treten ein Aktor zur Positionierung der Räder (Radwinkelsteller) sowie ein Motor zur Simulation der Rückstellkräfte am Lenkrad (Handkraftaktor). Die Koordination zwischen Handkraftaktor und Radwinkelsteller übernimmt der Lenkungsregler. Die Lenksäule wird quasi durch Kommunikationsleitungen ersetzt, der Fahrer lenkt „by wire“.

Steer-by-Wire

Neben der Realisierung einer variablen Lenkunterstützung und Lenkübersetzung, die Möglichkeit einer individuellen Einstellung der Lenkcharakteristik steckt das größte Potenzial einer solchen Lenkung nach dem  **Steer-by-Wire** -**Prinzip** in der Einbeziehung der Lenkung in die Fahrdynamikregelung um die aktive Sicherheit erhöhen zu können. Als konsequente Erweiterung des heutigen ESP eröffnet ESP II durch aktive Lenkregelfunktionen neue Dimensionen der Fahrdynamik und Fahrstabilität.


![1706354036521](image/1706354036521.png)

Weil der Ausfall der Lenkung den Verlust der Kontrolle über das Fahrzeug bedeutet, zählt die Lenkung ohnehin schon zu den sicherheitskritischsten Systemen im Kfz. Durch den **Verzicht auf die mechanische Rückfallebene** beim Lenksystem wird die Diskussion um die Zuverlässigkeit sicherheitskritischer, elektronischer Systeme im Kfz noch intensiver. Auf dem Weg zum Steer-by-Wire-System ist noch eine Reihe von komplexen Aufgaben, vor allem bezüglich der  **Fehlertoleranz** , zu lösen.

### Sicherheit und Fehlertoleranz

Sicherheitsrisiko

So vielfältig das Potenzial von aktiven Sicherheits- und Fahrerassistenzfunktionen auch ist - sie stellen, und dies gilt vor allem für elektronische Systeme mit elektronischen Schnittstellen zum Fahrwerk, ein großes **Sicherheitsrisiko** dar. Schon die Störung oder der Ausfall einzelner Systemkomponenten kann schwerwiegende Folgen haben. Um die Sicherheit von by-Wire-Systemen zu garantieren wird versucht, durch Perfektionieren der Systemkomponenten, das Auftreten von Fehlern von vornherein zu vermeiden.

Fehlertoleranz

Treten dennoch Fehler auf, wird zusätzlich das Konzept der **Fehlertoleranz** genutzt um die spezifizierte Funktion des Gesamtsystems aufrechtzuerhalten. Fehlertoleranz erfordert zusätzliche Mittel um aufgetretene Fehler tolerieren zu können. Dabei kann zwischen der Informationsredundanz und der strukturellen Redundanz unterschieden werden. Im Kontext der Gewährleistung einer sicheren Datenkommunikation, kommt beiden Prinzipien große Bedeutung zu.

Redundanz

**Informationsredundanz** entsteht durch die Ergänzung der Nutzinformation durch zusätzliche Information z. B. zur Fehlererkennung und Fehlerkorrektur. Damit die durch die Systemspezifikation festgelegten Anwendungsfunktionen ausfallfrei bleiben, auch wenn in kommunikationsspezifischen Komponenten wie Busknoten Fehler im Rahmen der Fehlervorgabe auftreten, wird ein Kommunikationssystem um zusätzliche, für den Nutzbetrieb nicht notwendige Komponenten erweitert ( **strukturelle Redundanz** ).

Bei der Art der Aktivierung von Redundanz unterscheidet man grundsätzlich zwischen der  **statischen Redundanz** , die ständig aktiv ist, und der  **dynamischen Redundanz** , die erst fehlerbedingt aktiviert wird. Aufgrund der sehr hohen Anforderungen an die Echtzeitfähigkeit von verteilten sicherheitskritischen Systemen, kommt für dort eingesetzte Kommunikationssysteme nur das Prinzip der statischen Redundanz in Frage.


![1706354082565](image/1706354082565.png)

Redundanter Kommunikationskanal

Zur Minimierung des Sicherheitsrisikos gerade im Kontext von by-Wire-Systemen sieht man zusätzlich auch die **redundante Auslegung des Kommunikationskanals** vor, was aber unbedingt voraussetzt, dass auf beiden Kommunikationskanälen stets die gleichen Informationen übertragen werden. Nur so kann der Ausfall eines Kanals toleriert werden. Die Grafik „Strukturelle Redundanz“ zeigt die redundante Auslegung der Busknoten und des Kommunikationskanals eines Kommunikationssystems unter Zugrundelegung einer physikalischen Linientopologie.

Aktiver Sternkoppler

Auch die Entscheidung für eine bestimmte **physikalische Topologie** beeinflusst die Fehlertoleranz eines Kommunikationssystems. Wenn sich der Systemdesigner z.B. für eine aktive Sterntopologie entscheidet, dann besteht die Möglichkeit, die Ausbreitung von Fehlern zu vermeiden, indem fehlerhafte Kommunikationszweige vom aktiven Sternkoppler abgeschaltet werden.

![1706354094564](image/1706354094564.png)

### Zusammensetzbarkeit


Komplexität

Die zunehmende Verflechtung elektronischer Systeme und die vermehrte Substitution mechanischer durch elektronische Komponenten, erhöht die **Komplexität** elektronischer Systeme im Kfz und treibt so den Zeitaufwand und die Kosten für Tests und Systemintegration immer mehr in die Höhe. Abhilfe schaffen Architekturen, die die Eigenschaft der Zusammensetzbarkeit aufweisen.

Integration

**Zusammensetzbare Kommunikationsarchitekturen** ermöglichen es, dass sich Änderungen in der Funktion eines Steuergeräts nicht auf die Funktion anderer Steuergeräte bzw. auf die Funktion des Gesamtsystems auswirken. Das heißt, die Integration einer Systemkomponente macht den Test des Gesamtsystems nicht notwendig, da es ausreicht, ausschließlich die einzelnen Systemkomponenten verlässlich zu prüfen.

![1706354129860](image/1706354129860.png)

Zeitplan

Voraussetzung für eine zusammensetzbare [Kommunikationsarchitektur](https://elearning.vector.com/mod/page/view.php?id=231 "Kommunikationsarchitektur") ist ein  **Zeitplan** , der sich aus einer Anzahl von aufeinanderfolgenden **Zeitschlitzen** zusammensetzt, die jeweils den einzelnen Busknoten zugeordnet sind. Jedem Zeitschlitz ist eine bestimmte Botschaft zugeordnet und ist durch einen klar definierten Anfangs- und Endzeitpunkt gekennzeichnet.

Einen beispielhaften Kommunikationsablaufplan mitsamt der **Systemintegration** zeigt die Grafik „Systemintegration“. Dem Kommunikationsablaufplan zugrunde gelegt ist ein Kommunikationssystem, das sich aus den Busknoten A, B und C zusammensetzt. Wie aus der Grafik hervorgeht, ergibt sich bei der Systemintegration genau der im Kommunikationsablaufplan definierte Kommunikationsablauf, wenn sich die Hersteller von Busknoten an den vorgegebenen Kommunikationsablaufplan halten.

### Motivation für FlexRay

Determinismus und Fehlertoleranz

**Sicherheitskritische Fahrerassistenzfunktionen** mit elektronischen Schnittstellen zum Fahrwerk stellen höchste Anforderungen an die Zuverlässigkeit, Sicherheit und Echtzeitfähigkeit des Kommunikationssystems. Benötigt wird ein Kommunikationssystem mit der Eigenschaft der [Zusammensetzbarkeit](https://elearning.vector.com/mod/page/view.php?id=228 "Zusammensetzbarkeit"), dessen Kerneigenschaft es ist, eine buslastunabhängige **deterministische und fehlertolerante Datenkommunikation** zu gewährleisten.

CAN

Diesem anspruchsvollen Anforderungsbündel kann  **CAN (Controller Area Network)** , die im Kfz etablierte  **Kommunikationstechnologie** , nicht gerecht werden, da CAN auf einem **ereignisorientierten Kommunikationsansatz** basiert. Das bedeutet, dass jeder Busknoten eines Kommunikationssystems zu jedem Zeitpunkt auf das gemeinsame Kommunikationsmedium zugreifen kann. Der Einsatz von Techniken zur Auflösung von Kollisionen führt dazu, dass sich der Kommunikationsablauf erst zur Laufzeit ergibt. Ereignisgesteuerte Kommunikationssysteme ermöglichen die schnelle Reaktion auf asynchrone Vorgänge, sind jedoch  **nicht deterministisch** .

Weil die zeitliche Schnittstelle in einem ereignisgesteuerten Kommunikationssystem nicht definiert ist, wirkt sich das Hinzufügen und Entfernen von Busknoten auf den Kommunikationsablauf aus. Diese Auswirkungen machen streng genommen eine vollständig neue Validierung des Gesamtsystems erforderlich. Ereignisgesteuerte Kommunikationssysteme weisen **nicht** die Eigenschaft der **[Zusammensetzbarkeit](https://elearning.vector.com/mod/page/view.php?id=228 "Zusammensetzbarkeit")** auf.

Weil die CAN-Kommunikationstechnologie aufgrund fehlenden redundanten Strukturen und Mechanismen auch den hohen Anforderungen an die **Fehlertoleranz** **nicht** gerecht werden kann, zudem im Serieneinsatz lediglich mit einer maximalen Datenrate von 500 KBit/s aufwarten kann, experimentierten schon so manche Kfz-Hersteller in den 90er Jahren mit fehlertoleranten, zeitgesteuerten Kommunikationstechniken, die sehr hohe Datenraten zuließen.

### Anfänge von FlexRay

Allerdings ergaben die Untersuchungen und Erfahrungen bei den Kfz-Herstellern, dass keine der untersuchten Kommunikationstechniken allen Anforderungen für einen Serieneinsatz für zukünftige, sicherheitskritische Systeme in Kraftfahrzeugen gerecht werden könnte. Deshalb verabredeten **BMW und DaimlerChrysler** 1999 die Spezifikation und Entwicklung einer zukünftigen, einheitlichen, zeitgesteuerten und fehlertoleranten Kommunikationstechnik gemeinsam voranzutreiben. Als Ergebnis dieser Zusammenarbeit entstand die erste grobe Anforderungsspezifikation für  **FlexRay** .

### FlexRay Konsortium

Gründung

Ein wesentlicher Grund für den Erfolg von FlexRay war die Gründung des FlexRay Konsortiums, in dessen Rahmen sich im Jahre 2000 die beiden Kfz-Hersteller DaimlerChrysler und BMW sowie die beiden Chiphersteller Motorola und Philips zusammenschlossen.Ziel

Das Ziel des Konsortiums bestand in der Schaffung eines herstellerübergreifenden, deterministischen und fehlertoleranten Kommunikationsstandards, welchen jedes Mitglied des Konsortiums ohne die Zahlung von Lizenzgebühren nutzen kann.Einsatzgebiete

Als **Haupteinsatzgebiete** standen sicherheits- und zeitkritische Anwendungen im Automobil im Vordergrund. Ebenso intendierte man FlexRay aufgrund seiner Datenrate von 10 Mbit/s als Backbone im Automobil zu etablieren.Spezifikation

Nachdem das FlexRay Konsortium im Jahr 2010 die Spezifikation in der Version 3.0.1 veröffentlicht hatte, wurde mit der Überführung in einen ISO-Standard begonnen. Mittlerweile ist die **ISO 17458** verfügbar. Diese beschreibt das FlexRay Protokoll, die physikalische Schicht und Conformance Tests zu deren Überprüfung. Der vollständige Standard ist über die ISO verfügbar.

ISO

##### [Webseite der ISO - International Organization for Standardization](http://www.iso.org/)

## FlexRay Kommunikation

### Kommunikationsarchitektur

Ein FlexRay Kommunikationssystem ( **FlexRay Cluster** ) setzt sich aus einer Anzahl von **[FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten")** und einem, alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") verbindenden, physikalischen Übertragungsmedium ( **[FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus")** ) zusammen. Da die FlexRay Kommunikation nicht an eine bestimmte physikalische Topologie gebunden ist, können einem FlexRay Cluster **unterschiedliche physikalische Topologien** zugrunde liegen. Eine Punkt-zu-Punkt-Verbindung ist genauso möglich wie eine Linientopologie, eine passive Sterntopologie oder eine aktive Sterntopologie.


![1706355863204](image/1706355863204.png)

Zur Minimierung des Ausfallrisikos sieht FlexRay die **redundante Auslegung des Kommunikationskanals** vor. Jeder der beiden Kommunikationskanäle kann mit einer Datenrate von bis zu 10 MBit/s betrieben werden. Dieser redundante Kanal kann allerdings auch zur Erhöhung der Datenrate auf bis zu 20 MBit/s herangezogen werden. Die Wahl zwischen Fehlertoleranz und erhöhter Übertragungsrate lässt sich für jede einzelne FlexRay Botschaft treffen.


![1706355875812](image/1706355875812.png)

Dem FlexRay Cluster liegt eine **zeitgesteuerte Kommunikationsarchitektur** zugrunde, deren Kerneigenschaft die statische, zeitlich festgelegte Aktivierung von Aktionen im verteilten System darstellt. Das Prinzip der Zeitsteuerung ermöglicht nicht nur eine  **deterministische Datenkommunikation** , sondern auch die einfache **Zusammensetzung** eines Kommunikationssystems und die Realisierung von darauf aufbauenden Konzepten wie **Fehlertoleranz,** durch Kopplung von **Redundanzen** und zeitgleiches Aktivieren von Aktionen.

Zur Realisierung der Zeitsteuerung kommt das **TDMA-Verfahren** (Time Division Multiple Access) zum Einsatz, was bedeutet, dass die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") nicht wie bei CAN, unkontrolliert im Zuge von anwendungsbezogenen Ereignissen auf den Bus zugreifen dürfen. FlexRay Knoten müssen sich an einen exakt definierten **Kommunikationsablaufplan** halten, der jeder FlexRay Botschaft pro [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") einen bestimmten Zeitschlitz zuordnet und dadurch die Sendezeitpunkte sämtlicher FlexRay Botschaften vorgibt.

![1706355892333](image/1706355892333.png)


Einen beispielhaften Kommunikationsablaufplan mitsamt Kommunikationsablauf auf dem Kommunikationsmedium zeigt die Grafik „TDMA-Prinzip“. Dem Kommunikationsablaufplan liegt ein Kommunikationssystem zugrunde, das sich aus vier Busknoten zusammensetzt, wobei jeder Busknoten zwei Botschaften zu ganz bestimmten Zeitpunkten zu übertragen hat.

### Passive Topologien

Die FlexRay Kommunikation ist nicht an eine bestimmte physikalische Topologie gebunden. Eine einfache Punkt-zu-Punkt-Verbindung ist genauso möglich wie eine Linientopologie oder eine Sterntopologie. Zudem kann der Systemdesigner zwischen einer einkanaligen und einer zweikanaligen Kommunikation entscheiden.

![1706356021764](image/1706356021764.png)

Im Falle der **Punkt-zu-Punkt-Verbindung** werden zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") unmittelbar verbunden. Aus der Electrical Physical Layer Specification (EPL Specification) geht hervor, dass die Verbindung 24 Meter nicht überschreiten darf. Im Falle von drei FlexRay Knoten schließt man die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") über einen zentralen, aber passiven, Sternpunkt zusammen.

![1706356032979](image/1706356032979.png)

Man bezeichnet eine solche Topologie als  **passiven Stern** . Auch bei dieser physikalischen Topologie sind nicht mehr als 24 Meter zwischen zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") erlaubt. Mehr als 22 [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") sollten laut EPL Specification auch nicht zu einem passiven Stern zusammengeschlossen werden.

Ab vier [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") kann der Systemdesigner zwischen der passiven Sterntopologie und der Linientopologie wählen. Bei der **Linientopologie** werden die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") über separate Stichleitungen (Stubs) an den Bus angeschlossen. Die Grafik „Linientopologie mit redundantem Bus“ zeigt einen FlexRay Cluster, dem eine Linientopologie zugrunde liegt, bei der der Bus, also der Kommunikationskanal redundant ausgeführt ist, was heißt, dass Daten über Kanal A und B übertragen werden können.

![1706356043188](image/1706356043188.png)

Die FlexRay Spezifikation schreibt vor, beim Einsatz einer Linientopologie eine maximale Distanz zwischen zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") von 24 Metern nicht zu überschreiten, wenn die Kommunikationskanäle des FlexRay Clusters mit 10 MBit/s betrieben werden. Die Reduzierung der Datenrate ermöglicht die Vergrößerung der maximalen Distanz zwischen den beiden weitest entfernten [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten"). Laut FlexRay Spezifikation sollten an eine Linie nicht mehr als 22 [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") angeschlossen werden.

Genauso wie für die passive Sterntopologie gilt für die Linientopologie, dass aus der Sicht der Signalintegrität die Anzahl und Länge der Stichleitungen, wegen der zu erwartenden erheblichen Probleme mit der **elektromagnetischen Verträglichkeit,** zu begrenzen sind.

### Aktive Topologien


Anstatt passiv kann man die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") auch aktiv mithilfe eines **aktiven Sternkopplers** zusammenschließen: man ordnet die zu einem FlexRay Cluster zusammenzuschließenden [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") physikalisch zu einem Stern an und ersetzt den passiven Sternmittelpunkt (passiver Stern) durch einen aktiven Sternkoppler.

Ein aktiver Sternkoppler nimmt Signale über einen Kommunikationszweig auf, verstärkt und verteilt sie an alle anderen Kommunikationszweige. Außer bei Mischtopologien befindet sich am Ende eines Zweiges jeweils ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten"). Der maximale Abstand zwischen aktivem Sternkoppler und [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") darf **24 Meter** nicht überschreiten.

![1706356066355](image/1706356066355.png)

Der Vorteil der **aktiven Sterntopologie** besteht primär darin, die Ausbreitung von Fehlern zu vermeiden, indem fehlerhafte Kommunikationszweige vom aktiven Sternkoppler abgeschaltet werden. Von Vorteil ist aber auch die Möglichkeit, FlexRay Cluster mit größeren Ausdehnungen und, aufgrund idealer Busabschlüsse, elektrisch stabileren Verhältnissen realisieren zu können.

![1706356077377](image/1706356077377.png)

Die Grafik „Aktive Sterntopologie“ zeigt eine aktive Sterntopologie mit einem Kommunikationskanal. Die Grafik „Aktive Sterntopologie mit redundantem Bus“ zeigt dagegen eine aktive Sterntopologie mit einem redundanten Kommunikationskanal.

Berücksichtigt werden muss bei der Dimensionierung einer aktiven Clustertopologie, dass der aktive Sternkoppler die Signalübertragung verzögert. Aufgrund der sog. „Star Truncation“ muss zudem die Übertragung jeder FlexRay Botschaft mit einer sog. „Transmission Start Sequence (TSS)“ beginnen. Die „Star Truncation“ ist jene Zeit, die ein aktiver Sternkoppler benötigt, um in den aktiven Betriebszustand zu gelangen. Laut FlexRay Spezifikation dürfen 450 Nanosekunden nicht überschritten werden.

![1706356090274](image/1706356090274.png)

Die Ausdehnung eines FlexRay Clusters kann durch das **Hintereinanderschalten zweier aktiver Sternkoppler** um 24 Meter auf maximal 72 Meter erweitert werden. Die Sicherstellung der Signalintegrität allerdings lässt diese maximal erreichbare Netzwerkausdehnung wesentlich schrumpfen, so dass man in der Praxis eher von einer Netzwerkausdehnung von bis zu **3x12m** ausgehen sollte.

### FlexRay Knoten


Bei einem FlexRay Knoten handelt es sich um ein elektronisches Steuergerät, welches über eine FlexRay Schnittstelle an einen FlexRay Bus angeschlossen wird. Die **FlexRay Schnittstelle** umfasst einen Kommunikationscontroller und je nach Kanalanzahl einen oder zwei Bustreiber. Bezeichnet wird der Kommunikationscontroller als  **[FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** . Den Bustreiber bezeichnet man als  **FlexRay Transceiver** .


![1706356117777](image/1706356117777.png)

Der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") wickelt das in der FlexRay Spezifikation definierte **Kommunikationsprotokoll** ab. Zu den Hauptaufgaben des FlexRay Controllers zählen so in erster Linie das Framing, der Buszugriff, die Fehlererkennung und -behandlung, die Synchronisation, das Schlafenlegen und Aufwecken des FlexRay Busses sowie das Codieren von Sendebotschaften und das Decodieren von Empfangsbotschaften.

Der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") kann als Peripheriemodul eines Hosts ausgeführt werden. In diesem Fall spricht man von einem  **integrierten [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** . Der Vorteil eines integrierten FlexRay Controllers liegt in der einfacheren und schnelleren Kommunikation zwischen Host und FlexRay Controller. Dieser Lösung mangelt es allerdings an Flexibilität. Diese erhält man, wenn der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") vom Host baulich getrennt ist. In diesem Fall spricht man von einem  **stand-alone [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** .

![1706356127905](image/1706356127905.png)

Der **FlexRay Transceiver** koppelt den [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") an das physikalische Übertragungsmedium an. Die Hauptaufgabe des FlexRay Transceivers besteht in der Signaltransformation: einerseits setzt er den vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") empfangenen logischen Signalstrom in einen physikalischen Signalstrom um. Andererseits setzt er den empfangenden physikalischen Signalstrom in einen logischen Signalstrom um.

### FlexRay Controller


Der FlexRay Controller entlastet den Host bei sämtlichen Kommunikationsfunktionen. Mit dem Host ist der FlexRay Controller über das sog. **CHI** **(Controller Host Interface)** verbunden. In der CHI untergebracht sind frei konfigurierbare Puffer für Sende- und Empfangsbotschaften. Puffer für Empfangsbotschaften sind zusätzlich mit Akzeptanzfilter ausgestattet. In der CHI sind auch Status- und Steuerregister untergebracht.

![1706356191128](image/1706356191128.png)

Den Kern des FlexRay Controllers stellt die **Protocol Engine** dar. Sie setzt sich aus mehreren Kommunikationskomponenten zusammen. So sorgt die Komponente **Media Access Control (MAC)** für den Buszugriff. Die Komponente **Coding** übernimmt das Codieren der vom MAC erhaltenen Bytes. Die Komponente **Decoding** übernimmt das Decodieren des vom FlexRay Transceiver erhaltenen logischen Bitstroms.

![1706356203165](image/1706356203165.png)

Die Komponente **Frame & Symbol Processing (FSP)** überprüft die Einhaltung des dem FlexRay Cluster zugrunde gelegten [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") genauso wie die Empfangsbotschaften auf Übertragungsfehler. Für die Synchronisierung des FlexRay Knotens sorgt die Komponente  **Clock Synchronization Process** . Die Komponente **Wake Up & Start Up** kümmert sich um den Wake Up und Start Up.

![1706356213375](image/1706356213375.png)

Ein FlexRay Controller kann in Abhängigkeit des Kommunikationsfortschrittes acht unterschiedliche **Zustände** einnehmen. Jeder Controllerzustand ist durch bestimmte kommunikationsspezifische Tätigkeiten gekennzeichnet, bei denen ganz bestimmte Kommunikationskomponenten aktiv sind. Für die Controllerzustandsübergänge ist die Kommunikationskomponente **Protocol Operation Control (POC)** verantwortlich.

![1706356263908](image/1706356263908.png)


* Default Config
* Config
* Ready
* Wake-up
* Startup
* Normal Active
* Normal Passive
* Halt

### FlexRay Bus


Die FlexRay Technologie ist ausgelegt für Datenraten bis zu 10 MBit/s. Dies und der Verzicht auf kostenintensive geschirmte Leitungen stellen große Herausforderungen für die Sicherstellung elektromagnetischer Verträglichkeit dar. Das FlexRay Physical Layer definiert deswegen einige Maßnahmen, die Immunität gegenüber hochfrequenten Störfeldern und elektrostatischen Entladungen (ESD) zu erhöhen, sowie die Emission von Störungen zu reduzieren.


![1706356335850](image/1706356335850.png)

Die physikalische Signalübertragung im FlexRay Cluster basiert auf der Übertragung von  **Spannungsdifferenzen** . Durch Motoren, Zündanlagen und Schaltkontakte induzierte Störspannungen können so unschädlich gemacht werden. Die Emissionen halten sich wegen vergleichsweise geringer Differenzspannungen (2 Volt für den Buspegel „Data_1“, -2 Volt für den Buspegel „Data_0“) in Grenzen.

![1706356344153](image/1706356344153.png)

Wegen der Differenzsignalübertragung setzt sich der FlexRay Bus aus zwei Leitungen zusammen: **Bus Plus (BP)** und  **Bus Minus (BM)** . Das Verdrillen der beiden Leitungen sorgt für eine erhebliche Reduzierung des magnetischen Feldes, so dass in der Praxis üblicherweise verdrillte Leiterpaare zum Einsatz kommen, aus Kostengründen üblicherweise ohne Abschirmung.

Aufgrund der endlichen Signalausbreitungsgeschwindigkeit nimmt der Einfluss von Ausgleichsvorgängen ( **Reflexionen** ) mit steigender Datenrate oder wachsender Busausdehnung zu. Die **Terminierung** der Enden des Kommunikationskanals mittels Abschlusswiderstand verhindert in einem FlexRay Cluster Reflexionen.

Weil die FlexRay Spezifikation eine Last zwischen 40 und 55 Ohm vorschreibt, müssen die Busabschlusswiderstände folglich zwischen 80 und 110 Ohm liegen. In der Konsequenz sollte ein Kabel zur Übertragung eingesetzt werden, dessen Wellenwiderstand zwischen 80 und 110 Ohm liegt.

Anstatt die Enden des Kommunikationskanals mit jeweils einem einzelnen Busabschlusswiderstand zu versehen, können die Enden des FlexRay Busses auch mit einem **geteiltem Busabschluss** terminiert werden. Der geteilte Busabschluss wirkt wie ein Tiefpassfilter: ohne Beeinflussung der Gleichspannungsverhältnisse werden hochfrequente Signale gegen Masse kurzgeschlossen.

### FlexRay Buspegel


Die physikalische Signalübertragung in einem FlexRay Cluster basiert auf der Übertragung von Spannungsdifferenzen ( **Differenzsignalübertragung** ). Das Übertragungsmedium ( **[FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus")** ) setzt sich deswegen aus den beiden Leitungen „Bus Plus“ (BP) und „Bus Minus“ (BM) zusammen.

![1706356366721](image/1706356366721.png)

Die Electrical Physical Layer Specification definiert vier Buspegel, die entweder dem rezessiven oder dominanten Buszustand zuzuordnen sind. Der rezessive Buszustand ist durch eine Differenzspannung von Null Volt gekennzeichnet. Der dominante Buszustand dagegen durch eine Differenzspannung von ungleich Null Volt.

Sowohl der Buspegel „Idle“ als auch der Buspegel „Idle Low Power“ sind rezessiv. Der Buspegel **Idle** ist dadurch gekennzeichnet, dass beide Leitungen das Potenzial 2,5 Volt aufweisen und so die Differenzspannung 0 Volt beträgt. Der gültige Bereich für den Idle Buspegel befindet sich zwischen 1,8 Volt und 3,2 Volt.

Der Buspegel **Idle Low Power** stellt sich dann auf dem [FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus") ein, wenn sich alle FlexRay Transceiver im Low Power Mode befinden. Gekennzeichnet ist dieser Buspegel ebenfalls durch eine Differenzspannung von 0 Volt. Die Leitungen weisen dabei aber das Potenzial von 0 Volt auf. Der gültige Bereich befindet sich zwischen -0,2 Volt und 0,2 Volt.

![1706356377266](image/1706356377266.png)

Bei den beiden Buspegeln „Data_1“ und „Data_0“ handelt es sich um dominante Buspegel. Beim Buspegel **„Data_1“** weist die Busleitung BP ein Potenzial von 3,5 Volt, die Busleitung BM ein Potenzial von 1,5 Volt auf. Die Spannungsdifferenz beträgt folglich 2 Volt. Der Buspegel „Data_1“ repräsentiert die logische Eins.

Beim Buspegel **Data_0** weist die Busleitung BP ein Potenzial von 1,5 Volt, die Busleitung BM ein Potenzial von 3,5 Volt auf. Die Spannungsdifferenz beträgt folglich -2 Volt. Der Buspegel „Data_0“ repräsentiert die logische Null.

Aus der Grafik „FlexRay Buspegel“ gehen die Buszustände und Buspegel hervor. Angegeben sind auch die entsprechenden Spannungsschwellen für Sender und Empfänger.

### FlexRay Busankopplung


Es ist nicht möglich, einen [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") direkt mit dem physikalischen Übertragungsmedium zu verbinden, da auf diesem eine Differenzsignalübertragung stattfindet, der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") aber mit binären Signalen arbeitet. Benötigt wird eine  **physikalische Busankopplung** , die im Wesentlichen vom FlexRay Transceiver abgedeckt wird.

Der FlexRay Transceiver setzt den vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") empfangenen logischen Signalstrom in einen Differenzsignalstrom um. Den vom FlexRay Bus empfangenen physikalischen Differenzsignalstrom setzt er in einen logischen Signalstrom um.

Neben der Schnittstelle zum [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") besitzt der FlexRay Transceiver auch eine  **Schnittstelle zum Host** , die primär die beiden Steuerleitungen STBN (Standby) und EN (Enable Input) umfasst. Über diese beiden Steuerleitungen steuert der Host den FlexRay Transceiver, der prinzipiell **vier verschiedene Zustände** einnehmen kann: „Normal“, „Standby“, „Sleep“, „ReceiveOnly“. Die letzten beiden Zustände sind optional.

Ein wesentlicher Charakterzug eines FlexRay Transceivers ist seine besonders hohe  **elektromagnetische Verträglichkeit** . Trotzdem lassen sich durch den Einsatz von Entstördrosseln die Emissionen noch weiter reduzieren, wodurch Störungen anderer Elektroniksysteme weitgehend vermieden werden.

Der Einsatz von **LC-Entstörschaltungen** bei den FlexRay Transceivern, unterdrückt eventuelle, durch Schaltungsunsymmetrie hervorgerufene, Störströme durch die relativ hohe Impedanz der Entstördrossel. Zudem schließt der Tiefpassfilter, bestehend aus Kopplungskondensator der Split-Terminierung und einer Entstördrossel, hochfrequente Störungen gegen Masse kurz.

![1706356409119](image/1706356409119.png)

Obwohl Drosseln mit höherer Induktivität aufgrund ihrer höheren Dämpfung bessere Ergebnisse liefern, hat man im Hinblick auf die Signalintegrität die Streuinduktivität im Auge zu behalten. Die Electrical Physical Layer Specification schreibt folgende Werte für Entstördrosseln vor: Leitungswiderstand < 2 Ohm; Induktivität >50 μH und Streuinduktivität <1 μH.

Ein kleiner Nachteil der LC-Schaltung besteht darin, dass die Kombination aus Streuinduktivität und Kopplungskondensator einen Schwingkreis bildet, was im Zusammenhang mit den Schaltvorgängen des FlexRay Transceivers zu einem **Überschwingen** der Bussignale führt.

### Busguardian (BG)


Haupteinsatzgebiet von FlexRay sind äußerst sicherheits- und zeitkritische Anwendungen im Automobil. Die Organisation der Kommunikation im FlexRay Cluster in statische Kommunikationszyklen und die Verknüpfung von Zeitschlitzen mit [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") sorgen für einen reibungslosen  **deterministischen Kommunikationsablauf** . Außer Tritt geratene [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") können diese Harmonie stören, wenn sie unerlaubt innerhalb ihnen nicht zugeordneter Zeitschlitze senden. Dies zu verhindern ist die Aufgabe der sog. Busguardians.

Beim Konzept des **lokalen Busguardian** ist jedem FlexRay Transceiver ein Busguardian (BG) zugeordnet, der es dem FlexRay Transceiver nur dann erlaubt, die vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") empfangenen Daten auf den Bus durchzuschalten (wie das realisiert wird, geht aus der Grafik „Lokaler BG“ hervor), wenn es laut Kommunikationsplan auch vorgesehen ist.

![1706356436046](image/1706356436046.png)

Bei den Daten handelt es sich um die im statischen Kommunikationssegment reservierten Slots. Innerhalb des dynamischen Kommunikationssegments kann es einen solchen Schutz nicht geben, da die Botschaften bedarfsabhängig von den FlexRay Knoten gesendet werden. Es besteht lediglich die Möglichkeit, einem [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") das Senden im dynamischen Kommunikationssegment komplett zu erlauben oder komplett zu verbieten.

![1706356455613](image/1706356455613.png)

Zur Umsetzung seiner Funktion muss vorausgesetzt werden, dass der Busguardian den Kommunikationsplan und die Zeit im FlexRay Cluster kennt. Ideal ist es, wenn der Busguardian nicht auf der vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") erzeugten **lokalen Zeitbasis** aufsetzt, sondern diese unabhängig vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") erzeugt. Denn erst dadurch kann ein Busguardian sicherstellen, dass ein FlexRay Knoten nur in seinen Zeitschlitzen senden kann, weil zusätzlich zur Überprüfung der Zeitschlitze alle Fehler der Uhr des FlexRay Controllers festgestellt werden können.

![1706356467317](image/1706356467317.png)

Dazu muss der Busguardian allerdings mit fast denselben Funktionen wie der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") ausgestattet sein, was nach sich zieht, dass der Busguardian eine ähnliche Komplexität wie der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") erreicht und somit die Kosten für die FlexRay Kommunikation in die Höhe treibt. Unabhängig davon, wie ein Busguardian die Zeit gewinnt: bis dato liegen noch keine Implementierungen eines lokalen Busguardians vor. Die entsprechende Spezifikation **Node Local Bus Guardian Specification** liegt in der Version 2.0.9 vor; ihr Status ist vorläufig.

![1706356479552](image/1706356479552.png)

Dasselbe gilt für die **Central Bus Guardian Specification** in der Version 2.0.9. Auch sie ist vorläufig und bis dato liegen keine Implementierungen eines **zentralen Busguardians** vor. Dabei handelt es sich um ein Konzept, bei dem sich der Busguardian auf einem **aktiven Sternkoppler** befindet. Der zentrale Busguardian aktiviert innerhalb des [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") immer jenen Kommunikationszweig, an dessen Ende jener [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") angeschlossen ist, der laut Kommunikationsplan senden darf. So können Signalkollisionen ausgeschlossen werden.

## FlexRay Buszugriff

### Prinzip des Buszugriffs


In einem FlexRay Cluster wird den [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") auf zwei unterschiedliche Arten der Zugang zum Kommunikationsmedium gewährt: zum einen über das **TDMA-Verfahren** (Time Division Multiple Access) und zum anderen über das **FTDMA-Verfahren** (Flexible Time Division Multiple Access), dessen Kern das TDMA-Verfahren darstellt.

![1706356507935](image/1706356507935.png)

Dem **TDMA-Verfahren** liegt ein **Kommunikationsplan** zugrunde, der sich in eine Anzahl von gleich langen Zeitschlitzen ( **statische Slots** ) gliedert, denen jeweils ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") zugeordnet ist. Während des Kommunikationsbetriebs wird den [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") der Zugang zum Kommunikationsmedium (Bus) dem Zeitplan nach gewährt: vom ersten bis zum letzten statischen Slot erhalten die den statischen Slots zugeordneten [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") den  **exklusiven Zugang zum Bus** , um die den statischen Slots zugeordneten Botschaften übertragen zu können.

![1706356518873](image/1706356518873.png)

Der Kommunikationsplan wird während des Kommunikationsbetriebs von allen [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") **zyklisch** abgearbeitet, so dass alle statische Botschaften mit vorgegebener Periode, also **deterministisch** übertragen werden. Der Kommunikationsplan definiert folglich nichts anderes als einen [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus"), genauer gesagt den  **FlexRay [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus")** .

Für **asynchrone Vorgänge** bzw. für die **sporadische Übertragung** von Botschaften ist das TDMA-Verfahren nicht ideal. Deshalb bietet die FlexRay Technologie die Option, den Zyklus um ein **[dynamisches Segment](https://elearning.vector.com/mod/page/view.php?id=244 "Dynamisches Segment")** zu erweitern, falls in einem FlexRay Cluster Botschaften nicht nur in einem festen Zeitraster übertragen werden sollen, sondern auch bedarfsorientiert.

Der [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") setzt sich dann aus einem statischen und einem dynamischen Segment zusammen. Damit trotz Gewährleistung einer dynamischen Botschaftsübertragung die **deterministische Datenkommunikation** im statischen Segment sichergestellt wird, weist das dynamische Segment ebenfalls eine feste zeitliche Länge auf.

Dem dynamischen Segment liegt das **FTDMA-Verfahren** zugrunde, welches sich vom TDMA-Verfahren darin unterscheidet, dass die im Kommunikationsplan definierten **dynamischen Botschaften** von den entsprechenden [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") bei Bedarf übertragen werden können. Das heißt, der Zeitpunkt der Botschaftsübertragung ist nicht vorhersehbar. Weil das dynamische Segment eine endliche Länge hat, kann es sogar vorkommen, dass sendewillige [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") ihre dynamische Botschaft gar nicht übertragen können.

### Kommunikationszyklus


Die Datenkommunikation in einem FlexRay Cluster erfolgt zyklisch auf der Basis eines Zeitplans. Der **Kommunikationszyklus** setzt sich aus mindestens zwei Zeitsegmenten zusammen, dem **statischen Segment** und dem Segment  **Network Idle Time (NIT)** . Das statische Segment dient der deterministischen Übertragung von Botschaften. Das NIT-Segment wird zur Synchronisierung der lokalen Uhren benötigt. Während des NIT-Segments findet keine Datenkommunikation statt.

![1706356537981](image/1706356537981.png)

Optional kann der Kommunikationszyklus um das **dynamische Zeitsegment** und um ein **Symbol Window** erweitert werden. Das dynamische Zeitsegment dient der bedarfsorientierten Botschaftsübertragung und folgt im Bedarfsfall stets dem statischen Segment. Das Symbol Window dient zur Übertragung von Symbolen. Über das Collision Avoidance Symbol zeigt ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") den Start des ersten Kommunikationszyklus an. Das Media Test Symbol kommt beim Test eines Busguardians und das WakeUp Symbol zum Wecken des FlexRay Clusters zum Einsatz.

![1706356549825](image/1706356549825.png)

Weil nur das statische Segment und das NIT-Segment zwingend für einen Zyklus sind, können vier **Zyklusvarianten** unterschieden werden. Die Grafik „Kommunikationszyklus“ zeigt einen Zyklus, der alle Zeitsegmente aufweist: [statisches Segment](https://elearning.vector.com/mod/page/view.php?id=242 "Statisches Segment"), dynamisches Segment, Symbol Window und NIT.

![1706356560108](image/1706356560108.png)

Ein Kommunikationszyklus setzt sich aus einer definierten Anzahl von **Makroticks** zusammen, die den einzelnen Segmenten zugeordnet sind. Gebildet werden die Makroticks aus einer Anzahl von  **Mikroticks** , der kleinsten Zeiteinheit lokaler Uhren. Aufgrund unterschiedlichen Quarzfrequenzen und folglich unterschiedlich langen Mikroticks können sich die Makroticks verschiedener [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") aus unterschiedlich vielen Mikroticks zusammensetzen.

### Statisches Segment


Dem statischen Segment kommt innerhalb des FlexRay [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") eine herausragende Rolle zu: es stellt die für verteilt realisierte Regelungen so wichtige **äquidistante Datenübertragung** sicher. Garantiert wird dies durch das, dem statischen Segment zugrunde liegende,  **TDMA-Verfahren** .

Dieses sieht die Gliederung des statischen Segments in eine Anzahl gleich langer Zeitschlitze ( **statische Slots** ) vor. Die den statischen Slots zugeordneten [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") können während des zyklischen Kommunikationsbetriebs die, den statischen Slots zugeordneten, **statischen Botschaften** übertragen. Vorausgesetzt werden dabei synchronisierte  **lokale Zähler** , die jeweils zu Beginn eines statischen Slots inkrementiert werden. Der Zählerwert korrespondiert mit einer statischen Botschaft und einem [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten").

Die Grafik „Statisches Segment“ zeigt einen Kommunikationsplan für zwei Kanäle ( **Kanal A und Kanal B** ). Im ersten Slot wird dieselbe Botschaft übertragen. Der Ausfall eines Kanals führt somit nicht dazu, dass die Botschaft nicht übertragen wird. Allerdings kann der redundante Kommunikationskanal anstatt zur Erhöhung der Fehlertoleranz auch zur Erhöhung der Datenrate herangezogen werden. Genau dieser Ansatz wird in den weiteren Slots des statischen Segments verfolgt: auf beiden Kanälen werden unterschiedliche Botschaften übertragen. Die Wahl zwischen Fehlertoleranz und erhöhter Datenrate lässt sich für jede einzelne FlexRay Botschaft treffen.

![1706356586852](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/mccat/OneDrive/Doing/EE-Automotive/BUSSYSTEME/image/1706356586852.png)

Maximal können bis zu 1023 statische Slots definiert werden. Weil zur Generierung der globalen Zeitbasis mindestens zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") erforderlich sind, muss das statische Segment mindestens zwei statische Slots umfassen.

### Statischer Slot



Eine reibungslose deterministische Botschaftsübertragung während des statischen Segments setzt voraus, dass der statische Slot lang genug ist. Bestimmt wird die Länge des statischen Slots primär durch die längste  **FlexRay Botschaft** . Grundsätzlich setzt sich eine FlexRay Botschaft aus Header, Payload, Trailer und Steuerzeichen zusammen. Berücksichtigt werden muss auch der sog.  **Channel Idle Delimiter** , welcher das Ende einer FlexRay Botschaft anzeigt.

![1706356612866](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/mccat/OneDrive/Doing/EE-Automotive/BUSSYSTEME/image/1706356612866.png)

Einfluss auf die Länge des statischen Slots nehmen aber auch die größtmögliche  **Signalverzögerung** , erlaubt sind maximal 2,5 Mikrosekunden, und die größtmögliche Zeitabweichung, die zwei beliebige [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") trotz Synchronisation aufweisen können ( **Präzision** ).

Ein statischer Slot setzt sich aus vier Zeitsegmenten zusammen. Dadurch wird sichergestellt, dass eine Botschaft innerhalb des entsprechenden statischen Slots empfangen werden kann, selbst bei maximaler Signalverzögerung und wenn [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") mit einem maximal vorlaufenden und mit einem maximal nachlaufenden lokalen Zeitgeber beteiligt sind.

![1706356623578](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/mccat/OneDrive/Doing/EE-Automotive/BUSSYSTEME/image/1706356623578.png)

Gestartet wird jeder statische Slot mit einem Offset, dem sog.  **Action Point Offset** . Diese Bezeichnung leitet sich aus dem sog. **Action Point** ab, jener Zeitpunkt, zu dem die Botschaftsübertragung beginnt. Dem Action Point Offset folgen der Action Point und die Botschaftsübertragung. Nach der Botschaftsübertragung, im Anschluss an den Channel Idle Delimiter (11 rezessive Bits), folgt eine Pause ( **Channel Idle** ), deren Dauer logischerweise dem Action Point Offset entspricht. Eine weitere Grafik verdeutlicht diesen Aufbau eines statischen Slots.

Es ist offensichtlich, dass die Präzision und die Signalverzögerung zur maximal erzielbaren Datenrate im FlexRay Cluster umgekehrt proportional zueinander sind: mit zunehmend schlechteren lokalen Taktgebern bzw. größer werdender Signalverzögerung, muss die Zeitspanne zwischen Slotbeginn und Action Point vergrößert werden, was schließlich die maximal erzielbare Datenrate reduziert.


### Dynamisches Segment



Das dynamische Segment ist optional. Es dient der Übertragung **bedarfsorientierter Botschaften** und unterstützt so  **asynchrone Vorgänge** . Um die deterministische Datenübertragung im statischen Segment nicht zu beeinflussen, weist das dynamische Zeitsegment immer die gleiche Länge auf. Das dynamische Zeitsegment folgt im Bedarfsfall stets auf das statische Segment.

![1706357087498](image/1706357087498.png)

Dem dynamischen Segment liegt das **FTDMA-Verfahren** (Flexible Time Division Multiple Access) zugrunde, dessen Kern zwar das TDMA-Verfahren darstellt, aber trotzdem einen flexiblen Kommunikationsablauf ermöglicht. Der Kommunikation im dynamischen Segment liegt deshalb auch ein **Kommunikationsplan** zugrunde. Die darin definierten dynamischen Botschaften werden aber nur dann im dynamischen Segment übertragen, wenn es dazu einen Bedarf gibt.

Das dynamische Segment beginnt damit, dass alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") ihre **lokalen Zähler** inkrementieren. Der Zählerwert korrespondiert mit einer **dynamischen Botschaft** und einem [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten"). Wenn für die zum Zählerwert korrespondierende dynamische Botschaft keine Sendeanforderung beim entsprechenden FlexRay Knoten vorliegt, dann inkrementieren die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") ihre Zähler nach der Länge eines  **Minislots** . Der **dynamische Slot** ist in diesem Fall genau ein Minislot lang.

Liegt dagegen eine Sendeanforderung vor, dann überträgt der entsprechende [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") die zum Zählerwert korrespondierende dynamische Botschaft. Dem dynamischen Slot folgt wieder ein Minislot, was dazu führt, dass die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") ihre Zähler inkrementieren. Liegt eine Sendeanforderung zum neuen Zählerwert vor, wird die zum Zählerwert gehörende dynamische Botschaft übertragen. Ist dies nicht der Fall, folgt sofort der nächste Minislot.

Dieses Vorgehen wiederholt sich solange, bis das dynamische Segment für die Übertragung einer dynamischen Botschaft nicht mehr lang genug ist. In diesem Fall findet bis zum Ende des dynamischen Segments keine Datenübertragung mehr statt. Für nicht übertragene dynamische Botschaften steht prinzipiell der nächste Zyklus zur Verfügung. Ihnen steht eine interaktive Grafik zur Verfügung um sich die Datenübertragung im dynamischen Segment klar zu machen. Lesen Sie sich die Anleitung durch, damit Sie die gesamte Funktionalität nutzen können.

Offensichtlich besteht zwischen dem Zählerwert, der einer dynamischen Botschaft zugeordnet ist, und der Übertragungswahrscheinlichkeit ein Zusammenhang: je höher der Zählerwert, desto unwahrscheinlicher die Botschaftsübertragung. Geschlossen werden kann, das jene Botschaft, die dem ersten Minislot des dynamischen Segments bzw. dem niedrigsten Zählerwert zugeordnet ist, die höchste **Priorität** besitzt.

Der Systemdesigner muss schließlich sicherstellen, dass auch dynamische Botschaften mit niedriger Priorität übertragen werden können – zumindest, wenn sonst kein anderer Bedarf mit höherer Priorität vorliegt. Der Systemdesigner hat auch darauf zu achten, dass die Übertragung der längsten dynamischen Botschaft möglich ist.


### Dynamischer Slot


Für die Bemessung eines dynamischen Slots gelten im Grunde die gleichen Bedingungen wie für die Bemessung eines statischen Slots. Deswegen ist ein dynamischer Slot ähnlich aufgebaut wie ein [statischer Slot](https://elearning.vector.com/mod/page/view.php?id=243 "Statischer Slot"). Jeder dynamische Slot beginnt mit dem sog.  **Action Point Offset** . Dieser Offset endet am  **Action Point** , jenem Zeitpunkt, zu dem die Übertragung einer dynamischen Botschaft beginnt. Dieser Action Point entspricht dem Action Point des  **Minislots** .

![1706357107075](image/1706357107075.png)

Dem Action Point Offset folgen der Action Point und die Botschaftsübertragung. Diese ist dadurch gekennzeichnet, dass man im dynamischen Segment Botschaften mit **unterschiedlich großem Payload** übertragen darf. Der Botschaftsübertragung folgt der  **Channel Idle Delimiter** , der sich wie auch im statischen Slot aus elf rezessiven Bits zusammensetzt.

Beachtet werden muss, dass laut FlexRay Spezifikation eine dynamische Botschaft genau mit dem nächstmöglichen Action Point zu enden hat. Um dies zu garantieren, wird die Botschaftsübertragung um die sog. **Dynamic Trailing Sequence** verlängert. Theoretisch kann diese Sequenz maximal einen Minislot lang sein.

### Demonstration


Zur weiteren Veranschaulichung des **hybriden Buszugriffsverfahrens** und der damit korrespondierenden Datenübertragung wird ein FlexRay Cluster definiert, welcher sich aus fünf **[FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten")** zusammensetzt ([FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") A bis E). Sämtliche [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") sind, wie aus der Grafik „Demo-Cluster“ hervorgeht, physikalisch mittels einer **Linie** verbunden. Zur Minimierung des Ausfallrisikos ist der Kommunikationskanal **redundant** ausgelegt. Zur Datenübertragung stehen somit zwei Kanäle zur Verfügung,  **Kanal A und Kanal B** .

![1706357160298](image/1706357160298.png)

Der, der Datenübertragung zugrunde liegende, **Kommunikationsplan** ist in ein **statisches und [dynamisches Segment](https://elearning.vector.com/mod/page/view.php?id=244 "Dynamisches Segment")** unterteilt. Beide Segmente umfassen fünf  **Slots** . Im statischen Segment sind die  **statischen Botschaften** , im dynamischen Segment die **dynamischen Botschaften** aufgeführt.

Während des **Kommunikationsbetriebs** werden alle im statischen Segment definierten statischen Botschaften stets dem Kommunikationsplan nach übertragen. Die im dynamischen Segment definierten dynamischen Botschaften werden aber nur dann übertragen, wenn es dazu einen Bedarf gibt.

Ihnen stehen sowohl eine interaktive Grafik als auch eine Animation zur Verfügung, um sich mit der Datenkommunikation im FlexRay Cluster vertraut zu machen. Die interaktive Grafik beleuchtet die Kommunikationstechnik im dynamischen Segment. Mit der Animation haben Sie die Möglichkeit, sich mit der Kommunikation sowohl im statischen als auch dynamischen Segment zu beschäftigen. Lesen Sie sich die jeweiligen Anleitungen durch, damit Sie die gesamte Funktionalität der Medienobjekte nutzen können.

## FlexRay Framing

### Frame Header


Die Datenübertragung in einem FlexRay Cluster erfolgt mithilfe eines einheitlichen Botschaftsrahmens (FlexRay Botschaft). Jede **FlexRay Botschaft** setzt sich aus drei Teilen zusammen:  **Header** , **Payload** und  **Trailer ** . Der Header setzt sich aus 40 Bits zusammen. Davon gehören elf Bit zum Identifier (ID). Dieser kennzeichnet eine Botschaft und korrespondiert mit einem Slot. Alle IDs können frei genutzt werden. Ausgenommen ist der ID=0x00, dieser dient der Kennzeichnung von ungültigen Botschaften.

Dem ID vorangestellt sind  **vier Indikatorbits** , denen wiederum ein reserviertes Bit vorausgeht. Die Indikatorbits dienen zur näheren Spezifizierung einer Botschaft. Der **Payload Preamble Indicator** zeigt an, ob im Payload einer statischen Botschaft ein **Network Management Vector** bzw. im Payload einer dynamischen Botschaft ein **Message Identifier** übertragen wird.

![1706357222021](image/1706357222021.png)

In besonderen Fällen kann der Sender die Payload einer Botschaft ausschließlich mit Nullen übertragen. Dabei handelt es sich dann um keinen regulären Payload. Um anzeigen zu können, ob der Payload regulär oder ungültig ist, existiert der  **Null Frame Indicator** . Der **Sync Frame Indicator** gibt an, ob die im statischen Segment übertragene Botschaft als **Sync Frame** im Rahmen der Synchronisation verwendet wird. Der **Startup Frame Indicator** gibt an, ob die im statischen Segment übertragene Botschaft als **Startup Frame** im Rahmen des Startup verwendet wird.

Dem Identifier folgt die  **Payload Length** . Sie zeigt die Größe des Payloads in Words an und umfasst 7 Bits. Insgesamt lassen sich mit einer Botschaft 254 Nutzbytes übertragen. Gesichert wird der Identifier mittels  **CRC-Verfahren** . Dabei wird auf der Basis des Identifiers, der Payload Length, des Sync Frame Indicators und des Startup Frame Indicators und einem, durch die FlexRay Spezifikation definierten, Generatorpolynoms eine elf Bit lange **Header CRC Sequence** berechnet, die dann auf die Payload Length folgt.

Abgeschlossen wird der Header durch den  **Cycle Counter** . Dieser setzt sich aus sechs Bits zusammen und repräsentiert die Nummer des Zyklus, in dem die Botschaft gesendet wird. Der Cycle Counter zählt stets bis 63.

### Frame Payload


Maximal können mit einer Botschaft 254 Nutzbytes ( **Payload** ) transportiert werden. Der Parameter **Payload Length** zeigt die Größe des Payloads in Words an. Die Payload Length weist bei allen im statischen Segment übertragenen Botschaften denselben Wert auf. Diesen muss der Systemdesigner während der Konfigurationsphase festlegen. Da **dynamische Botschaften** nicht an eine feste Payloadgröße gebunden sind, kann der Payload Length für solche Botschaften unterschiedliche Werte annehmen.

Bei einer im **statischen Segment** übertragenen Botschaft besteht die Möglichkeit, die ersten zwölf Nutzbytes für die Übertragung des **Network Management Vector** zu verwenden. Dazu muss der im Header übertragene **Payload Preamble Indicator** gesetzt werden. Der Network Management Vector steht für die Realisierung des Netzmanagements in einem FlexRay Cluster zur Verfügung.

Wenn der Payload Preamble Indicator bei einer **dynamischen FlexRay Botschaft** gesetzt ist, dann zeigt dies nicht an, dass der Payload mit einem Network Management Vector startet. Bei einer dynamischen Botschaft wird angezeigt, dass es sich bei den ersten beiden Nutzbytes um den **Message Identifier** handelt. Mithilfe des Message Identifiers steht dem Systemdesigner eine Möglichkeit zur Verfügung, den Payload näher zu spezifizieren, als mögliche Basis für eine differenziertere Akzeptanzfilterung.

![1706357242957](image/1706357242957.png)

In besonderen Fällen kann der Sender den Payload einer Botschaft ausschließlich mit Nullen übertragen. Ein solcher Fall liegt dann vor, wenn ein [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") dem Kommunikationsplan nach eine statische Botschaft übertragen muss, aber der mit der Botschaft korrespondierende Puffer vom Host gesperrt ist. Dies kann z.B. auftreten, wenn der Host in diesem Moment selbst auf diesen Puffer zugreift. Weil der FlexRay Controller nicht auf die Daten im Puffer zugreifen kann, überträgt er die statische Botschaft automatisch als  **Nullframe** . Dabei weist der **Null Frame Indicator** im Header der Botschaft den Wert „Null“ auf.

Zur Sicherung des Payloads kommt das **CRC-Verfahren** (CRC: Cyclic Redundancy Check), ein sehr leistungsstarkes Fehlererkennungsverfahren, zum Einsatz. Im Rahmen des CRC-Verfahrens wird auf der Basis des Headers und Payloads und einem, durch die FlexRay Spezifikation definierten, **Generatorpolynoms** eine **CRC-Sequenz** berechnet, die dem Header und Payload als **Trailer** angehängt wird.

Die Checksumme entspricht dann dem Vielfachen des Headers und des Payloads. Der Empfänger der Botschaft erkennt mit sehr hoher Sicherheit einen Übertragungsfehler. Ein Fehler wird dann festgestellt, wenn die Division durch das Generatorpolynom einen Rest ergibt. Bei einer Payload bis zu 248 Bytes garantiert das CRC-Verfahren eine  **Hamming-Distanz von sechs** , für eine größere Payload liegt die Hamming-Distanz bei vier, was zu einer geringeren Fehlererkennungsfähigkeit führt.

### Codierung


Die physikalische Übertragung einer Botschaft beginnt nicht mit dem ersten Bit des Frame Headers, sondern mit der sog.  **Transmission Start Sequence (TSS)** . Dies um zu verhindern, dass in einem FlexRay Cluster, dem eine **aktive Sterntopologie** zugrunde liegt, die ersten Bits einer Botschaft vom **aktiven Sternkoppler** nicht vom Empfangs- zu den Sendezweigen transportiert werden können.

![1706357267376](image/1706357267376.png)

Dies liegt darin begründet, dass ein aktiver Sternkoppler eine gewisse Zeit benötigt, um in den aktiven Betriebszustand zu gelangen ( **Star Truncation** ). In einem FlexRay Cluster mit einem aktiven Sternkoppler muss die TSS mindestens der Star Truncation entsprechen: mindestens 3 und maximal 15 Bits Low Pegel.

Abgeschlossen wird die TSS mit der sog.  **Frame Start Sequence (FSS)** . Im Anschluss an die FSS kann die Übertragung des Headers erfolgen. Dabei ist zu berücksichtigen, dass jedem zu übertragenden Byte eine sog. **Byte Start Sequence (BSS)** vorangestellt wird. Der durch diese Sequenz entstehende Flankenwechsel nutzt der Empfänger für die Nachsynchronisation. Das Ende einer Botschaft markiert die sog.  **Frame End Sequence (FES)** .

![1706357280161](image/1706357280161.png)

Sowohl im statischen auch als im dynamischen Slot zeigen elf rezessive Bits ( **Channel Idle Delimiter** ) an, dass das Kommunikationsmedium wieder frei ist. Da laut FlexRay Spezifikation eine dynamische Botschaft genau mit dem nächstmöglichen Action Point zu enden hat, wird die Botschaftsübertragung um die sog. **Dynamic Trailing Sequence** verlängert. Diese stellt sicher, dass jeder Empfänger den Minislot bestimmen kann, in dem die dynamische Botschaft endete.

Zur Veranschaulichung der Codierung von Botschaften stehen Ihnen zwei Grafiken zur Verfügung. Die Grafik „Statische Botschaft“ zeigt eine statische Botschaft unter Berücksichtigung der zur physikalischen Übertragung notwendigen Codeelemente. Die Grafik „Dynamische Botschaft“ zeigt eine dynamische Botschaft ebenfalls unter Berücksichtigung der zur physikalischen Übertragung notwendigen Codeelemente.

## FlexRay Synchronisation

### Synchronisationsprinzip


Der reibungslose Ablauf der Datenkommunikation in einem FlexRay Cluster setzt voraus, dass alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") **das gleiche Zeitverständnis** haben, weil alle Aktivitäten des Kommunikationssystems durch das Erreichen bestimmter Punkte im Zeitablauf ausgelöst werden.

![1706357307158](image/1706357307158.png)

Sichergestellt werden muss in einem FlexRay Cluster, dass aus der Sicht aller FlexRay Knoten alle Kommunikationszyklen immer zum selben Zeitpunkt beginnen und gleich lang sind. Genauso muss garantiert werden, dass alle statischen Slots der [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") immer an der gleichen Stelle innerhalb des Zyklus beginnen.

Voraussetzung dafür ist ein  **globales Zeitverständnis** . Weil ein FlexRay Cluster auf einer **Multi-Master-Architektur** basiert, kann ein solches globales Zeitverständnis nur auf der Basis der lokalen Zeitbasen kooperativ hergestellt werden. Dies stellt eine große Herausforderung dar, weil **Frequenztoleranzen** und Toleranzen der passiven Bauelemente in der Quarzbeschaltung bei identischer Nennfrequenz für **unterschiedliche Frequenzen und Phasen** sorgen.

![1706357318801](image/1706357318801.png)

Der FlexRay Spezifikation kann entnommen werden, dass die lokalen Taktgeber über die gesamte Lebensdauer eines Fahrzeugs eine maximale Frequenzabweichung von 1500 ppm nicht überschreiten sollten. Diese Frequenzabweichung trägt erstens Sorge, dass man über eine Laufzeit von zehn Jahren mit Quarztoleranzen von etwa 250 ppm rechnen muss. Zweitens muss man wissen, dass die passiven Bauelemente in der Quarz-Beschaltung in ähnlicher Höhe zur Frequenzabweichung beitragen. Drittens fließt in die maximal erlaubte Frequenzabweichung von 1500 ppm ein ausreichend großer Sicherheitsfaktor ein.

Es ist offensichtlich, dass ohne regelmäßiges Stellen der lokalen Zeitbasen keine netzwerkweite Zeitbasis hergestellt werden kann. Die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") verwenden einen speziellen Algorithmus um ihre lokalen Uhren so zu korrigieren, dass alle lokalen Uhren im FlexRay Cluster bis auf eine definierte Abweichung zu einer globalen Uhr synchron laufen. Hierzu kommen zwei Verfahren zum Einsatz: **Phasen- bzw. Offsetkorrektur** und  **Frequenz- bzw. Steigungskorrektur** .

### Phasen- und Frequenzkorrektur


Die **Phasenkorrektur** sorgt dafür, dass die lokalen Uhren der [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") dieselbe Phase besitzen und so die Kommunikationszyklen stets zeitgleich beginnen. Ohne weitere Korrekturmaßnahmen muss bei der Systemauslegung stets die maximale Abweichung der lokalen Takte zugrunde gelegt werden.

Dies hieße, bei einer maximalen Abweichung zweier lokaler Uhren von 3000 ppm und einer Zyklusdauer von beispielsweise 10 Millisekunden kämen am Ende des Zyklus 30 Mikrosekunden Drift zusammen, was die maximal mögliche Datenrate erheblich reduzieren würde.

![1706357345004](image/1706357345004.png)

Eine Verbesserung der Bandbreiteneffizienz zeitgesteuerter Kommunikationssysteme erreicht man durch den zusätzlichen Einsatz der  **Frequenzkorrektur** . Während die Phasenkorrektur lediglich die Symptome der Frequenzabweichung behandelt, setzt die Frequenzkorrektur an der Ursache für die Frequenzabweichung an.

Dies ist allerdings gar nicht so einfach, weil die Frequenz eines Quarzes nicht direkt beeinflusst werden kann. Deswegen kommt ein Frequenzteiler ins Spiel, der die Quarzfrequenz in die lokale Zeitbasis des FlexRay Knotens umsetzt. Durch die Änderung des Teilverhältnisses können die lokalen Uhren beschleunigt oder gebremst werden, so dass schließlich die Kommunikationszyklen für alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") gleich lang sind.

Weil durch die Frequenzkorrektur alle lokalen Uhren nahezu mit der gleichen Geschwindigkeit laufen, bleiben trotz transienter Störungen der, zur Synchronisation erforderlichen, Synchronisationsbotschaften über mehrere Kommunikationszyklen hinweg, die Abweichungen der lokalen Uhren innerhalb definierbarer Grenzen. Der Einsatz der Frequenzkorrektur macht die Uhrensynchronisation in einem FlexRay Cluster äußerst robust gegenüber transienter Störungen. Der Ausfall der Uhrensynchronisation kann über mehrere Kommunikationszyklen hinweg toleriert werden.

### Synchronisationsmethode


Die Synchronisation lokaler Uhren in einem FlexRay Cluster basiert darauf, dass jedem [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") die **Sende- und Empfangszeitpunkte** aller **statischen Botschaften** von vornherein bekannt sind. Damit sind alle Knoten eines FlexRay Clusters in der Lage sowohl den **Offset** als auch die **Steigung** so zu korrigieren, dass schon nach wenigen Zyklen alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") jeden [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") zum selben Zeitpunkt mit dem gleichen Takt beginnen.

In einem FlexRay Cluster fungieren mindestens 2 und maximal 15 [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") als **Sync-Knoten** bzw. **Sync Node** (Synchronisationsknoten), die pro Zyklus eine **Sync-Botschaft** (Synchronisationsbotschaft) in einem definierten **statischen Slot** übertragen. Dabei handelt es sich um keine zusätzlichen Botschaften, sondern um statische Botschaften, bei denen der **Sync Frame Indicator** gesetzt ist.

![1706357368420](image/1706357368420.png)

Alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") vergleichen die a priori bekannten Zeitpunkte mit den Zeitpunkten, zu denen die Sync-Botschaften real eintreffen. Sie erstellen dann eine sortierte Liste von Differenzen, aus denen sie mit dem **Fault Tolerant Midpoint (FTM) Algorithmus** ihren **Offsetkorrekturwert** errechnen.

Der FTM-Algorithmus sieht vor, dass die Extremwerte aus der Liste getilgt werden, damit stark abweichende lokale Uhren die Kommunikation im FlexRay Cluster nicht aus dem Tritt bringen. Bei bis zu sieben Sync-Knoten werden Minimum und Maximum gestrichen. Bei mehr als sieben Sync-Knoten fallen auch die zweitgrößten und zweitkleinsten Messwerte heraus.

Die verbleibenden Messwerte werden addiert und gemittelt - das Ergebnis stellt den Offsetkorrekturwert dar. Die Ermittlung des **Steigungskorrekturwertes** läuft identisch ab, nur mit dem Unterschied, dass die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") die, den Sync-Botschaften zugrunde liegenden, Zykluslängen messen.

![1706357386908](image/1706357386908.png)

Sowohl die Offset- als auch die Steigungskorrektur erfolgt auf der Basis der lokalen Uhren, deren kleinste Einheit der **Mikrotick** darstellt. Einen **Offset** gleicht ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") durch das Hinzufügen oder Weglassen einer, dem Offset entsprechenden, Anzahl von Mikroticks in der NIT am Ende jedes ungeraden Zyklus aus. Dadurch verschiebt ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") den eigenen Start des nächsten Zyklus und passt sich so an die anderen [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") an.

Damit die **Steigungskorrektur** nicht wie eine Offsetkorrektur wirkt, verteilt ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") die dem Steigungskorrekturwert entsprechende Anzahl von Mikroticks gleichmäßig über den folgenden geraden und ungeraden Zyklus. So ist jeder [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") in der Lage, seinen Zyklus entweder zu verkürzen oder zu verlängern.
