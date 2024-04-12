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
