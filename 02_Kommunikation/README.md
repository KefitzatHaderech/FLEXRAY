# FlexRay Kommunikation

## Kommunikationsarchitektur

Ein FlexRay Kommunikationssystem ( **FlexRay Cluster** ) setzt sich aus einer Anzahl von **[FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten")** und einem, alle [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") verbindenden, physikalischen Übertragungsmedium ( **[FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus")** ) zusammen. Da die FlexRay Kommunikation nicht an eine bestimmte physikalische Topologie gebunden ist, können einem FlexRay Cluster **unterschiedliche physikalische Topologien** zugrunde liegen. Eine Punkt-zu-Punkt-Verbindung ist genauso möglich wie eine Linientopologie, eine passive Sterntopologie oder eine aktive Sterntopologie.

![1706355863204](image/1706355863204.png)

Zur Minimierung des Ausfallrisikos sieht FlexRay die **redundante Auslegung des Kommunikationskanals** vor. Jeder der beiden Kommunikationskanäle kann mit einer Datenrate von bis zu 10 MBit/s betrieben werden. Dieser redundante Kanal kann allerdings auch zur Erhöhung der Datenrate auf bis zu 20 MBit/s herangezogen werden. Die Wahl zwischen Fehlertoleranz und erhöhter Übertragungsrate lässt sich für jede einzelne FlexRay Botschaft treffen.

![1706355875812](image/1706355875812.png)

Dem FlexRay Cluster liegt eine **zeitgesteuerte Kommunikationsarchitektur** zugrunde, deren Kerneigenschaft die statische, zeitlich festgelegte Aktivierung von Aktionen im verteilten System darstellt. Das Prinzip der Zeitsteuerung ermöglicht nicht nur eine  **deterministische Datenkommunikation** , sondern auch die einfache **Zusammensetzung** eines Kommunikationssystems und die Realisierung von darauf aufbauenden Konzepten wie **Fehlertoleranz,** durch Kopplung von **Redundanzen** und zeitgleiches Aktivieren von Aktionen.

Zur Realisierung der Zeitsteuerung kommt das **TDMA-Verfahren** (Time Division Multiple Access) zum Einsatz, was bedeutet, dass die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") nicht wie bei CAN, unkontrolliert im Zuge von anwendungsbezogenen Ereignissen auf den Bus zugreifen dürfen. FlexRay Knoten müssen sich an einen exakt definierten **Kommunikationsablaufplan** halten, der jeder FlexRay Botschaft pro [Kommunikationszyklus](https://elearning.vector.com/mod/page/view.php?id=241 "Kommunikationszyklus") einen bestimmten Zeitschlitz zuordnet und dadurch die Sendezeitpunkte sämtlicher FlexRay Botschaften vorgibt.

![1706355892333](image/1706355892333.png)

Einen beispielhaften Kommunikationsablaufplan mitsamt Kommunikationsablauf auf dem Kommunikationsmedium zeigt die Grafik „TDMA-Prinzip“. Dem Kommunikationsablaufplan liegt ein Kommunikationssystem zugrunde, das sich aus vier Busknoten zusammensetzt, wobei jeder Busknoten zwei Botschaften zu ganz bestimmten Zeitpunkten zu übertragen hat.

## Passive Topologien

Die FlexRay Kommunikation ist nicht an eine bestimmte physikalische Topologie gebunden. Eine einfache Punkt-zu-Punkt-Verbindung ist genauso möglich wie eine Linientopologie oder eine Sterntopologie. Zudem kann der Systemdesigner zwischen einer einkanaligen und einer zweikanaligen Kommunikation entscheiden.

![1706356021764](image/1706356021764.png)

Im Falle der **Punkt-zu-Punkt-Verbindung** werden zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") unmittelbar verbunden. Aus der Electrical Physical Layer Specification (EPL Specification) geht hervor, dass die Verbindung 24 Meter nicht überschreiten darf. Im Falle von drei FlexRay Knoten schließt man die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") über einen zentralen, aber passiven, Sternpunkt zusammen.

![1706356032979](image/1706356032979.png)

Man bezeichnet eine solche Topologie als  **passiven Stern** . Auch bei dieser physikalischen Topologie sind nicht mehr als 24 Meter zwischen zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") erlaubt. Mehr als 22 [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") sollten laut EPL Specification auch nicht zu einem passiven Stern zusammengeschlossen werden.

Ab vier [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") kann der Systemdesigner zwischen der passiven Sterntopologie und der Linientopologie wählen. Bei der **Linientopologie** werden die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") über separate Stichleitungen (Stubs) an den Bus angeschlossen. Die Grafik „Linientopologie mit redundantem Bus“ zeigt einen FlexRay Cluster, dem eine Linientopologie zugrunde liegt, bei der der Bus, also der Kommunikationskanal redundant ausgeführt ist, was heißt, dass Daten über Kanal A und B übertragen werden können.

