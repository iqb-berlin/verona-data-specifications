[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

English version [see below](#english)

# IQB-Definitionen für Verona-Daten

In diesem Repository sind alle Datenformate beschrieben, die das IQB im Zusammenhang 
mit Verona-Anwendungen nutzt. Verona steht hier für eine Initiative zur Spezifizierung 
von Schnittstellen, die im computerbasierten Testen genutzt werden können. Weitere 
Informationen zu Verona-Schnittstellen [hier](https://github.com/verona-interfaces/introduction).

## Unit-Definitionen
Die Fragen eines Tests werden üblicherweise gruppiert. Obwohl auch eine Frage einzeln
auf einer Seite präsentiert werden kann, nimmt man oft mehrere Fragen, die inhaltlich 
eine Einheit bilden, zusammen. Diese sogenannte Unit kann man mit einer Aufgabe 
vergleichen, die mehrere Teilaufgaben hat.

Der Verona-Ansatz sieht vor, dass ein Testsystem jeweils die Daten einer Unit lädt 
und dann eine dazu passende Komponente zur Präsentation wählt (den sog. Player). Folgende 
Datentypen verwendet das IQB für seine Player:

* [iqb-scripted](unit-defs/manual_iqb-scripted.md): Die Unit-Definition besteht aus einem Script. 
Diese Folge von Anweisungen ist eine einfache Text-Datei, die in einem Texteditor bearbeitet
werden kann oder aus einem Hilfsprogramm automatisiert erzeugt wird. Es gibt keine Vorschriften zur 
Verarbeitung der Antworten (richtig/falsch usw.). Dieses Format wird vorrangig für 
Befragungen genutzt (z. B. Evaluationen oder Protokolle von Testsitzungen).

## Player-Antwortdaten  
Während der Durchführung eines Tests oder einer Befragung gibt der Player die 
Antwortdaten an das Testsystem zur Speicherung. Die Spezifikation dieser 
Antwortdaten ist wichtig, um nachfolgend eine korrekte Datenverarbeitung (Kodierung,
Analyse) zu gewährleisten:
* [iqb-key-value](responses/manual_iqb-key-value.md): Dieses JSON-Format ordnet Antworten als String einem
für die Unit eindeutigen Schlüssel (ebenfalls vom Typ string) zu. Da dieses Format kaum Festlegungen
enthält, ist es zwar universell, aber erst mit vielen Zusatzinformationen aus dem 
Erhebungszusammenhang sinnvoll zu verarbeiten.


# <a name="english"></a>IQB Verona Data Specifications
Verona interfaces are specifications concerning computer based assessment. You can learn 
more about this German initiative [here](https://github.com/verona-interfaces/introduction).

The IQB uses these interface specs for it's own applications. One important feature of these 
Verona interfaces is the black box approach for data exchange. Although the 
applications communicate via well defined channels, the structure of the transferred 
data is unknown. Only the name and version of data specification is needed to select 
the matching component.  

Nevertheless, every producer of data should document data structures. For the IQB, we 
do this in this repository. The manuals are in German language, because most of the 
people involved in data supply and processing welcome this language very much.
