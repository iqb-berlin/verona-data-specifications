# IQB-Standardformat für Antworten
*version 1.0.0*

Als Antworten bezeichnen wir die Daten, die durch die Interaktion der Testperson mit dem Testsystem entstehen und als Zustände zum Ende der Bearbeitung gespeichert werden. Antworten absolvieren einen Verarbeitungsprozess vom Ursprung (sog. Basisvariable, Rohdaten-Wert) über Ableitung, Cleaning, Kodierung bis zur Bewertung. Die Daten, die nach der Aufbereitung für die Datenanalyse bereitgestellt werden (z. B. IRT-/Rasch-Analyse), nennen wir Primärdaten.

Die zweite Art von Daten, die aus der Interaktion mit dem Testsystem resultieren, sind Log-Daten. Diese beschreiben nicht Zustände zum Ende der Bearbeitung, sondern beschreiben Veränderungen während der Bearbeitung. Sie können zu weiteren Variablen führen, die jedoch nicht Teil der hier beschriebenen Datenstruktur sind.

Jede Antwort wird mit der folgenden JSON-Datenstruktur abgespeichert. Wenn eine Software-Komponente das Datenformat definieren soll (z. B. im Player als Teil der Verona-Spezifikation), dann wird das Schlüsselwort 'iqb-standard' gefolgt von der Version in SemVer-Notation verwendet, also z. B. `iqb-standard@1.0.0`.

```
{
    id: string,
    status: string,
    value: any,
    code?: number,
    score?: number
}
```
## id
Mit dieser Kennung wird die Antwort einer Variablen zugeordnet.

## status
#### Variablen aus dem Testsystem/Player
| Wert | Bedeutung | Beschreibung |
| :------------- | :------------- | :------------- |
| `NOT_REACHED`* | Nicht erreicht | Die Testperson ist noch nicht zu der Stelle gelangt, an der eine Interaktion möglich ist. |
| `DISPLAYED`* | Gezeigt | Der Testperson ist eine Interaktion möglich. |
| `VALUE_CHANGED` | Wert geändert | Die Testperson hat eine Antwort gegeben. |

#### Abgeleitete Variablen

| Wert | Bedeutung | Beschreibung |
| :------------- | :------------- | :------------- |
| `VALUE_DERIVED` | Erfolgreich abgeleitet | Alle Werte für die Ableitung lagen im korrekten Format vor und die Ableitung ist abgeschlossen. |
| `SOURCE_MISSING`* | Quellwert(e) nicht verfügbar | Einer oder mehrere Quellen für die Ableitung liegen nicht vor. Als Status zulässig<ul><li>für Wert: VALUE_CHANGED, VALUE_DERIVED oder ein CODING-Status</li><li>für Code/Score muss CODING_COMPLETE gesetzt sein</li></ul> |
| `DERIVE_ERROR` | Ableitungsfehler | Die Ableitungsoperation war fehlerhaft, z. B. weil einer der vorausgesetzten Werte im falschen Format vorliegt. |

#### Variablen nach der Kodierung

| Wert | Bedeutung | Beschreibung |
| :------------- | :------------- | :------------- |
| `CODING_COMPLETE`* | Kodierung vollständig | Für Code und Score sind gültige Werte gesetzt. |
| `NO_CODING`* | Keine Kodierung | Es ist ein Wert für die Variable gesetzt, aber es sind keine Instruktionen oder Regeln zum Kodieren verfügbar. |
| `CODING_INCOMPLETE` | Kodierung unvollständig | Es wurden Versuche unternommen, automatisch und evtl. zusätzlich  manuell zu kodieren, aber es konnte kein Code und kein Score zugeordnet werden. |
| `CODING_ERROR` | Kodierungsfehler | Der Wert hat nicht das erwartete Format (z. B. numerisch) oder die Transformation ist fehlgeschlagen (z. B. Umformung eines Datums in ein Standardformat). |

Die mit * gekennzeichneten Stati können im Primärdatensatz enthalten sein. Sie sind also zulässige Zustände einer Antwort zum Ende der Aufbereitung und der Kodierung. Die anderen Zustände kennzeichnen nur Verarbeitungsstufen während der Aufbereitung und Kodierung. 

## value
Hier ist der Antwortwert gespeichert. Das Format ist nicht festgelegt, sondern ist auf alle in JSON zulässige Daten bzw. Datenstrukturen ausgeweitet. Das ermöglicht dem Player, bei Bedarf sehr komplexe Zustände effizient zu speichern.

Zur Weiterverarbeitung der Antworten wird allerdings der Wert in einen String umgewandelt. Die nachfolgenden Prozesse - insbesondere die Kodierung - erwarten ein einheitliches Datenformat. Ein string-Wert wird nicht weiter verändert, aber alle anderen Datentypen müssen (z. B. über `JSON.stringify()`) serialisiert werden. Boolsche Wert sind dann beispielsweise als `"true"` und `"false"` auswertbar.

## code
Sofern der Wert kodiert wurde, wird zusätzlich dieser Code mit angegeben. Es handelt sich stets um einen ganzzahligen Integer, der die Antwort in eine Kategorie einordnet und damit für eine statistische Analyse erschließt. Üblicherweise werden positive ganze Zahlen für gültige Antworten und negative ganze Zahlen für ungültige oder fehlende Antworten verwendet.

## score
Sofern der Wert kodiert wurde, kann zusätzlich eine Bewertung des Codes mit angegeben werden. Damit kann z. B. ausgedrückt werden, ob es sich um eine richtige oder eine falsche Antwort handelt, also üblicherweise `0` oder `1`. Dies ist für die nachfolgende statistische Analyse wichtig. Es kann aber als score auch ein Wert gesetzt werden, der  eine abgeleitete Variable steuert und hierfür auch negative ganze Zahlen einschließt.
