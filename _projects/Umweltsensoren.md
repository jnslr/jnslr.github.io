---
layout: page
title: Umweltsensoren
description: Modulares, WiFi basiertes Sensorsystem zum Erfassen von Umweltdaten. Datenspeicherung, Monitoring und Auswertung in der Cloud.
img: assets/img/projects/envsensors/Luftsensoren.jpg
importance: 2
category: freiberufliche Tätigkeit
---

## Anforderung

Bei diesem Kundenprojekt sollten mehrere hermetisch voneinander abgeschlossene Umgebungen insbesondere im Bezug auf deren Luftqualität überwacht werden.
Gefordert war die Umsetzung folgender Punkte:

- Überwachung der Luftqualität in mehreren Umgebungen durch Erfassen von
  - Temperatur, Luftfeuchte, Luftdruck
  - Kohlenstoffdioxid (CO2) Konzentration
  - Sauerstoff (O2) Konzentration
- Aktivitäten/Bewegungen erkennen und grob quantifizieren (Aktivitätslevel bestimmen)
- Globale Datenverfügbarkeit &rarr; Anbindung an ein Cloudsystem
- Live Monitoring und Alerting bei kritischen Zuständen
- Möglichst geringe Kosten
- Flexibles System
  - Einfaches Erweitern oder auch Entfernen von Sensoren
  - Einfacher Anschluss/Umpositionieren der Sensorsysteme. Häufiger Umbau/Wartung erfordert auch das Abbauen und erneute Anschließen der Sensoren. Daher soll dies möglichst schnell und einfach von der Hand gehen.


## Umsetzung

### Konzept

Die Umsetzung erfolgte mit D1 Mini Modulen, welche auf dem ESP8266 Chip basieren.
Die Firmware der Sensormodule wurde mit [Platformio](https://platformio.org/) erstellt.
Diese erledigt die Erfassung von Sensordaten per GPIO oder I²C Schnittstelle und publiziert die Messwerte anschließend als MQTT Nachricht im lokalen Netzwerk.

Der MQTT Broker läuft auf einem Raspberry PI, welcher sich im lokalen Netzwerk befindet.
Durch die zusätzlich auf dem Gerät laufende [Telegraf-Instanz](https://www.influxdata.com/time-series-platform/telegraf/) werden bestimmte MQTT Nachrichten an eine in der Cloud gehostete InfluxDB weitergeleitet.
Der Raspberry PI fungiert somit als Gateway in die Cloud.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/envsensors/schematic.svg" title="Prinzipbild" class="p-3 bg-white img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Sensorkonzept mit Cloudanbindung
</div>


### Modularität

Die Sensoren werden entweder per I²C Schnittstelle ausgelesen, oder nutzen die GPIO's des D1 Mini Moduls.
Um das Konzept möglichst modular und erweiterbar zu halten, wurde hier ein entsprechendes Adapterboard/Breakoutboard entwickelt.
Dieses macht die I²C, SPI und GPIO Schnittstellen per Steckerbuchse verfügbar.
So können Sensoren einfach per Steckverbindung angeschlossen bzw. getauscht werden.

Das Adapterboard versorgt zudem auch alle angeschlossenen Sensoren mit Energie.
So benötigt jedes Sensorsystem nur einen einzigen Anschluss (`Micro-USB` zur Spannungsversorgung) für den Betrieb.
Die Versorgungsspannung kann mit günstigen, handelsüblichen USB-Steckernetzteilen bereitgestellt werden.
Dadurch ist die Portabilität des Sensorsystems gewährleistet und für jeden handhabbar: Ausstecken, Einstecken läuft.


<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/envsensors/espboxcut.png" title="Haupteinheit" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Prototyp der Sensor-Haupteinheit mit Steckbuchsen zum Verbinden der Sensorkomponenten
</div>

Auch die Gerätefirmware wurde diesem *Plug and Play* Ansatz entsprechend konzipiert:
Die Messdaten werden nur veröffentlicht wenn auch tatsächlich ein Sensor verbunden ist.
Neu angeschlossene Sensoren werden automatisch erkannt und deren Daten erfasst.


Die Gerätefirmware kann per WiFi aktualisiert werden, was durch den VPN Zugriff sogar von jedem Standort weltweit möglich ist.
Hierdurch kann das System jederzeit angepasst oder um zusätzliche Funktionen erweitert werden.


### Gehäuse

Um die Sensormodule vor Umwelteinflüssen zu schützen und eine sichere Befestigung zu gewährleisten, wurden passende Gehäuse entworfen und anschließend 3D gedruckt.


<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/envsensors/Luftsensoren.jpg" title="Luftsensoren" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Luftsensormodul, enthält erforderliche Sensorik zum Erfassen von Temperatur, Luftfeuchte, Luftdruck, Co2, O2
</div>

Besonders die eingesetzten Lichtschranken profitieren von den 3D gedruckten Montagevorrichtungen.
Die Lichtschranken bestehen aus Sender- und Empfängereinheit.
Diese müssen mechanisch relativ präzise aufeinander ausgerichtet werden, um die Funktion des Sensors sicherzustellen.
Durch die 3D gedruckten Gehäuse ist deren Position jederzeit definiert, eine Fehlausrichtung ist nicht mehr möglich.


### Datenauswertung und Monitoring

Um die Daten sinnvoll auswerten zu können ist auch ein entsprechendes *Labeling* notwendig.
D.h. es müssen *Metadaten* zu den entsprechenden Datensätzen vorhanden sein.
Die Sensorfirmware unterstützt das Eintragen von Metadaten, wie beispielsweise des Sensorstandorts.
Mit dieser Information können die erfassten Daten bei der Auswertung auf den Standort und dessen - zum damaligen Zeitpunkt geltenden - Randbedingungen bezogen werden.

Bei einigen Sensoren wurde zumindest ein rudimentäres *Edge Computing* eingesetzt, d.h. die Daten werden vor dem Veröffentlichen schon auf dem Mikrocontroller vorverarbeitet.
Dies ist z.B. bei den eingesetzten Lichtschranken und IR-Sensoren zur Aktivitätsmessung der Fall:
Da die Messwerte teilweise stark *prellen* wurde ein Mikrocontroller seitiges Debouncing des berechneten Aktivitätslevels eingeführt. 
Werden die Sensoren mehrfach durch eine einzige Bewegung getriggert, so werden die fälschlicherweise ausgelösten Sensorsignale herausgefiltert.
Es werden also nur tatsächliche Bewegungen erkannt.

Da die Daten allesamt in der Cloud verfügbar sind, können schon auf der Website des Cloudanbieters nützliche Datenbankabfragen und entsprechende Visualisierungen eingerichtet werden.
Kritische Werte werden direkt online überwacht.
Zusätzlich wurde ein Flux-Script eingerichtet, welches eine E-Mail an eingetragene Benutzer sendet, sobald einer dieser *Alarme* anschlägt.
Somit werden verantwortliche Personen quasi in Echtzeit über kritische Systemzustände informiert.
Die Reaktionszeit beträgt weniger als 15 Minuten, kann aber auch einfach in den Einstellungen konfiguriert werden.

Sobald weitergehende Analysen der Daten erforderlich sind, können die Daten bspw. über die Rest-Schnittstelle abgefragt und in einem beliebigen Tool (z.B. Python mit Pandas, Numpy, etc.) weiterverarbeitet werden.