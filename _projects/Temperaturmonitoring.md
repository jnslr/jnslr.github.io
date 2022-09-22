---
layout: page
title: Temperatur überwachen
description: Temperaturüberwachung eines leerstehenden Gebäudes via Mobilfunk
img: assets/img/projects/tempmonitor/TempSensor1.PNG
importance: 1
category: Sonstiges
---

Im Bekanntenkreis wurde ich damit betraut in einem leerstehenden Gebäude am anderen Ende der Stadt ab und an nach dem Rechten zu sehen.
Der Altbau musste über die Wintermonate geheizt werden, um Frostschäden zu vermeiden.
Leider hat sich schnell herausgestellt, dass die Heizungsanlage mehrmals pro Woche ausfällt und anschließend manuell in Gang gesetzt werden muss.
Zudem kühlte die Immobilie aufgrund der schlechten Isolierung sehr schnell aus, was einen täglichen Kontrollgang notwendig machte.

Es war also eine schnelle und günstige Lösung gefragt um den Aufwand zu reduzieren und dennoch ruhigen Gewissens schlafen zu können.
Folgende Punkte sollten umgesetzt werden:

- Temperaturerfassung an mehreren Stellen im Haus
- Sensordaten sollten online abrufbar sein
- Möglichst keine/geringe Kosten
- Kein Festnetz bzw. Internetanschluss vorhanden &rarr; Lösung zum Übermitteln der Daten finden

## Umsetzung

### Hardware

Da die Zeit drängte, musste auf vorhandene Materialien aus der Bastelkiste zurückgegriffen werden.
Die Wahl fiel auf einen ESP8266 Mikrocontroller in Form von Wemos D1 Mini Modulen sowie dem Bosch BMP280 Sensor zur Temperaturerfassung.

