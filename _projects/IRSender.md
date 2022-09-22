---
layout: page
title: IR Sender
description: Senden von Infrarot Signalen zum Ersetzen einer Fernbedienung
img: assets/img/projects/irbox/irbox.jpg
importance: 1
category: Sonstiges
---

Kleine Studentenbude, großes Kino? Kein Problem dachte ich mir, und habe mir für mein 12m² großes Studentenzimmer einen Beamer angeschafft.
Das Erlebnis wurde allerdings dadurch getrübt, dass der Infrarot-Empfänger des Beamers auf der Hinterseite des Geräts angebracht war.
Da das Gerät direkt an der Wand - halb verdeckt durch ein Regalbrett - positioniert war, hatten die Infrarot-Signale der Fernbedienung kaum ein Durchkommen, diese war quasi unbrauchbar.

Warum also nicht die Fernbedienung durch das Smartphone ersetzen?
Gesagt getan, und so entstand die IR-Box.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/irbox/irbox.jpg" title="IR Sender Box" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    IR Sender Box und die zu simulierende Fernbedienung. Aus der Box heraus schaut die Infrarot-LED
</div>

Diese kleine Box verbindet sich mit dem WLAN Netzwerk und hostet eine simple Website.
Die Seite ist das digitale Abbild der analogen Fernbedienung.
Bei Klick eines Buttons sendet bzw. simuliert die Box das IR-Signal des entsprechenden Knopfes der Fernbedienung mithilfe der verbauten Infrarot-LED.
Da die Kommunikation von Smartphone zur Box per WLAN stattfindet ist diese nicht auf Sichtkontakt angewiesen.
Auf die kurze Strecke zum Beamer ist das IR-Signal dann auch völlig ausreichend und zuverlässig.
Die Box kann einfach per USB vom Beamer per Strom versorgt werden und ist somit direkt einsatzfähig sobald der Beamer angeschaltet wird.


### Hardware

Obwohl unverkennbar aus meiner persönlichen Prä-3D-Druck-Ära ist die Box nicht minder funktional.
Anstatt teure Elektronikgehäuse zu verwenden wurde eine "Tupperbox" aus dem 1€ Shop um die Ecke eingesetzt, farblich passend zur Wandfarbe versteht sich.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/irbox/internals.jpg" title="IR Sender Internals" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    <i>Eingeweide</i> der Box
</div>

Im Inneren der Box kommt ein ESP01 Modul zum Einsatz.
Diese sind extrem kostengünstig (1-2€ pro Stück), bieten allerdings nur sehr limitierten GPIO.
Da in diesem Projekt nur eine LED angesteuert werden muss ist dies völlig ausreichend.
Das Programmieren der Boards erfordert einen externen USB-zu-TTL Adapter (auf größeren Boards ist dieser schon verbaut) und auch das versetzen des Boards in den Programmiermodus erfordert etwas Geschick. Hierzu muss nämlich `GPIO0` auf Ground gezogen und gleichzeitig ein Reset durchgeführt werden.

Ein weiterer Nachteil des ESP01 ist der fehlende Spannungswandler auf dem Board, es kann nur mit 3,3V betrieben werden.
Daher kommt ein DC-DC Wandler (links im Bild) zum Einsatz, der die USB-Spannung von 5V auf 3,3V umsetzt.
Mittig sind der ESP01, die Infrarot-LED sowie deren Vorwiderstände auf einer kleinen Lochrasterplatine verdrahtet.

Rechts im Bild ist die improvisierte Zugentlastung zu erkennen. Diese Klemmt das USB-Kabel, um eine Beschädigung der internen Verkabelung bei Zug am USB-Kabel zu vermeiden.


### Software

Softwareseitig bestand die Herausforderung zunächst darin das IR-Signal der Fernbedienung zu identifizieren um dieses dann später reproduzieren zu können.

Hierzu wurde ein Infrarot-Empfänger am Arduino betrieben.
Mit Hilfe der [IRremote](https://github.com/Arduino-IRremote/Arduino-IRremote) Bibliothek konnte so das verwendete Infrarot Protokoll ausfindig gemacht und die Signale aufgezeichnet werden.

Dies gelang nicht auf Anhieb und erforderte viel Geduld und einiges an "Spielerei" mit den Parametern der Library bis schließlich die korrekten Signale emuliert werden konnten.
In meinem Fall verwendete die Fernbedienung das `NEC` Protokoll die Kommandos welches mit der Funktion `irsend.sendNEC(0xC03FB847, 32);` aufgerufen werden konnte.

|Kommando    |HEX-Code|
|------------|--------|
|OnOff       |C03FB847|
|Mute        |C03F40BF|
|LastSong    |C03FE01F|
|PlayPause   |C03F9867|
|NextSong    |C03FA05F|
|ButtonUp    |C03F906F|
|ButtonLeft  |C03F50AF|
|ButtonRight |C03F10EF|
|ButtonDown  |C03F807F|
|Ok          |C03FD02F|
|Back        |C03FB04F|
|Menu        |C03F7887|
|Bookmark    |C03FF807|
|VolumeDown  |C03FA857|
|VolumeUp    |C03F8877|
{: .table .table-sm}



Die Website wurde statisch in den Quellcode einkompiliert und verwendet einfache http-Requests zum auslösen der IR-Kommandos.
Selbstverständlich hätten hier noch weitere Funktionen, bspw. eine MQTT Anbindung, Sleep-Timer oder ähnliches hinzugefügt werden können.
