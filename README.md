# Track Viewer – Video Overlay Website

Ein kleines Browser-Tool, das **FIT- und GPX-Dateien** (Radfahren, Garmin, Wahoo & Co.) einliest, auswertet und daraus **Overlays als PNG** erzeugt, etwa für Endcards, Instagram-Beiträge oder als Seitenleiste in einem Video.

Das Tool besteht aus **einer einzigen HTML-Datei** (`fit-viewer.html`). Es gibt keinen Server und kein Konto. Deine Dateien werden **nur lokal im Browser** verarbeitet und nirgendwohin hochgeladen.

> ## ⚠️ Hinweis: Vibe-Coding-Projekt
> Dieses Projekt ist **„vibe-coded“**: Es wurde von einem Programmier-Anfänger gemeinsam mit einer KI (Claude von Anthropic) in einem Dialog entwickelt.
>
> - **Es kann ungenau oder fehlerhaft sein.** Nicht alles wurde unabhängig überprüft, vieles wurde nur in einer simulierten Umgebung getestet, nicht auf allen Geräten und Browsern.
> - **Berechnete Werte können von deinem Gerät oder von Plattformen wie Garmin Connect und Strava abweichen**, besonders bei Höhenmetern, Bewegungszeit und Kalorien (siehe [Bekannte Einschränkungen](#bekannte-einschränkungen)).
> - **Prüfe wichtige Zahlen selbst**, bevor du sie veröffentlichst.
> - Die Nutzung erfolgt auf eigene Verantwortung, es gibt keine Gewähr.

---

## Was kann das Tool?

Das Tool hat links eine Seitenleiste (Upload und Quicklook) und rechts drei Reiter.

### Rohdaten
- Alle Messpunkte als Tabelle, mit frei wählbarem Zeilenbereich (maximal 1000 Zeilen gleichzeitig)
- **CSV-Download** aller Zeilen

### Fullscreen
Ein Overlay in voller Bildgröße, gedacht für Endcards und Instagram-Beiträge.
- Zusammenfassung eines Zeitraums per **Uhrzeit**, **Zeit nach Start** oder **Kilometermarke** (von/bis)
- Strecke, Höhenmeter, Bewegungszeit, Pause, Gesamtzeit, Tempo (Ø/Max), Puls (Ø/Max), Leistung, Kadenz, Kalorien
- Formate **16:9**, **1:1** und **9:16**, Auflösung 720p bis 2160p, optional transparenter Hintergrund
- **Layout-Schema mit Drag & Drop**: bis zu 3 Hauptfelder, bis zu 4 Zeilen, Felder ein- und ausblenden
- Eigene Feldnamen, Titel und „Summe bis Vortag“ (Tageswerte der Vortage werden von Hand eingetragen)
- Export als **PNG**

### Seitenleiste
Ein Overlay für den linken oder rechten Rand eines Videos, das den Stand **vom Start bis zu einem gewählten Zeitpunkt** zeigt.
- Breite **Schmal (1/5)**, **Normal (1/4)** oder **Breit (1/3)**
- Zeitpunkt per **Uhrzeit**, **Zeit nach Start** oder **Kilometermarke**
- Startzustand: alle Werte 0, Herzfrequenz „-“
- Layout-Schema mit 7 Zeilen und höchstens 2 Feldern nebeneinander (bei „Schmal“ 1)
- Eigene Überschrift, eigene Feldnamen und „Summe bis Vortag“ (grau neben dem Wert)
- Export als **PNG** in voller Bildgröße mit transparentem Hintergrund, zum Drüberlegen im Schnittprogramm

## So benutzt du es

1. Datei `fit-viewer.html` im Browser öffnen (oder die gehostete Seite aufrufen).
2. Links eine **FIT- oder GPX-Datei** auswählen oder hineinziehen.
3. Im Reiter **Fullscreen** oder **Seitenleiste** Zeitraum bzw. Zeitpunkt wählen, Layout anpassen und das **PNG herunterladen**.

## Technik und Datenschutz

- Eine einzige HTML-Datei mit reinem JavaScript, ohne Build-Schritt
- Eigener FIT-Parser (Messpunkte sowie Session- und Lap-Daten) und GPX-Parser
- Externe Bibliotheken, jeweils mit fester Version:
  - [SortableJS](https://sortablejs.github.io/Sortable/) 1.15.2 für Drag & Drop
  - [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 für den PNG-Export
- **Keine Datenübertragung:** Deine FIT-/GPX-Dateien bleiben im Browser.
- Downloads nutzen den normalen Browser-Download. In der Claude-Umgebung, in der die Seite entwickelt wird, läuft er zusätzlich über die Plattform-Funktion.

## Bekannte Einschränkungen

- **Höhenmeter** werden mit einer Schwelle von 3 m berechnet (Messrauschen wird ignoriert). Bei der ganzen Aktivität nutzt das Tool die Werte des Geräts, sofern vorhanden.
- **Kalorien** speichert das Gerät nur pro Runde und gesamt. Für Teilzeiträume werden sie anteilig **geschätzt**.
- **Bewegungszeit** zählt Zeit mit mindestens 1 km/h. Andere Plattformen rechnen anders.
- Unterstützt werden nur **FIT und GPX** (kein TCX oder KML).
- Das Layout wird nicht dauerhaft gespeichert, es gilt nur, solange die Seite geöffnet ist.
- Die Seitenleiste exportiert bisher nur ein **Standbild**, kein laufendes Overlay.

## Geplant

- Diagramm mit Zeitregler
- Live-Overlay synchron zum Video und Export als WebM mit Transparenz
- Layout speichern, Import und Export des Layouts
- Mehrere Dateien auf einmal, automatische Summen über mehrere Tage
- Design-Presets und eigene Farben

## Change Index

> Die Datumsangaben vor dem 7. Oktober 2026 wurden nachträglich zugeordnet und können um einen Tag abweichen.

### 2026-10-07
- **Seitenleiste:** neuer Reiter mit Overlay für den Rand eines Videos
  - Position links oder rechts, Breite Schmal (1/5), Normal (1/4), Breit (1/3)
  - Zeitpunkt per Uhrzeit, Zeit nach Start oder Kilometermarke
  - Layout-Schema mit 7 Zeilen, höchstens 2 Felder nebeneinander (bei Schmal 1)
  - „Summe bis Vortag“ für Strecke, Anstieg, Kalorien und Zeiten
  - Startzustand: alle Werte 0, Herzfrequenz „-“
  - PNG-Export in voller Bildgröße mit transparentem Hintergrund
- **Umbenennung:** Reiter heißen jetzt „Rohdaten“, „Fullscreen“ und „Seitenleiste“
- **Fullscreen:** Auswahl per Kilometermarke (von/bis), „Aktivitätsdauer“ heißt jetzt „Zeit nach Start“
- **Karten:** Beschriftung oben, Wert unten, Karten einer Zeile sind gleich hoch
- Dateinamen der Exporte angepasst (`fullscreen-…`, `seitenleiste-…`)
- Behoben: Kilometereingabe wurde beim Verlassen des Feldes als Zeit umformatiert

### 2026-10-04 bis 2026-10-06
- **Formate** 1:1 und 9:16 für Fullscreen, jedes Format merkt sich sein Layout
- **Layout der Seite:** Seitenleiste mit Upload und Quicklook, drei Reiter am Computer, einspaltig am Handy
- **Layout-Schema mit Drag & Drop** statt Dropdowns, Reihenfolge per Pfeilen, auf dem Handy untereinander
- Hauptfelder (max. 3) und Zeilen 1 bis 4, Fehlermeldung bei zu vielen Hauptfeldern
- Eigene Feldnamen, neues Feld „Gesamtzeit“, Pause als Zusatzzeile
- Zusätzliche Felder: Ø/Max. Leistung, Ø Kadenz, Höchster Punkt
- **Fullscreen-Overlay** erzeugt PNG aus den Werten der Zusammenfassung, mit „Summe bis Vortag“
- Gerätewerte (Session) werden bei der ganzen Aktivität bevorzugt
- Kalorien aus Session- und Lap-Daten, bei Teilzeiträumen geschätzt
- Behoben: CSV-Button fehlte, wenn die Plattform-Download-Funktion nicht erreichbar war (jetzt Ersatz-Download im Browser)

### 2026-10-03
- **Erste Version („Track Viewer“):** FIT-Datei laden, Messpunkte als Tabelle anzeigen
- **GPX-Unterstützung**
- **CSV-Download**
- Auswählbarer Zeilenbereich (max. 1000 Zeilen) mit Hilfe-Tooltip
- **Zusammenfassung eines Zeitraums** per Uhrzeit oder Aktivitätsdauer (Strecke, Höhenmeter, Tempo, Puls, Leistung, Kadenz)
- Zeiteingabe ohne Doppelpunkte für die iPhone-Zahlentastatur
- Behoben: Upload-Bereich wurde zerrissen dargestellt

## Lizenz

Noch nicht festgelegt.
