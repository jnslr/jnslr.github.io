---
layout: page
title: Invoice Creator
description: Progressive Web App zum Erstellen und Verwalten von Rechnungen
img: assets/img/projects/invoicecreator/Editor.png
importance: 4
category: freiberufliche Tätigkeit
---

## Motivation

Zur selbständigen Tätigkeit gehören neben der fachlichen Umsetzung meiner Projekte auch buchhalterische Aufgaben wie beispielsweise das Schreiben von Rechnungen.

Daher war ich auf der Suche nach einem Tool, welches es ermöglicht mit wenigen Klicks eine Rechnung zu erstellen.
Diese sollten wieder *bearbeitbar* abgespeichert werden und natürlich auch optisch einheitlich und ansprechend aussehen.

Entsprechend kristallisierten sich folgende Anforderungen an das Tool heraus:

- Einfach verfügbar und benutzbar
- Speichern der Rechnungen in einem menschenlesbaren Format, optimalerweise auch per .git verwaltbar
- Wechsel auf andere Tools beziehungsweise Konvertierung in andere Formate einfach möglich
- Generieren von ansehnlichen Rechnungen in einheitlichem Design
- Rechtliche Anforderungen müssen erfüllt werden
- Texte sollen individuell anpassbar sein

## Mögliche Lösungen

Die wohl einfachste Lösung wäre natürlich **bestehende Webanwendungen oder Online-Services** zu nutzen. 
Leider hat keines der von mir evaluierten Tools die oben genannten Anforderungen in Gänze erfüllt.
Häufig ist es nicht möglich die Rechnungen in einem nachträglich bearbeitbaren Format abzuspeichern, sprich bei einer notwendigen Änderung müssten alle Informationen erneut angegeben werden.
Auch die Textfelder sind meist vorgegeben und können nur bei wenigen Tools ausreichend individualisiert werden.

Auch **Textverarbeitungsprogramme** wie zum Beispiel Word, LibreOffice oder OpenOffice ermöglichen das einfache Aufsetzen von Rechnungen.
Allerdings sind die Dateiformate nicht in .git verwaltbar und zudem nicht (einfach) menschenlesbar.
Die Formatierung solcher Dokumente gestaltet sich bekanntermaßen als schwierig.
Und auch die Templating Funktionen, das heißt eine Änderung der *Vorlage* müsste in allen bisher geschriebenen Rechnungen angepasst werden und ist eher aufwändig.

Eine weitere Möglichkeit wäre das Schreiben der Rechnungen in **Markdown**.
Mit Tools wie beispielsweise **Pandoc** kann dann eine ansehnliche **Rechnung als PDF Dokument generiert werden**.
Bei dieser Variante gestaltet sich vor allem das Templating, welches beispielsweise in *LaTeX* erfolgen kann, als herausfordernd und nicht sehr intuitiv.

Daher habe ich entschieden eine **eigene kleine Anwendung** für dieses Problem zu schreiben.

## Meine Lösung

Der erste Prototyp in Form einer `HTML`-Seite war schnell erzeugt.
Durch die Verwendung von **Bootstrap** als CSS Framework und **Vue.js** zum dynamischen Anzeigen beziehungsweise Bearbeiten der Daten konnte die Anwendung in kurzer Zeit realisiert werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/invoicecreator/Editor.png" title="Editor" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Bearbeiten einer Rechnung in der fertigen Anwendung
</div>

Mit der [Native File System API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) kann auch eine einfache Website wie diese auf das native Dateisystem des Rechners zugreifen.
Entsprechend können erstellte Rechnungen vom Dateisystem geöffnet, bearbeitet und gespeichert werden.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/invoicecreator/FileList2.png" title="FileList" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Anzeige der Rechnungen vom Dateisystem in der Anwendung
            </div>
        </div></div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/invoicecreator/FileExplorer2.png" title="FileExplorer" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Speichern der Rechnungen auf dem Dateisystem
            </div>
        </div></div>
    </div>
