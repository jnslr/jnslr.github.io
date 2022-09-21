---
layout: page
title: Motoren synchronisieren
description: Phasengleichlauf zweier Motoren mit Siemens S7
img: assets/img/projects/motorsync/P_ST70_XX_07579J.jpg
importance: 1
category: freiberufliche Tätigkeit
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/motorsync/P_ST70_XX_07579J.jpg" title="symbolbild" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    <a href="https://www.automation.siemens.com/bilddb/index.aspx?gridview=view2&objkey=P_ST70_XX_07579&showdetail=true&view=Searc">© Siemens AG 2022, Alle Rechte vorbehalten</a>
</div>

## Anforderung

In diesem Projekt sollten 2 Motoren einer Produktionsanlage miteinander synchronisiert werden.
Die Motoren wurden bisher durch mechanische Kopplung miteinander synchronisiert. Diese war allerdings sehr verschleißanfällig und somit wartungsintensiv.
Daher wurde der zweite Antrieb mechanisch entkoppelt und wird nun per SPS angesteuert und synchronisiert.

Durch die Entkopplung entstehen folgende Vorteile:
- Der Hauptantrieb wird entlastet
- Weniger Verschleiß und bessere Wartbarkeit
- Geringerer Energiebedarf durch weniger bewegte Massen und Reibung
- Entsprechend ist auch ein höherer Durchsatz der Anlage möglich

Eine besondere Herausforderung bestand darin, dass die Motoren nicht nur drehzahlsynchron laufen müssen, sondern auch ihre Phasenlage aufeinander abgestimmt werden muss.

Zusätzlich wurden Sicherheitsfunktionen wie die Zuhaltung von Schutztüren über ein Sicherheitsprogramm implementiert.

## Umsetzung

- Die Drehzahl und Position des Hauptantrieb wird mit einem Absolutencoder erfasst. Dieser wird per Profinet angebunden
- Der zu synchronisierende Motor wird über einen V90 Frequenzumrichter angesteuert und über Profinet angebnunden.
- Der Sicherheitskreis wird mit Sicherheitsein-/ bzw. Ausgängen im Sicherheitsprogramm der SPS realisiert.
- Die Steuerung der Anlage wird von einer Siemens S7 1500 mit MotionControl Objekten übernommen.
- Eine LED zeigt die Zustände der Analage (nicht synchronisiert, synchronisieren, synchonisiert) durch unterschiedliche Blinklängen an.

## Testaufbau

Zum Prüfen der Funktion des Systems, ohne die komplette Anlage betreiben zu müssen wurde ein Testsaufbau umgesetzt. Dieser besteht aus einem kleinen Gleichstrommotor, welcher mit vergleichbarer Drehzahl des Hauptantriebs betrieben werden kann.
Der DC-Motor treibt den Encoder an, der im realen System mit dem Hauptantrieb gekoppelt ist.
Der zu synchronisierende Motor wurde durch einen kleineren Motor der gleichen Baureihe ersetzt.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/motorsync/testaufbau.jpg" title="testaufbau" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Testaufbau mit DC-Motor (Hauptantrieb), Encoder und Servomotor (Synchronlauf), v.r.n.l.
</div>

Die Kopplung des Testantriebs wurde mit einem 3D gedruckten Flansch und einem Riemenantrieb realisiert.
Um die korrekte Funktion der Phasengleichlaufs zu prüfen wurden an Encoder und Motorwelle jeweils 3D gedruckte *Fahnen* angebracht.

## Weitere Punke

- Phasenversatz und Übersetzung wurden über ein Webinterface sowie über das Displaypanel der SPS einstellbar gemacht.
- Bei Problemen kann eine Logdatei über das Webinterface heruntergeladen werden, welche die Zustandsübergänge der Motoren aufzeichnet
- Es wurde ein Schaltplan mit Hilfe von [QElectroTech](https://qelectrotech.org/) erstellt
- Es wurde eine ausführliche Dokumentation im PDF und HTML Format bereitgestellt. Die Dokumentation wurde in *Markdown* verfasst, und anschließend mit [Pandoc](https://pandoc.org/) exportiert. Für den PDF Export wurde das [Eisvogel LaTeX Template](https://github.com/Wandmalfarbe/pandoc-latex-template) verwendet.



## Besondere Herausforderungen

- Der Absolutwertgeber hat in der Standardkonfiguration nach einem Neustart des Systems seine Absolutposition verloren. Hier musste das Telegramm im SPS Code modifiert werden, damit die Absolutposition korrekt übermittelt wird.
- Die STO (SafeTorqueOff) Funktion des Frequenzumrichters (V90) sollte durch die Sicherheitsausgänge der SPS geschaltet werden. Diese führen allerdings regelmäßig einen Dunkeltest (kurzes Abschalten des Ausgangs zum prüfen der korrekten Funktion). Dieser Test hat die STO Funktion des Frequenzumrichters ausgelöst und zum Stillstand und Fehlermeldung des Motors geführt. Hier musste ein weiteres Sicherheitsschaltgerät verwendet werden um die korrekte Funktion zu gewährleisten.