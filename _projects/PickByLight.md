---
layout: page
title: Pick By Light
description: Pick By Light System mit Wifi basierten Microcontrollern und Electron App zur Auftragsverwaltung
img: assets/img/projects/pickbylight/app.png
importance: 3
category: freiberufliche Tätigkeit
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/app.png" title="Desktopanwendung" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Screenshot aus der Desktop Anwendung
</div>

## Pick By Light

Als Pick by Light bezeichnet man die visuelle Unterstützung der Mitarbeiter während des Montage- oder Kommissionierprozesses.
Hierbei leuchten meist am entsprechenden Entnahmeplatz kleine LED's auf, sodass das Personal direkt das richtige Fach zur Entnahme einer Position erkennen kann.
Die Entnahme des Artikels kann dann beispielsweise per Knopfdruck bestätigt, oder aber auch per Lichtschranke erkannt werden.

Solche Systeme erhöhen zum einen den Durchsatz, besonders bei weniger routiniertem Personal, da ein langes Suchen nach dem korrekten Fach ausbleibt.
Zudem kann durch die Bestätigung der Entnahme geprüft werden, dass alle benötigten Positionen auch entnommen wurden.
Die Wahrscheinlichkeit einer Fehlkommissionierung oder fehlender Bauteile bei der Montage wird somit erheblich reduziert.

Zudem ermöglicht der Einsatz eines Pick by Light Systems oftmals erst die "chaotische Lagerhaltung".
Darunter versteht man eine effiziente Lagerhaltung, bei der die Positionen nicht nach Kategorien sortiert werden.
So kann der zur Verfügung stehende Lagerraum perfekt ausgenutzt werden, ohne dass Lagerflächen freigehalten oder umsortiert werden müssen.
Indem man ähnliche Bauteile (bei denen Verwechslungsgefahr besteht) räumlich möglichst weit voneinander entfernt lagert können auch so wieder Fehlkommissionierungen vermieden werden.
Der Nachteil der chaotischen Lagerhaltung, nämlich das lange Suchen nach den Positionen kann hier wieder durch ein Pick by Light System kompensiert werden.


Das hier vorgestellte Pick By Light System basiert auf einer Desktopanwendung sowie per WLAN verbundenen Pick By Light Geräten.
Die Geräte sind durch ihre WLAN Anbindung frei positionierbar und benötigen lediglich eine Spannungsversorgung. Sie sind mit einer LED, sowie einem Knopf zur Entnahmebestätigung ausgestattet.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/SystemDiagram.svg" title="Pick by Light Konzept" class="bg-light img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Anbindung der Geräte per WLAN
</div>

> Dieses Projekt wurde als "Showcase" bzw. Proof of Concept umgesetzt und ist aktuell nicht im produktiven Einsatz

## Desktopanwendung

Die Desktopanwendung ermöglicht das Laden und Bearbeiten von Aufträgen. Die Aufträge können einfach per SAP im .htm Format exportiert werden.
Die Software liest alle Positionen des Auftrags ein und lässt die Geräte an den entsprechenden Entnahmefächern aufleuchten.
Die Entnahme wird dann vom Anwender per Knopfdruck direkt am Gerät bestätigt. Enthält der Auftrag Positionen die nicht mit einem Gerät verknüpft sind, so kann die Entnahme einfach in der Anwendung bestätigt werden.

Solange die Anwendung läuft wird, der Bearbeitungsstatus gespeichert. Es können also auch mehrere Aufträge gleichzeitig bearbeitet werden.

### Neue Geräte einrichten