</div>

Die erzeugten Rechnungen werden als JSON Datei auf dem Rechner abgelegt und können auch im Nachhinein wieder geladen und bearbeitet werden. 
Bevor eine Datei gespeichert wird, werden die Daten validiert, sodass keine fehlerhaften Konfigurationen auf dem Rechner gespeichert werden können.

Die JSON Dateien werden in folgendem Format gespeichert:

```json
{
  "customer": {
    "name": "Hans Wurst",
    "company": "TestComany",
    "address": "Teststraße 1",
    "city": "12345 Bielefeld"
  },
  "invoice": {
    "inv_number": "1",
    "inv_date": "2022-12-28",
    "del_date": "2022-12-27"
  },
  "items": [
    {
      "description": "Artikelbezeichung 1",
      "quantity": 1,
      "cost": "240.00"
    },
    {
      "description": "Stundenleistung\nMit Multiline Beschreibung",
      "quantity": 4,
      "cost": "80.00"
    }
  ]
}
```

Das Speichern von Nutzereinstellungen wird über eine [IndexedDB](https://web.dev/indexeddb/) umgesetzt.
Jeder moderne Webbrowser ermöglicht es Webseiten, Daten in einem abgeschotteten Datenbankbereich persistent zu Lesen und zu Schreiben.

Entsprechend kann hier jeder Nutzer seine persönlichen Daten hinterlegen, ohne dass zusätzliche Tools/Bibliotheken oder ähnliches benötigt werden.
Diese Nutzereinstellungen werden anschließend in der Fußzeile jeder Rechnung automatisch eingeblendet.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/invoicecreator/Settings2.png" title="Settings" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Modifizieren der Einstellungen, welche in der Indexed DB hinterlegt sind.
</div>

Zum Versenden der Rechnung an den Kunden kann diese einfach über den Druckdialog als PDF Datei gespeichert/exportiert werden.

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/projects/invoicecreator/PrintDialog.png" title="PrintDialog" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Druckdialog zum PDF Export
</div>


Schlussendlich habe ich die finale Version auf [https://jnslr.github.io/InvoiceCreator/](https://jnslr.github.io/InvoiceCreator/) veröffentlicht.
Somit ist das Tool jederzeit online verfügbar.

Zusätzlich wurde die Anwendung als [Progressive Web App (PWA)](https://whatpwacando.today/) aufgebaut. 
Entsprechend kann das Tool auch für die *offline* Verwendung auf dem Desktop oder mobilen Endgeräten installiert werden und ist kaum mehr von einer *nativen Anwendung* zu unterscheiden.

## Fazit

Ich habe die App ist in dieser Form nun schon seit circa 2 Jahren in Verwendung.
Bisher hat Sie alle meine Anforderungen an ein Rechnungstool erfüllt.
Kundenrechnungen exportiere ich als PDF und verschicke diese. Die "Rohdaten" sind weiterhin auf dem Rechner abgelegt, sodass die Rechnung auch nachträglich wieder geöffnet und bearbeitet werden kann.

Durch den einfachen Aufbau als Website können weitere benötigte Funktionen jederzeit einfach und schnell nachgereicht werden.

Selbstverständlich ist das Tool recht stark auf meine persönlichen Bedürfnisse zugeschnitten, weshalb der Nutzen für andere Anwender wohl recht beschränkt ist.

Auch die Benutzerführung zeigt noch deutliches Verbesserungspotential.

Zwar kann die PWA auch auf Mobilgeräten installiert werden, allerdings ist Sie auf solchen nicht funktional, da vor allem die FileSystemAPI Funktionen nicht auf Mobilgeräten getestet wurden.
Der Nutzen eines Rechnungstool auf Mobilgeräten ist sicherlich auch nicht allzu groß, weshalb hier kein Wert auf die Kompatibilität mit Mobilgeräten gelegt wurde.

