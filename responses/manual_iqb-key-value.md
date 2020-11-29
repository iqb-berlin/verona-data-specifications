# Simples Antwortformat "iqb-key-value"

Die Verona-Schnittstelle für Player sieht vor, dass die Antwortdaten aufgeteilt 
geschickt werden können. Jedes Teilstück (sog. data chunk) wird über einen Schlüssel
(string) identifiziert.

Ein data chunk ist ein utf-8-string-serialisiertes JSON-Dictionary, also eine Schlüssel-Wert-Liste. 
Sowohl Schlüssel als auch Wert ist stets im string-Format gespeichert. Beispiel:
```
{
	"canvasElement25":"-1",
	"canvasElement26":"-1",
	"canvasElement16":"femal elephant",
	"canvasElement17":"1m",
	"canvasElement18":"80kg",
	"canvasElement19":"zoo keeper",
	"canvasElement20":"stut up",
	"canvasElement21":"between",
	"canvasElement22":"true"
}
```

Die Schlüssel-Daten sind im Format nicht bestimmt. Insbesondere ist folgendes
zu beachten:
* Unterformulare könnten im Schlüssel durch angehängte Suffixe kodiert sein
* die Werte von mehreren Schlüssel-Wert-Paaren könnten zusammen eine Antwort
darstellen, z. B: bei Radio-Button-Groups
* Nicht vorhandene Schlüssel müssen nicht bedeuten, dass es hierzu keine Antwort gab

Die Werte-Daten sind im Format nicht bestimmt. Insbesondere ist folgendes
zu beachten:
* Ein Boolscher Wert "Wahr" könnte definiert sein als "T", "t", "1", "true", "True" 
usw.
* Numerische Werte könnten eine Exponentialschreibweise haben.
* Datums- und Zeitwerte könnten normalisiert sein, eine Zeitzone enthalten oder eine 
Vormittags-/Nachmittagsmarkierung

Bei diesem offenen Format ist also zusätzliches Wissen für eine sinnvolle Verarbeitung
erforderlich. Wie dieses in die nachfolgenden Schritte gelangt, ist offen.
