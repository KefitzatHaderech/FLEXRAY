# FlexRay

Dieses Repository enthält Informationen und Erklärungen zum FlexRay. Es bietet Einblicke in die Funktionsweise, die Protokolle und die Technologien hinter diesem Netzwerk. FlexRay steht für "Flexible Ray" und ist ein Kommunikationsprotokoll, das speziell für den Einsatz in der Antriebsdomäne der Fahrzeugnetzwerken entwickelt wurde. Es ermöglicht eine zuverlässige und deterministische Datenübertragung in Echtzeit zwischen verschiedenen elektronischen Steuergeräten in modernen Fahrzeugen. FlexRay wurde entwickelt, um den steigenden Anforderungen an die Kommunikation in Fahrzeugen gerecht zu werden, insbesondere im Hinblick auf Sicherheit, Zuverlässigkeit und Bandbreitenanforderungen in komplexen automobilen Systemen.

## Inhaltsverzeichnis

1. [🔍 Einführung](#Einfuehrung)
   * 1.1. Elektronische Assistenten
   * 1.2. Brake-by-Wire
   * 1.3. Steer-by-Wire
   * 1.4. Sicherheit und Fehlertoleranz
   * 1.5. Zusammensetzbarkeit
   * 1.6. Motivation für FlexRay
   * 1.7. Anfänge von FlexRay
   * 1.8. FlexRay Konsortium
   * 1.8.1. Webseite der ISO - International Organization for Standardization
2. [📡 FlexRay Kommunikation](#flexray-kommunikation)
   * 2.1. Kommunikationsarchitektur
   * 2.2. Passive Topologien
   * 2.3. Aktive Topologien
   * 2.4. FlexRay Knoten
   * 2.5. FlexRay Controller
   * 2.6. FlexRay Bus
   * 2.7. FlexRay Buspegel
   * 2.8. FlexRay Busankopplung
   * 2.9. Busguardian BG
3. [🔓 FlexRay Buszugriff](#flexray-buszugriff)
   * 3.1. Prinzip des Buszugriffs
   * 3.2. Kommunikationszyklus
   * 3.3. Statisches Segment
   * 3.4. Statischer Slot
   * 3.5. Dynamisches Segment
   * 3.6. Dynamischer Slot
   * 3.7. Demonstration
4. [🖼️ FlexRay Framing](#flexray-framing)
   * 4.1. Frame Header
   * 4.2. Frame Payload
   * 4.3. Codierung
5. [🔄 FlexRay Synchronisation](#flexray-synchronisation)
   * 5.1. Synchronisationsprinzip
   * 5.2. Phasen- und Frequenzkorrektur
   * 5.3. Synchronisationsmethode
