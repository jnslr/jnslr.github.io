---
layout: page
title: Dokumente archivieren
description: Meine Methode zum digitalen Archivieren von Dokumenten
img: assets/img/projects/archiving/archive.jpg
importance: 2
category: Sonstiges
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/archiving/archive.jpg" title="symbolbild" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  Photo by <a href="https://unsplash.com/es/@qwitka?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Maksym Kaharlytskyi</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</div>  

## Das Problem

Fast täglich landen Mitteilungen, Verträge, Rechnungen und - glücklicherweise eher selten - Mahnungen in meinem Briefkasten.
Diese wandern zunächst auf meinen persönlichen Stapel des Grauens.

Ist dann endlich der lang ersehnte, verregnete Sonntagnachmittag gekommen, mache ich mich - gut gestärkt vom Sonntagsbrunch und bewaffnet mit einer Tasse Kaffee - daran, den Stapel dem Erdboden gleich zu machen. Es wird gelocht, geheftet, sortiert, beschriftet. Für jedes Thema gibt es einen Ordner oder zumindest eine eigene Registerkarte.
Nach getaner Arbeit blicke ich stolz auf mein Werk, in einem spontanen Anflug von Hybris sage ich "Er sah, dass es gut war".

Doch man ahnt es gleich: Beim nächsten Garantiefall ist die Rechnung unauffindbar, und spätestens bei der Steuererklärung macht sich Ernüchterung breit:
War die Rechnung des Küchenmonteurs jetzt unter *Rechnungen* oder doch im Verzeichnis *Wohnung* einsortiert? Oder vielleicht doch bei *Versicherungen*, da der Wasserschaden ja von der Versicherung übernommen wurde?
Er sah also, dass es schlecht war.

## Eine Lösung

Anstatt unnötig Zeit mit der Archivierung zu vergeuden bin ich dazu übergegangen alle meine Dokumente zu digitalisieren, mit einer Nummer zu versehen und einfach chronologisch abzuheften.
Die digitalen Kopien werden mittels OCR (Optical Character Recognition), sprich einer Texterkennung, gescannt.

Dies erlaubt es, elektronisch nach Inhalten im Dokument zu suchen, und das sogar ohne zusätzlich zu installierende Software.
Ich lege alle Dokumente in einem Ordner auf meinem Rechner ab. Mit der Suche im Windows-Explorer - ja ich nutze auf meinem Haupsystem Windows - kann ich nun einfach und effizient nach Inhalten suchen.

Meine Lösung kurz gefasst:

- Chaotische Archivierung &rarr; Alles in einen Ordner (sowohl analog als auch digital)
- Digitalisierung &rarr; Scannen, Texterkennung und Durchnummerieren
- Indizierung &rarr; Erledigt die Windows-Suche


### Chaotische Archivierung

Nach der Digitalisierung werden die Dokumente mit einer eindeutigen Nummer versehen und anschließend in **einen einzigen Ordner** abgeheftet.
Vielleicht wäre der Begriff chonologische Archivierung angebrachter.

Wir wollen schließlich nicht mehr die analogen Dokumente, sondern ihre *digitalen Zwillinge* durchforsten, wenn wir auf der Suche nach einem bestimmten Dokument sind.
Sollte doch einmal das Original benötigt werden, so können wir duch unsere Indizierung immer schnell das Original ausfindig machen.

Falls unser Dokumentenmanagement doch einmal versagt, so sind die Dokumente zumindest chronologisch geordnet, und können so gefunden werden. 

### Digitalisierung

