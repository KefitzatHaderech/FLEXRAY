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
