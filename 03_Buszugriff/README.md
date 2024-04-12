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
