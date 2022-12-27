---
layout: page
title: Android App
description: Android App zum Verwalten von Kochrezepten und Erstellen von Einkaufslisten
img: assets/img/projects/cookbook/thumbnail.jpg
importance: 2
category: Sonstiges
---

## Das Problem

Was koche ich heute? Diese Frage stellt sich immer wieder aufs Neue.
Vor allem genervt davon neue Rezepte herauszusuchen, entstand eine Excel Tabelle mit ca. 30 Gerichten, welche ich immer wiederkehrend gekocht habe.
So konnte zumindest die Zeit zur Auswahl der Gerichte deutlich reduziert werden.

Trotzdem mussten weiterhin für jeden Einkauf die Gerichte herausgesucht und die benötigten Zutaten in eine Einkaufsliste überführt werden.

Die Überlegung, auch diese Prozesse in Excel abzubilden mündete schließlich in der Idee eine eigene Android App zu erstellen, welche genau diese Aufgaben übernimmt:
Rezepte verwalten, Rezepte vorschlagen, Rezepte anzeigen und Einkaufslisten erstellen.

> Mit Sicherheit gibt es diese oder ähnliche Apps schon zuhauf. Der Reiz und die Erfahrung eine eigene Anwendung zu schreiben und zu veröffentlichen hat mich allerdings dazu bewogen dennoch die eigene Entwicklung zu starten.

## Die Lösung