Zunächst scanne ich alle Dokumente, die sich über einen längeren Zeitraum angesammelt haben.
Da mein Scanner mit einem [ADF (Automatic Document Feeder)](https://de.wikipedia.org/wiki/Automatischer_Vorlagenwechsler) ausgestattet ist, kann ich hier bis zu 50 Seiten automatisiert scannen und mich entspannt zurücklehnen.
Zum Scannen nutze ich den [PDF24 Creator](https://tools.pdf24.org/de/creator).
Dieser stellt eine WLAN-Verbindung zu meinem Scanner her, und ich kann alle Seiten automatisch über den ADF scannen.

Ich gehe hier wie folgt vor:

Alle Seiten in den Scanner legen und die Vorderseiten scannen.

Nun die Rückseiten aller Dokumente scannen. Dadurch dass man den Papierstapel beim Scannen der Rückseiten umdreht, ist die Reihenfolge natürlich invertiert.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24ScanVorderUndRuckseite.PNG" title="DuplexScan" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Scan von 2 beidseitig bedruckten Dokumenten, zuerst Vorder- dann Rückseiten
</div>

Die Reihenfolge der Rückseitenscans über das Menü des Dokuments umkehren.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24SeitenreihenfolgeUmkehren.PNG" title="Seitenreihenfolge umkehren" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24SeitenreihenfolgeUmgekehrt.PNG" title="Seitenreihenfolge der Rückseiten korrekt" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0 caption">
        Seitenreihenfolge der Rückseiten über das Kontextmenü umkehren
    </div>
    <div class="col-sm mt-3 mt-md-0 caption">
        Seitenreihenfolge der Rückseiten ist nun korrigiert
    </div>
</div>

Nun müssen Vorder- und Rückseiten nur noch über die Reißverschlußmethode zusammengefügt werden. Hierzu beide Dokumente auswählen und dann den entpsrechenden Button drücken. Man erhält ein Dokument mit Vorder- und Rückseiten in der richtigen Reihenfolge.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24Reißverschluss.PNG" title="Vorder und Rückseiten zusammenführen" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Vorder- und Rückseiten mit dem Reißverschlußtool zusammenführen
</div>

Im PDF Creator die einzelnen Dokumente per Drag and Drop trennen und unter einer eindeutigen Nummer abspeichern. Ich nutze `0085_210501.pdf` als Format.
Wobei `0085` Die Dokumentennummmer angibt und `210501` Datum der Archivierung angibt. Die Dokumentennummer schreibe ich dann zusätzlich auf das Dokument.
Sodass wir eine eindeutige Indizierung von analogem Dokument und digitalem Zwilling (PDF-Dokument) erzeugt haben.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24DokumenteUnterteilen.PNG" title="Dokumente separieren" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Nun den Scan in einzelne Dokumente aufteilen
</div>

Im Anschluss müssen wir noch die Texterkennung über die Dokumente laufen lassen.
Hier bringt der PDF24 das "Text erkennen (OCR)" Modul mit.
Einfach alle neu erstellten Dokumente per Drag-and-Drop in das Fenster ziehen und die Texterkennung starten.
Diese erkennt Text im pdf Dokument und speichert den erkannten Text in den Metadaten der Datei ab.
Für maschinell erstellte Dokumente funktioniert das sehr zuverlässig, für handschriftliche Dokumente ist diese Methode allerdings kaum benutzbar.
Die Dateigröße wird im Übrigen nur minimal beeinflusst.
Bspw. 4 Seiten dicht bedruckter Text erhöhen die Dateigröße nur um wenige Kilobytes.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/PDF24OCR.PNG" title="Texterkennung starten" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Texterkennung für die neuen Dokumente starten
</div>

Sicherheitshalber speichere ich auch den Originalscan ab. Falls ich das OCR Tool wechseln sollte, kann ich die Texterkennung erneut über alle bisher angefertigten Originalscans laufen lassen, ohne erneut scannen zu müssen.

> Mit ein wenig Routine geht dieses Procedere recht schnell von der Hand. 
> In wenigen Minuten können mehrere, beidseitig bedruckte Dokumente digitalisiert und archiviert werden. 
> Der Mehraufwand ist für mich minimal, vor allem wenn man mehrere Dokumente im Block scannt und archiviert.
> Die Zeitersparnis, gerade bei der Steuererklärung o.ä. ist dafür umso höher.


### Indizierung

Ja, Dokumentenmanagement ist eigentlich ein gelöstes Problem. Sogenannte Dokumentenmanagementsysteme gibt es zuhauf.
Allerdings konnte ich - zumindest nach meiner kurzen Recherche - kein geeignetes Tool finden, das plattformunabhängig, kostenfrei und einfach zu bedienen sowie zu installieren ist. Die meisten Tools benötigen einiges an Installationsaufwand (Datenbank aufsetzen, Webserver einrichten, etc.). Durch die datenbankbasierte Funktionsweise der meisten Tools gestaltet sich auch der Wechsel zwischen Tools als sehr schwierig.

> **Nachtrag:** Einige interessante Projekte gibt es dann doch:
>  - [Openpaper](https://openpaper.work)
>  - [Papermerge](https://www.papermerge.com/)
>  - [papgerless-ng](https://github.com/jonaswinkler/paperless-ng)

Die Dokumentensuche im Windows Dateiexplorer hingegen ist mittlerweile in der Lage Dokumente in einem Ordner effizient zu indizieren und auch anhand deren Inhalt zu durchforsten.
Daher habe ich für meine aktuellen Belange keinen Bedarf an weiteren Tools.
Ich habe alle Dateien in einem einzigen Ordner (sowohl einem analogen Ordner, also auch einem Windows Ordner).
Suche ich nach einem Dokument, so genügt es, die Schlagworte in die Suchleiste des Dateiexplorers einzugeben.
Eine Auflistung aller Dateien mit den entsprechenden Schlagworten wird dann angezeigt.
Durch die fortlaufende Nummerierung der Dokumente ist es jederzeit möglich auch das analoge Original im Aktenordner schnell ausfindig zu machen.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/archiving/WindowsSuche.png" title="Suche nach Dokumenten mit der Suche im Datei Explorer" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Hier suche ich nach der Rechnung meiner Tastatur und bekomme prompt das passende Dokument angezeigt
</div>

### Und was ist mit der Cloud?

Da es sich technisch gesehen nur um einen Ordner mit pdf Dokumenten handelt funktioniert das ganze auch mit jedem Cloudsystem.
Vorrausgesetzt natürlich die Cloudanwendung kann auch die Metadaten der Dokumente indizieren um nach Dokumenten zu suchen.

Ich habe den betreffenden Ordner einfach über das entsprechende Desktop-Tool meines Cloudanbieters synchronisiert.

So habe ich immer eine lokale Kopie auf meinem Rechner und zudem automatisierte Cloud-Backups.

Dadurch habe ich jederzeit und weltweit Zugriff auf alle meine Dokumente.
Auch die Suche nach Schlagworten funktioniert bspw. über die Android App meines Cloudanbieters einwandfrei.

> Ob man solche vertraulichen Dokumente mit seinem Cloudanbieter teilen möchte ist natürlich eine ganz andere Frage.
> Sebstverständlich könnte man das auch ein selbstgehostetes Cloud System realisieren.
> Dieses sollte dann aber auf einem gemieteten Rechenzentrum laufen, sodass lokale Kopie und Server räumlich getrennt sind.