#### Ersteinrichtung
{: #setup}

Alle notwendigen Konfigurationsdaten werden persistent auf den Geräten gespeichert und lassen sich anschließend auch "remote" also über das WLAN Netzwerk anpassen.
Für die Ersteinrichtung müssen allerdings zumindest die WLAN-Zugangsdaten auf dem Gerät konfiguriert werden.

Dies kann schon beim Programmieren erledigt werden, was insbesondere für große Stückzahlen sinnvoll ist.
Für die Einrichtung einzelner Geräte wurde eine Setup-Funktion eingeführt die es ermöglicht die Einrichtung ohne Programmierkenntnisse durchzuführen:

Wird der Button des Geräts während dem Bootvorgang gedrückt, so erstellt dieses einen eigenen WLAN-Hotspot.
Verbindet man sich mit diesem, so kann eine Konfigurationsseite aufgerufen werden, welche die Eingabe der Konfigurationsdaten ermöglicht.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/setuppage.png" title="Einrichtung per Website" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Einrichtung per Website
</div>

Die Scanfunktion ermöglicht es nach vorhandenen Netzwerken zu suchen, so muss zumindest der Netzwerkname nicht händisch eingetragen werden.
`Broker Adresse` bezeichnet die IP-Adresse der Rechners auf dem die Desktopanwendung läuft. Diese sollte - sofern möglich - statisch vergeben sein.


#### Koppeln der Geräte mit Artikelnummern

Sobald ein neues Gerät eingerichtet wurde, erscheint es in der Geräteliste.
Nun muss noch die Zuordnung des Geräts zu einer Artikelnummer erfolgen.

Sollten die Geräte zum Zeitpunkt der Zuordnung schon am Platz angebracht sein, oder die Geräte nicht mehr eindeutig identifizierbar sein, so besteht hier auch die Möglichkeit die LED direkt anzusteuern (über das Glühbirnensymbol) und so das Gerät ausfindig zu machen.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/devices.gif" title="Gerätezuordnung" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Neue Geräte werden automatisch gefunden und können dann zugeordnet werden
</div>


### Aufträge bearbeiten

Dies ist der Hauptbildschirm der Anwendung.
Es werden alle verfügbaren Aufträge und deren wichtigsten Infos aufgelistet.
Klickt man auf einen Auftrag so wird dieser gestartet. Neue Aufträge können über das Ordnersymbol hinzugefügt werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/orderProcessing.gif" title="Auftragsverarbeitung" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Aufträge können per Klick gestartet werden
</div>

Sobald ein Auftrag gestartet wurde, werden alle erforderlichen Artikel für diesen Auftrag aufgelistet.
Ist die Artikelnummer mit einem Gerät verknüpft, so leuchtet die LED auf.
Der Benutzer muss hier die Entnahme über den Button am Gerät bestätigen, dann erlischt die LED und in der Anwendung wird die entsprechende Zeile des Auftrags als abgeschlossen (grün) markiert.

Sind Artikelnummern nicht mit einem Gerät verknüpft, so erscheint das Warnsymbol und die Entnahme muss in der Anwendung bestätigt werden.

Sind alle Positionen des Auftrags abgeschlossen, so erscheint eine Erfolgsmeldung und der Auftrag wird archiviert.
Er ist dann nicht mehr unter den verfügbaren Aufträgen sichtbar.


### Geräteupdates
{: #fw-update}

Die Firmware der Geräte kann auch per WLAN aktualisiert werden.
Sobald sich ein Gerät anmeldet, prüft die Software automatisch ob die Firmware dem aktuellen Stand entspricht.
Falls nicht, kann ein Update über den entsprechenden Button durchgeführt werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/fwupdate.gif" title="Firmware Update" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Firmware updates der Geräte per Wlan
</div>

Der Updatestatus wird live aktualisiert. Ist das Update komplett, so dauert es einen kurzen Moment bis sich das Gerät wieder anmeldet, dann mit der neuen Firmware-Version.

### Hilfeseite für den Benutzer

Die Hilfeseite bietet dem Benutzer direkte Hilfestellung für unterschiedliche Aufgaben und ist übersichtlich als ausklappbares Akkordeon-Menü ausgeführt.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/pickbylight/help.png" title="Hilfeseite" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Hilfeseite für den Benutzer
</div>


## Technologien

### Desktopanwendung

Die Desktopanwendung basiert auf dem [Electron Framework](https://www.electronjs.org/).
Dieses ermöglicht das packen einer Webanwendung (HTML,CSS, Javascript) in eine Desktopanwendung.
Zusätzlich kann auch *Backend* Code in Javascript geschrieben werden.

Das Frontend nutzt [Bootstrap](https://getbootstrap.com/) und [Vue.js](https://vuejs.org/) um ansehnliche dynamische Inhalte bereitzustellen.
Für die *Toast* Nachrichten, kommt die [Toastr](https://github.com/CodeSeven/toastr) Bibliothek zum Einsatz.

Zur persistenten Speicherung der Daten (bspw. der Geräteliste) wird [electron-store](https://github.com/sindresorhus/electron-store) verwendet.
Die JSON-Objekte werden vor dem Speichern und Laden mit [Ajv](https://ajv.js.org/) validiert.
Bedenken bezüglich der Performanz wurden mit einem Testskript ausgeräumt: Das Lesen von 1 Million Datensätzen dauerte ca. 1,6 Sekunden und skalierte linear.
Dies sollte für den Anwendungsfall mehr als ausreichend sein, eine "echte" Datenbank muss also nicht zwingendermaßen eingesetzt werden.

Um auch Fehler die beim Kunden auftreten analysieren zu können, werden mit Hilfe von [electron-log](https://github.com/megahertz/electron-log) Logdateien geschrieben.


### Kommunikation Desktopanwendung &harr; Firmware

Die Kommunikation zwischen Desktopanwendung und Firmware findet per MQTT statt.
Bei MQTT gibt es einen *Broker* welcher Nachrichten von *Clients* empfängt und diese an *abonnierte (subscribed)* Clients weiterleitet.
In diesem Projekt sind sowohl die GUI, als auch die Firmware Clients, welche sich zum Broker verbinden.
Sobald ein Pick by Light Gerät online geht, sendet es eine Nachricht, die von der GUI empfangen wird.
So können beispielsweise die "Neues Gerät gefunden" Nachrichten realisiert werden.
Analog funktioniert auch das Schalten der LED: Die GUI verschickt eine MQTT Nachricht, welche in der Firmware der Pick By Light Geräte verarbeitet wird.

Normalerweise ist der MQTT Server auf einem separaten Rechner im Netzwerk eingerichtet oder er läuft als separates Programm bspw. auf dem Rechner.
Um den Einrichtungsaufwand des Systems so gering wie möglich zu halten wurde in diesem Projekt darauf verzichtet einen separaten Broker zu verwenden.
Stattdessen wurde der Broker direkt in das Backend der Electron-Anwendung integriert.
Hierzu wurde die Node.js Bibliothek [aedes](https://github.com/moscajs/aedes) eingesetzt. 

### Vorteile

Durch die Verwendung von MQTT und Webtechnologien im Frontend, wäre es durchaus denkbar die Anwendung mit nur geringem Mehraufwand als Serverapplikation bzw. Webapp umzubauen.
So könnten z.B. auch mehrere Rechner in einem Unternehmen gleichzeitig und von mehreren Standorten auf die Anwendung zugreifen und das MQTT System wäre nicht mehr davon abhängig, dass die Desktopanwendung gestartet ist.


### Pick By Light Geräte und Firmware

Der ursprüngliche Entwurf der Geräte basierte auf dem [Sonoff SV](https://itead.cc/product/sonoff-sv/) Board.
Dieses bietet den Vorteil, dass es mit 5-24V Versorgungsspannung gängige Industriespannungsbereiche abdeckt.
Durch das verbaute Relay können bei Bedarf auch größere Verbraucher geschaltet werden.
Das Board basiert - mal wieder - auf dem ESP8266 Chip, somit ist die Firmware einfach auf andere Boards die diesen Chip verwenden portierbar.
> Die Entwicklung bspw. erfolgte auf Wemos D1 Mini Modulen. Hier ist lediglich zu beachten , dass die D1 Mini mehr Flashspeicher bieten im Vergleich zum Sonoff SV. 

Als LED's werden NeoPixel Module verwendet. Diese ermöglichen bei Bedarf auch komplexere Lichtszenarien und unterstützen auch die Verwendung unterschiedlicher Farben.


Die Firmware der Geräte ist recht simpel gehalten:

Das *little.fs* Filesystem sorgt für die persistente Speicherung der Konfigurationsdaten als JSON-Objekt.
Hierbei ist es auch möglich einzelne Einstellungen zu ändern oder neue Konfigurationen zu *mergen*.
Somit stellt auch die Konfiguration mehrerer/aller Geräte per Netzwerk kein Problem dar.

Das Firmwareupdate per Netzwerk wurde mit dem [espota.py](https://github.com/esp8266/Arduino/blob/master/tools/espota.py) Tool realisiert.
Dieses wurde mit *pyinstaller* in eine Windows executable *kompiliert* und wird zusammen mit der Desktopanwendung ausgeliefert.

Bei Verwendung von espota (OTA = OverTheAir) werden 2 Partitionen auf dem Speicher des ESP angelegt, eine für die gerade aktuelle Firmware und eine für eine neue Firmware, welche per WiFi eingespielt werden kann. 
Erst wenn das Update der neuen Partition erfolgreich war, wird der ESP von der neuen Partition gebootet, die alte Partition steht dann für neue Updates bereit.
Dies ermöglicht einen sehr zuverlässigen Updateprozess, schlägt ein Update fehl, so wird wieder von der alten Partition gebootet, das Gerät bleibt funktionsfähig. 

> Aufgrund der 2 Partitionen steht bei Verwendung von OTA-Updates nur noch der halbe Programmspeicher auf dem Mikrocontroller zur Verfügung.

Zur Ansteuerung der LED's wurde die [NeoPixel](https://github.com/adafruit/Adafruit_NeoPixel) Bibliothek verwendet.
Farbe und Helligkeit der LED's können in der Konfiguration eingestellt werden.
Aktuell sind die Einstellungen nicht dynamisch veränderbar. Dies könnte jedoch einfach ergänzt werden, möchte man bspw. in einem Mulit-User Szenario für jeden Nutzer eine eigene Farbe verwenden oder etwa unterschiedliche Artikelkategorien farblich kennzeichnen.


### Continous Integration und Versionierung

Sobald ein commit auf dem *main* branch erzeugt wird, werden automatisch eine neue Firmware und anschließend eine neue Desktopanwendung gebaut und eindeutig versioniert.
Hierzu werden Github Actions verwendet.
Die Desktopanwendung wird in Form eines *.msi* Installers ausgeliefert. Entsprechend können auch technisch weniger versierte Nutzer einfach ein Update durchführen indem Sie den Installer ausführen.

Der Installer beinhaltet auch eine Firmwareversion.
Um die [Updatefunktion](#fw-update) zu realisieren muss die Desktopanwendung Kenntnis über die Version der Firmware besitzen. Eine Möglichkeit wäre es, entsprechende *Infofiles* mitzuliefern. Erfahrungsgemäß ist dies aber unzuverlässig, da immer darauf geachtet werden muss, dass die Infofiles synchron mit der Firmware gehalten werden.
Daher wurde hier die Versionsinformation in die Firmware integriert/einkompiliert. Die Desktopanwendung analysiert die Binärdatei der Firmware und sucht sich diesen Versionsinfostring heraus. Somit kann die Firmware komplett unabhängig von GUI und sonstigen Dateien getauscht werden.

## Mögliche Weiterentwicklungen 

- Flashen bzw. Update der Konfiguration per USB anstelle von WiFi: So könnte die [Website basierte Ersteinrichtung](#setup) vereinfacht werden. Insbesondere, da die meisten Einstellungen (bspw. IP des Desktoprechners, Netzwerkname, MQTT Port) schon der Desktopanwendung bekannt sind, bzw. ausfindig gemacht werden können.
- Statistikerfassung, bspw. Zeit pro Auftrag, Zeit pro Artikel, Aufträge pro Tag erfassen, auswerten und darstellen.
- Portieren auf Serveranwendung könnte auch Multi-User Szenarien ermöglichen