![1706356043188](image/1706356043188.png)

Die FlexRay Spezifikation schreibt vor, beim Einsatz einer Linientopologie eine maximale Distanz zwischen zwei [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") von 24 Metern nicht zu überschreiten, wenn die Kommunikationskanäle des FlexRay Clusters mit 10 MBit/s betrieben werden. Die Reduzierung der Datenrate ermöglicht die Vergrößerung der maximalen Distanz zwischen den beiden weitest entfernten [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten"). Laut FlexRay Spezifikation sollten an eine Linie nicht mehr als 22 [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") angeschlossen werden.

Genauso wie für die passive Sterntopologie gilt für die Linientopologie, dass aus der Sicht der Signalintegrität die Anzahl und Länge der Stichleitungen, wegen der zu erwartenden erheblichen Probleme mit der **elektromagnetischen Verträglichkeit,** zu begrenzen sind.

## Aktive Topologien

Anstatt passiv kann man die [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") auch aktiv mithilfe eines **aktiven Sternkopplers** zusammenschließen: man ordnet die zu einem FlexRay Cluster zusammenzuschließenden [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") physikalisch zu einem Stern an und ersetzt den passiven Sternmittelpunkt (passiver Stern) durch einen aktiven Sternkoppler.

Ein aktiver Sternkoppler nimmt Signale über einen Kommunikationszweig auf, verstärkt und verteilt sie an alle anderen Kommunikationszweige. Außer bei Mischtopologien befindet sich am Ende eines Zweiges jeweils ein [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten"). Der maximale Abstand zwischen aktivem Sternkoppler und [FlexRay Knoten](https://elearning.vector.com/mod/page/view.php?id=234 "FlexRay Knoten") darf **24 Meter** nicht überschreiten.

![1706356066355](image/1706356066355.png)

Der Vorteil der **aktiven Sterntopologie** besteht primär darin, die Ausbreitung von Fehlern zu vermeiden, indem fehlerhafte Kommunikationszweige vom aktiven Sternkoppler abgeschaltet werden. Von Vorteil ist aber auch die Möglichkeit, FlexRay Cluster mit größeren Ausdehnungen und, aufgrund idealer Busabschlüsse, elektrisch stabileren Verhältnissen realisieren zu können.

![1706356077377](image/1706356077377.png)

Die Grafik „Aktive Sterntopologie“ zeigt eine aktive Sterntopologie mit einem Kommunikationskanal. Die Grafik „Aktive Sterntopologie mit redundantem Bus“ zeigt dagegen eine aktive Sterntopologie mit einem redundanten Kommunikationskanal.

Berücksichtigt werden muss bei der Dimensionierung einer aktiven Clustertopologie, dass der aktive Sternkoppler die Signalübertragung verzögert. Aufgrund der sog. „Star Truncation“ muss zudem die Übertragung jeder FlexRay Botschaft mit einer sog. „Transmission Start Sequence (TSS)“ beginnen. Die „Star Truncation“ ist jene Zeit, die ein aktiver Sternkoppler benötigt, um in den aktiven Betriebszustand zu gelangen. Laut FlexRay Spezifikation dürfen 450 Nanosekunden nicht überschritten werden.

![1706356090274](image/1706356090274.png)

Die Ausdehnung eines FlexRay Clusters kann durch das **Hintereinanderschalten zweier aktiver Sternkoppler** um 24 Meter auf maximal 72 Meter erweitert werden. Die Sicherstellung der Signalintegrität allerdings lässt diese maximal erreichbare Netzwerkausdehnung wesentlich schrumpfen, so dass man in der Praxis eher von einer Netzwerkausdehnung von bis zu **3x12m** ausgehen sollte.

## FlexRay Knoten

Bei einem FlexRay Knoten handelt es sich um ein elektronisches Steuergerät, welches über eine FlexRay Schnittstelle an einen FlexRay Bus angeschlossen wird. Die **FlexRay Schnittstelle** umfasst einen Kommunikationscontroller und je nach Kanalanzahl einen oder zwei Bustreiber. Bezeichnet wird der Kommunikationscontroller als  **[FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** . Den Bustreiber bezeichnet man als  **FlexRay Transceiver** .

![1706356117777](image/1706356117777.png)

Der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") wickelt das in der FlexRay Spezifikation definierte **Kommunikationsprotokoll** ab. Zu den Hauptaufgaben des FlexRay Controllers zählen so in erster Linie das Framing, der Buszugriff, die Fehlererkennung und -behandlung, die Synchronisation, das Schlafenlegen und Aufwecken des FlexRay Busses sowie das Codieren von Sendebotschaften und das Decodieren von Empfangsbotschaften.

Der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") kann als Peripheriemodul eines Hosts ausgeführt werden. In diesem Fall spricht man von einem  **integrierten [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** . Der Vorteil eines integrierten FlexRay Controllers liegt in der einfacheren und schnelleren Kommunikation zwischen Host und FlexRay Controller. Dieser Lösung mangelt es allerdings an Flexibilität. Diese erhält man, wenn der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") vom Host baulich getrennt ist. In diesem Fall spricht man von einem  **stand-alone [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller")** .

![1706356127905](image/1706356127905.png)

Der **FlexRay Transceiver** koppelt den [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") an das physikalische Übertragungsmedium an. Die Hauptaufgabe des FlexRay Transceivers besteht in der Signaltransformation: einerseits setzt er den vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") empfangenen logischen Signalstrom in einen physikalischen Signalstrom um. Andererseits setzt er den empfangenden physikalischen Signalstrom in einen logischen Signalstrom um.

## FlexRay Controller

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

## FlexRay Bus

Die FlexRay Technologie ist ausgelegt für Datenraten bis zu 10 MBit/s. Dies und der Verzicht auf kostenintensive geschirmte Leitungen stellen große Herausforderungen für die Sicherstellung elektromagnetischer Verträglichkeit dar. Das FlexRay Physical Layer definiert deswegen einige Maßnahmen, die Immunität gegenüber hochfrequenten Störfeldern und elektrostatischen Entladungen (ESD) zu erhöhen, sowie die Emission von Störungen zu reduzieren.

![1706356335850](image/1706356335850.png)

Die physikalische Signalübertragung im FlexRay Cluster basiert auf der Übertragung von  **Spannungsdifferenzen** . Durch Motoren, Zündanlagen und Schaltkontakte induzierte Störspannungen können so unschädlich gemacht werden. Die Emissionen halten sich wegen vergleichsweise geringer Differenzspannungen (2 Volt für den Buspegel „Data_1“, -2 Volt für den Buspegel „Data_0“) in Grenzen.

![1706356344153](image/1706356344153.png)

Wegen der Differenzsignalübertragung setzt sich der FlexRay Bus aus zwei Leitungen zusammen: **Bus Plus (BP)** und  **Bus Minus (BM)** . Das Verdrillen der beiden Leitungen sorgt für eine erhebliche Reduzierung des magnetischen Feldes, so dass in der Praxis üblicherweise verdrillte Leiterpaare zum Einsatz kommen, aus Kostengründen üblicherweise ohne Abschirmung.

Aufgrund der endlichen Signalausbreitungsgeschwindigkeit nimmt der Einfluss von Ausgleichsvorgängen ( **Reflexionen** ) mit steigender Datenrate oder wachsender Busausdehnung zu. Die **Terminierung** der Enden des Kommunikationskanals mittels Abschlusswiderstand verhindert in einem FlexRay Cluster Reflexionen.

Weil die FlexRay Spezifikation eine Last zwischen 40 und 55 Ohm vorschreibt, müssen die Busabschlusswiderstände folglich zwischen 80 und 110 Ohm liegen. In der Konsequenz sollte ein Kabel zur Übertragung eingesetzt werden, dessen Wellenwiderstand zwischen 80 und 110 Ohm liegt.

Anstatt die Enden des Kommunikationskanals mit jeweils einem einzelnen Busabschlusswiderstand zu versehen, können die Enden des FlexRay Busses auch mit einem **geteiltem Busabschluss** terminiert werden. Der geteilte Busabschluss wirkt wie ein Tiefpassfilter: ohne Beeinflussung der Gleichspannungsverhältnisse werden hochfrequente Signale gegen Masse kurzgeschlossen.

## FlexRay Buspegel

Die physikalische Signalübertragung in einem FlexRay Cluster basiert auf der Übertragung von Spannungsdifferenzen ( **Differenzsignalübertragung** ). Das Übertragungsmedium ( **[FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus")** ) setzt sich deswegen aus den beiden Leitungen „Bus Plus“ (BP) und „Bus Minus“ (BM) zusammen.

![1706356366721](image/1706356366721.png)

Die Electrical Physical Layer Specification definiert vier Buspegel, die entweder dem rezessiven oder dominanten Buszustand zuzuordnen sind. Der rezessive Buszustand ist durch eine Differenzspannung von Null Volt gekennzeichnet. Der dominante Buszustand dagegen durch eine Differenzspannung von ungleich Null Volt.

Sowohl der Buspegel „Idle“ als auch der Buspegel „Idle Low Power“ sind rezessiv. Der Buspegel **Idle** ist dadurch gekennzeichnet, dass beide Leitungen das Potenzial 2,5 Volt aufweisen und so die Differenzspannung 0 Volt beträgt. Der gültige Bereich für den Idle Buspegel befindet sich zwischen 1,8 Volt und 3,2 Volt.

Der Buspegel **Idle Low Power** stellt sich dann auf dem [FlexRay Bus](https://elearning.vector.com/mod/page/view.php?id=236 "FlexRay Bus") ein, wenn sich alle FlexRay Transceiver im Low Power Mode befinden. Gekennzeichnet ist dieser Buspegel ebenfalls durch eine Differenzspannung von 0 Volt. Die Leitungen weisen dabei aber das Potenzial von 0 Volt auf. Der gültige Bereich befindet sich zwischen -0,2 Volt und 0,2 Volt.

![1706356377266](image/1706356377266.png)

Bei den beiden Buspegeln „Data_1“ und „Data_0“ handelt es sich um dominante Buspegel. Beim Buspegel **„Data_1“** weist die Busleitung BP ein Potenzial von 3,5 Volt, die Busleitung BM ein Potenzial von 1,5 Volt auf. Die Spannungsdifferenz beträgt folglich 2 Volt. Der Buspegel „Data_1“ repräsentiert die logische Eins.

Beim Buspegel **Data_0** weist die Busleitung BP ein Potenzial von 1,5 Volt, die Busleitung BM ein Potenzial von 3,5 Volt auf. Die Spannungsdifferenz beträgt folglich -2 Volt. Der Buspegel „Data_0“ repräsentiert die logische Null.

Aus der Grafik „FlexRay Buspegel“ gehen die Buszustände und Buspegel hervor. Angegeben sind auch die entsprechenden Spannungsschwellen für Sender und Empfänger.

## FlexRay Busankopplung

Es ist nicht möglich, einen [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") direkt mit dem physikalischen Übertragungsmedium zu verbinden, da auf diesem eine Differenzsignalübertragung stattfindet, der [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") aber mit binären Signalen arbeitet. Benötigt wird eine  **physikalische Busankopplung** , die im Wesentlichen vom FlexRay Transceiver abgedeckt wird.

Der FlexRay Transceiver setzt den vom [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") empfangenen logischen Signalstrom in einen Differenzsignalstrom um. Den vom FlexRay Bus empfangenen physikalischen Differenzsignalstrom setzt er in einen logischen Signalstrom um.

Neben der Schnittstelle zum [FlexRay Controller](https://elearning.vector.com/mod/page/view.php?id=235 "FlexRay Controller") besitzt der FlexRay Transceiver auch eine  **Schnittstelle zum Host** , die primär die beiden Steuerleitungen STBN (Standby) und EN (Enable Input) umfasst. Über diese beiden Steuerleitungen steuert der Host den FlexRay Transceiver, der prinzipiell **vier verschiedene Zustände** einnehmen kann: „Normal“, „Standby“, „Sleep“, „ReceiveOnly“. Die letzten beiden Zustände sind optional.

Ein wesentlicher Charakterzug eines FlexRay Transceivers ist seine besonders hohe  **elektromagnetische Verträglichkeit** . Trotzdem lassen sich durch den Einsatz von Entstördrosseln die Emissionen noch weiter reduzieren, wodurch Störungen anderer Elektroniksysteme weitgehend vermieden werden.

Der Einsatz von **LC-Entstörschaltungen** bei den FlexRay Transceivern, unterdrückt eventuelle, durch Schaltungsunsymmetrie hervorgerufene, Störströme durch die relativ hohe Impedanz der Entstördrossel. Zudem schließt der Tiefpassfilter, bestehend aus Kopplungskondensator der Split-Terminierung und einer Entstördrossel, hochfrequente Störungen gegen Masse kurz.

![1706356409119](image/1706356409119.png)

Obwohl Drosseln mit höherer Induktivität aufgrund ihrer höheren Dämpfung bessere Ergebnisse liefern, hat man im Hinblick auf die Signalintegrität die Streuinduktivität im Auge zu behalten. Die Electrical Physical Layer Specification schreibt folgende Werte für Entstördrosseln vor: Leitungswiderstand < 2 Ohm; Induktivität >50 μH und Streuinduktivität <1 μH.

Ein kleiner Nachteil der LC-Schaltung besteht darin, dass die Kombination aus Streuinduktivität und Kopplungskondensator einen Schwingkreis bildet, was im Zusammenhang mit den Schaltvorgängen des FlexRay Transceivers zu einem **Überschwingen** der Bussignale führt.

## Busguardian (BG)

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