Um die Hardware etwas zu schützen wurde ein [Gehäuse](https://www.thingiverse.com/thing:3727934) von Thingiverse heruntergeladen und gedruckt.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/D1MiniMitSensor.jpg" title="D1MiniMitSensor" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    D1 Mini Modul,BMP280 Sensor und Gehäuse
</div>

Der Sensor wurde fest verlötet, um Fehler durch unzuverlässige Steckverbindungen zu vermeiden.
Zusätzlich wurden Verdrahtung und Module mit etwas Heißkleber fixiert.

Da zu diesem Zeitpunkt noch nicht klar war ob eventuell ein Akkubetrieb notwendig ist wurden die Pins `D0 (GPIO16)` und `RST` gebrückt.
Dies erlaubt den stromsparenden Betrieb des ESP im [Deep Sleep](https://randomnerdtutorials.com/esp8266-deep-sleep-with-arduino-ide/).
Hierbei wird der Mikrocontroller in einen "Schlafzustand" versetzt. Über ein Signal am `RST` Pin kann dieser wieder aufgeweckt werden.
Das Signal kann extern getriggert werden, oder - wie in unserem Fall - vom ESP selbst am *Wake Pin* `GPIO16` erzeugt werden.
Im Deep Sleep selbst werden nur wenige µA Strom benötigt, somit können bspw. mit einer 18650 Akkuzelle Laufzeiten von mehreren Monaten (je nach Aufwachrhythmus) erreicht werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/wiring.jpg" title="Verkabelung" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Gehäuse und Verkabelung gewinnen keinen Schönheitspreis, sind aber zuverlässig und funktional
</div>

### Software

Auch für das Schreiben eigener Software musste aus Zeitgründen verzichtet werden.
Glücklicherweise gibt es auch hier tolle OpenSource Software, die triviale Anwendungsfälle wie diesen abdeckt.

Hier fiel die Wahl auf [ESPEasy](https://github.com/letscontrolit/ESPEasy).
Die Firmware kann schon fertig kompiliert von der Release-Seite des Github Projekts heruntergeladen werden.
Über ein Webinterface können die Geräte dann konfiguriert werden.

ESPEasy unterstützt das Senden der Daten an [Thingspeak](https://thingspeak.com/), eine Cloud Platform zum Sammeln und Analysieren von Sensordaten.
Hier können bis zu 4 "Channels", sprich Sensoren mit bis zu 3 Millionen Datenpunkten pro Jahr kostenlos eingebunden werden.
Hierzu wurde ein Account auf Thingspeak erstellt und 2 Channels für die beiden Sensoren angelegt.
Anschließend konnten die ChannelID'S und API-Keys (Berechtigungen zum lesen/schreiben der Daten) im Webinterface von ESPEasy eingetragen werden.

Um die Daten auch mobil abrufen zu können habe ich die App [ThingShow](https://play.google.com/store/apps/details?id=com.devinterestdev.thingshow&hl=de&gl=US) verwendet.
Auch hier muss man die entsprechenden ChannelID's und API-Keys in der App eintragen und hat anschließend Zugriff auf die Daten.

### Internetanbindung

Blieb noch das Problem der fehlenden Internetanbindung.
Lösungen wie beispielsweise LoRaWAN kamen leider aufgrund von Kosten, Lieferzeit und Entwicklungsaufwand nicht in Frage. 

Glücklicherweise besitze ich einen Zweitrouter ([gl-mt300n-v2](https://www.gl-inet.com/products/gl-mt300n-v2/)).
Diesen nutze ich hauptsächlich um ein Testnetzwerke aufzubauen, während ich an Projekten/Geräten arbeite.
Dank des OpenWRT Betriebssystems dieser Router sehr individuell und frei konfigurierbar.
Zudem unterstützt er auch erweiterte Funktionen wie beispielsweise USB-Tethering, also das Teilen der Internetverbindung eines Smartphones mit dem Router und somit auch mit allen Geräten im Routernetz.

Ein erster Versuch dauerhaft ein altes Smartphone per USB-Tethering anzuschließen ist gescheitert, da das Telefon regelmäßig die USB-Verbindung unterbrochen hat und diese manuell wieder aktiviert werden musste.

Glücklicherweise fand sich auf dem Online Flohmarkt des Vertrauens ein günstig abzugebender 3G Surfstick.
Open WRT ermöglicht es auch mit solchen "Modems" eine mobile Internetverbindung aufzubauen. Hierzu müssen im Routermenü USB-Port, Service, APN und Pin der Simkarte eingestellt werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/ModemSettings.png" title="ModemSettings" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Konfiguration des UMTS-Sticks im Routermenü
</div>

Als Simkarte wurde eine werbefinanzierte gratis Simkarte bestellt, welche ein Datenvolumen von 200MB pro Monat gratis bereitstellt.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/router.jpg" title="router" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Router mit UMTS Stick
</div>


## Datenauswertung

Eine "echte" Datenauswertung fand nicht statt. Für den Anwendungsfall genügt es 1-2 mal täglich per App die Temperatur zu prüfen.
Sobald die Heizungsanlage ausfiel waren im Temperaturverlauf starke Temperatureinbrüche erkennbar.
Dies war ausreichend um zu wissen, dass ein "Serviceeinsatz" erforderlich war.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/HeatingFailures.png" title="HeatingFailures" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Langzeitmessdaten mit Temperatureinbrüchen
</div>

Interessant war es zu sehen, dass die Sensoren sehr identische Temperaturverläufe über den Tag hinweg zeigten.
Hier war der Tagesverlauf der Außentemperatur vom morgendlichen Erwärmen bis zum Abkühlen über Nacht erkennbar.
Sensor 1 zeigte an manchen Tagen starke Temperatur "Spikes" immer zur gleichen Uhrzeit. Diese wurden durch eine etwas ungünstige Positionierung verursacht: Zu dieser Tageszeit schien die Sonne für kurze Zeit direkt auf den Sensor. Nur an bewölkten Tagen waren geringere oder gar keine Sprünge zu erkennen.


<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/tempmonitor/SunSpikes2.png" title="SunSpikes2" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Temperatursprünge durch Sonneneinstrahlung
</div>


## Fazit

Mit einer Investition von ~5€ (UMTS Stick) und einem "Implementierungsaufwand" von weniger als einem Tag erreicht dieses Projekt wohl ein unschlagbares "Kosten-Nutzen" Verhältnis.
Die Überwachung stellte hier eine große Erleichterung dar und funktionierte bis auf wenige Ausnahmen über den kompletten Winter zuverlässig.
Es ermöglichte mir sogar ein paar Tage wegzufahren, denn im Falle eines Heizungsausfalls konnte einfach ein Nachbar informiert werden, der die Heizung wieder in Gang setzte.


### Verbesserungspotential

Sicherlich gäbe es auch in diesem Projekt einiges an Verbesserungspotential.
Eine automatisierte Datenauswertung mit passendem Alerting, bspw. per Mail wäre hier wohl eine der einfachsten und sinnvollsten Verbesserungen.

Da die Heizung durch einen einfachen Knopfdruck wieder in Betrieb genommen werden konnte wäre hier auch eine "remote" Lösung denkbar gewesen.
Beispielsweise "non-invasiv" indem ein kleiner Servomotor den Knopf betätigt.