Die fertige [Android App](https://play.google.com/store/apps/details?id=lauer.cookbook) ist im Google Playstore veröffentlicht.

Alle Rezepte werden lokal und ohne Cloud Anbindung auf dem Mobiltelefon gespeichert.
Diese können aus der App heraus, beispielsweise per Mail oder als Messenger-Anhang geteilt werden.
Auch das Speichern als Textdatei ist möglich, sodass ein *Backup* aller Einträge durchgeführt werden kann.

Im folgenden werden die wichtigsten Ansichten beziehungsweise Funktionen der Anwendung kurz gezeigt und beschrieben:


### Rezeptübersicht

In der Hauptansicht der App wird die persönliche Rezeptsammlung angezeigt.
Diese kann entweder als *Galerieansicht* mit kleinem Thumbnail der einzelnen Gerichte oder als kompakte Listenansicht erfolgen.
Auch das Suchen von bestimmten Rezepten und Hinzufügen zu einer Einkaufsliste ist direkt möglich.

Zudem kann die Sammlung in dieser Ansicht bearbeitet werden, also neue Rezepte erstellt oder bestehende gelöscht werden.



<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/overview.jpg" title="Rezeptübersicht" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Rezeptübersicht mit Bildern
            </div>
        </div></div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/overviewList.jpg" title="Rezeptübersicht" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Kompakte Rezeptübersicht als Liste
            </div>
        </div></div>
    </div>
</div>

### Rezeptvorschläge

In der "Rezeptvorschläge" Ansicht werden zufällig ausgewählte Rezepte vorgeschlagen.
Mit einem Wischen nach rechts kann der Vorschlag angenommen und zur Einkaufsliste hinzugefügt werden.
Wischen nach links führt zum nächsten Vorschlag.
Die Vorschläge können auch eingegrenzt (gefiltert) werden, beispielsweise wenn gerade ein schnelles Gericht gefragt ist, oder nur vegetarische Gerichte vorgeschlagen werden sollen.

<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/suggestion.jpg" title="Rezeptvorschläge" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Rezeptvorschläge
            </div>
        </div></div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/filter.jpg" title="Filtereinstellungen" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Filtereinstellungen für die Rezeptvorschläge
            </div>
        </div></div>
    </div>
</div>

### Einkaufsliste

Schlussendlich können alle Rezepte in der aktuellen Einkaufsliste angezeigt werden.
Selbstverständlich kann hier auch nochmals die Anzahl an Personen für das jeweilige Gericht abgeändert werden. Die Mengenangaben werden dann entsprechend umgerechnet.

Die Einkaufsliste selbst fasst die einzelnen Zutaten der Rezepte zu einer Liste zusammen. Diese kann beim Einkauf im Supermarkt abgehakt werden.


<div class="row px-4">
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/shoppingList.jpg" title="Rezepte Einkaufsliste" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Rezepte in der Einkaufsliste
            </div>
        </div></div>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <div class="row px-4"> <div class="col">
            {% include figure.html path="assets/img/projects/cookbook/shoppingCart.jpg" title="Einkaufsliste" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div></div>
        <div class="row px-4"> <div class="col">
            <div class="caption">
                Einkaufsliste zum Abhaken
            </div>
        </div></div>
    </div>
</div>


## Technische Umsetzung

### Cordova

Die App wurde als [Apache Cordova](https://cordova.apache.org/) Webapp umgesetzt.
Dieses Framework erlaubt es *native* Apps mit Webtechnologien zu erstellen.
Vereinfacht gesehen besteht die App aus einer einzigen Webview, die eine intern gehostete Seite anzeigt.
Um native Funktionen nutzen zu können, kann die App mit sogenannten Plugins erweitert werden.

Hier kamen folgende Plugins zum Einsatz:
  - *Camera*: Erlaubt den Zugriff auf Galerie und Kamera, so können Bilder der Rezepte erstellt und in der Datenbank gespeichert werden
  - *Socialsharing*: Ermöglicht das Teilen von Rezepten über die vom Nutzer gewohnten *Teilen* Mechanismen
  - *Intent*: Ermöglicht das Öffnen von geteilten Dateien mit der App, um diese zu importieren
    
    > Dieses Plugin hat die meisten Probleme verursacht, da nicht bei allen Verfahren des Teilens der Mime-Type der Dokumente richtig gesetzt wurde/erhalten blieb.
    > Wurde die App nur zum Öffnen eines bestimmten Mime-Types registriert, so konnte Sie teilweise nicht verwendet werden um die entsprechenden Dateien zu öffnen.
    > Daher wurde Sie aktuell für jeden Mime-Type ("*/*") registriert, was allerdings nur einen workaround darstellt.

Das Cordova Framework erlaubt es, die App ohne Veränderung auch für IOS oder Windows bereitzustellen.
Die Entwicklung für diese Platformen lag allerdings nicht im Fokus, entsprechend wird die App aktuell nur für Android bereitgestellt.

Da zudem fast ausschließlich Webtechnologien zum Einsatz kommen, wäre es auch möglich die App als Website oder als progressive web app (PWA) bereitzustellen.
Hier müssten lediglich die nativen Cordova Plugins durch die jeweiligen Web-Versionen ersetzt werden.
Zum Zeitpunkt der Entwicklung der App waren PWA's noch nicht so weit fortgeschritten, mittlerweile sollte dies kein Problem mehr darstellen.



### Frontend

Im Frontend kommt Bootstrap als CSS Framework zum Einsatz.
Um das dynamische Frontend zu realisieren wurde zudem Vue.js verwendet.

Das Modul [vue2-hammer](https://github.com/bsdfzzzy/vue2-hammer) erlaubt die Verwendung von Touch-Bindings, wie sie beispielsweise beim Scrollen und Swipen eingesetzt werden.

Mit Hilfe von [vue-virtual-scroller](https://github.com/Akryum/vue-virtual-scroller) können lange Listen (hier das komplette Rezeptbuch mit Bildern) dynamisch gerendert werden, ohne dass das komplette Rezeptbuch im Speicher vorgeladen werden muss.
Diese Bibliothek trägt maßgeblich zur guten Performance der App bei.


### Datenbank

Als Datenbank wird IndexedDB verwendet.
Vorteil hierbei ist, dass es sich um eine reine Webtechnologie handelt:
Jede Website kann eine eigene IndexedDB anlegen. Somit kann der Datenbankteil der App auch bei einer möglichen Migration ins Web weiter verwendet werden.

Die IndexedDB funktioniert auch in der *WebView* der Cordova App problemlos. Die Daten bleiben auch bei einem Update der App erhalten.

Nachteilig bei der Verwendung von IndexedDB ist, dass die Datenbank keine Relationen unterstützt.
Entsprechend mussten alle Relationen zwischen Datenbanktabellen selbst abgebildet werden.
Hier werden nur 3 Tabellen verwendet:
  - *Recipes*: Zum Speichern der Rezepte (Zutaten, Zubereitungsschritte, Metadaten) als JSON Objekt
  - *GroceryLists*: Speichert alle Einkaufslisten, also welche Rezepte für wie viele Personen hinzugefügt wurden
  - *Images*: Bilder werden mit einer eindeutigen ID als *DataURL* (Base64 kodierter String) in der Datenbank gespeichert. Die Bild-ID wird mit den Metadaten eines Rezepts verknüpft um so die Zuordnung Bild rarr; Rezept zu realisieren. Bilder werden vor dem Speichern komprimiert um die Datenmengen zu reduzieren.
    > Meine aktuelle Rezeptsammlung umfasst 52 Rezepte, zum Großteil mit Bildern. Beim Export der kompletten Datenbank wird eine ~10MB große Datei erzeugt. Der Export gelingt in unter 5 Sekunden. 