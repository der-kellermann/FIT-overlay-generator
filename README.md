# OverlayUnplugged – Video Overlay Website

> Früher „Track Viewer“. Die Datei heißt vorerst weiter `fit-viewer.html`.

Ein kleines Browser-Tool, das **FIT- und GPX-Dateien** (Radfahren, Garmin, Wahoo & Co.) einliest, auswertet und daraus **Overlays als PNG, PNG-Sequenz oder MOV-Video** erzeugt, etwa für Endcards, Instagram-Beiträge oder als Seitenleiste in einem Video.

Das Tool besteht aus **einer einzigen HTML-Datei** (`fit-viewer.html`) mit Startseite und App. Es gibt keinen Server und kein Konto. Deine Dateien werden **nur lokal im Browser** verarbeitet und nirgendwohin hochgeladen.

> ## ⚠️ Hinweis: Vibe-Coding-Projekt
> Dieses Projekt ist **„vibe-coded“**: Es wurde von einem Programmier-Anfänger gemeinsam mit einer KI (Claude von Anthropic) in einem Dialog entwickelt.
>
> - **Es kann ungenau oder fehlerhaft sein.** Nicht alles wurde unabhängig überprüft, vieles wurde nur in einer simulierten Umgebung getestet, nicht auf allen Geräten und Browsern.
> - **Berechnete Werte können von deinem Gerät oder von Plattformen wie Garmin Connect und Strava abweichen**, besonders bei Höhenmetern, Bewegungszeit und Kalorien (siehe [Bekannte Einschränkungen](#bekannte-einschränkungen)).
> - **Prüfe wichtige Zahlen selbst**, bevor du sie veröffentlichst.
> - Die Nutzung erfolgt auf eigene Verantwortung, es gibt keine Gewähr.

---

## Was kann das Tool?

Beim Öffnen erscheint eine **Startseite** mit Kurzinfos, „Zur App“ führt in die App. Die App hat links eine **Seitenleiste** (Upload und Quicklook, ein- und ausklappbar, dazu der Knopf „Rohdaten ansehen“) und rechts drei Reiter: Fullscreen, Seitenleiste und Data-Viewer. Oben rechts wechselt ein Schalter zwischen **automatisch, hell und dunkel**, das Zahnrad daneben öffnet die **Einstellungen**.

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
- Zeitpunkt per **Uhrzeit**, **Zeit nach Start** oder **Kilometermarke**; beim Wechsel der Angabe wird der eingestellte Bereich **umgerechnet** und nicht zurückgesetzt
- Startzustand: alle Werte 0, Herzfrequenz „-“
- Layout-Schema mit 7 Zeilen und höchstens 2 Feldern nebeneinander (bei „Schmal“ 1)
- Eigene Überschrift, eigene Feldnamen und „Summe bis Vortag“ (grau neben dem Wert)
- **Zeitvorschau mit Regler**: zeigt den Verlauf im gewählten Zeitbereich, mit Abspielen. Sie nutzt dieselbe Zeichenroutine wie der Export.
- **Export als Bildfolge oder Video, komplett offline und ohne Bibliothek**, jeweils mit transparentem Hintergrund (Bildrate 1 fps bis 60 fps beim Video):
  - **PNG-Sequenz (ZIP)**: immer 1 Bild pro Sekunde, mit Anleitung (`LIESMICH.txt`)
  - **MOV „Animation“ (QuickTime RLE)**: verlustfrei mit Transparenz, schneller zu erzeugen
  - **MOV aus PNG-Bildern**: Bilder in einem MOV-Container
  - Zu jeder Option gibt es Vor- und Nachteile und einen Info-Tooltip, wie man sie im Schnittprogramm benutzt. Getestet mit DaVinci Resolve.
- Einzelnes **PNG** in voller Bildgröße wie bisher

### Design-Presets
Ein gemeinsamer Bereich in den Reitern Fullscreen und Seitenleiste (beide zeigen dieselbe Wahl). Ein Look ändert Form, Schrift und Farben der Overlays, in der Vorschau und in allen Exporten.
- **Classic** (wie bisher), **Modern** (Schrift schwebt, dunkler Verlauf), **Edgy** (schräge Ecke, Rahmen in Akzentfarbe), **Fancy** (Serifen, Pastell, Papierkarten), **Unplugged** (Pillen wie die Website, Überschrift mit Logo)
- **Eigene Farben:** Akzentfarbe und Deckkraft
- **Eigene Presets** speichern, umbenennen und löschen; sie bleiben im Browser gespeichert

### Einstellungen (Zahnrad)
- **Dezimalzeichen** Punkt oder Komma (Standard: Punkt)
- **Tausendertrennzeichen** aus, Punkt oder Komma (Standard: aus)
- Gilt überall: in der App, in den Vorschauen und in den erzeugten Overlays. CSV-Dateien bleiben unverändert.

### Data-Viewer
Diagramm der geladenen Aktivität mit Zeitregler und Abspielen.
- Wählbare Verläufe (u. a. Kalorien), X-Achse wahlweise Zeit nach Start, Uhrzeit oder Strecke, Glättung 5 s bis 60 s
- Einen Zeitbereich markieren und ihn mit **einem Klick in die Seitenleiste übernehmen**

### Rohdaten (Fenster)
Öffnet über den Knopf „Rohdaten ansehen“ links, schließt per ✕, Klick daneben oder Esc.
- Alle Messpunkte als Tabelle, mit frei wählbarem Zeilenbereich (maximal 1000 Zeilen gleichzeitig)
- **CSV-Download** aller Zeilen

## So benutzt du es

1. Datei `fit-viewer.html` im Browser öffnen (oder die gehostete Seite aufrufen).
2. Auf der Startseite **Zur App** wählen, dann links eine **FIT- oder GPX-Datei** auswählen oder hineinziehen.
3. Im Reiter **Fullscreen** oder **Seitenleiste** Zeitraum bzw. Zeitpunkt wählen, Layout und Design-Preset anpassen.
4. **PNG** (Fullscreen oder Seitenleiste) bzw. **PNG-Sequenz oder MOV** (Seitenleiste) herunterladen und im Schnittprogramm über das Video legen.

## Technik und Datenschutz

- Eine einzige HTML-Datei mit reinem JavaScript, ohne Build-Schritt
- **Schriften** sind eingebettet (auf die nötigen Zeichen gekürzt, Lizenz SIL OFL): [Sora](https://github.com/sora-xor/sora-font) für Überschriften, [Cormorant Garamond](https://github.com/CatharsisFonts/Cormorant) für den Namen, dazu für die Overlay-Looks [Inter](https://github.com/rsms/inter) und [Chakra Petch](https://github.com/cadsondemak/Chakra-Petch)
- Eigener FIT-Parser (Messpunkte sowie Session- und Lap-Daten) und GPX-Parser
- Externe Bibliotheken, jeweils mit fester Version:
  - [SortableJS](https://sortablejs.github.io/Sortable/) 1.15.2 für Drag & Drop
  - [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 für den PNG-Export
- Der **Video-Export** braucht keine Bibliothek: QuickTime-RLE-Encoder, MOV-Container und ZIP-Writer sind selbst geschrieben. Die Ausgabe wurde gegen ffmpeg verglichen (bit-genau).
- **Keine Datenübertragung:** Deine FIT-/GPX-Dateien bleiben im Browser.
- Downloads nutzen den normalen Browser-Download. In der Claude-Umgebung, in der die Seite entwickelt wird, läuft er zusätzlich über die Plattform-Funktion.

## Bekannte Einschränkungen

- **Höhenmeter** werden mit einer Schwelle von 3 m berechnet (Messrauschen wird ignoriert). Bei der ganzen Aktivität nutzt das Tool die Werte des Geräts, sofern vorhanden.
- **Kalorien** speichert das Gerät nur pro Runde und gesamt. Für Teilzeiträume werden sie anteilig **geschätzt**.
- **Bewegungszeit** zählt Zeit mit mindestens 1 km/h. Andere Plattformen rechnen anders.
- Unterstützt werden nur **FIT und GPX** (kein TCX oder KML).
- Das Layout wird nicht automatisch gespeichert. Es lässt sich als **Backup-Datei** sichern und wieder importieren. Die Backup-Dateien tragen vorerst noch den alten Namen „track-viewer“, damit ältere Backups weiter laden. Ab der Beta wird das umbenannt, dann sind ältere Backups nicht mehr kompatibel.
- Der gewählte **Look** wird noch nicht im Layout-Backup mitgesichert.
- Der Look **Fancy** hat bewusst keinen Schatten unter den Karten, weil der PNG-Export ihn verzerrt darstellen würde.
- Im Browser gemerkt werden: hell/dunkel, das Zahlenformat, der gewählte Look und eigene Presets. Sonst wird nichts gespeichert.
- **WebM** wird nicht angeboten: WebM aus dem Browser zeigte in DaVinci Resolve Artefakte und nicht transparente Karten. Browser können kein ProRes erzeugen; der ffmpeg-Befehl dafür steht in der `LIESMICH.txt` der ZIP-Datei.
- Der Video-Export läuft im Browser. Der Tab sollte dabei **im Vordergrund** bleiben, MOV-Dateien sind auf **4 GB** begrenzt, bei großen Exporten warnt das Tool vor dem Speicherbedarf.
- Zeitbereiche in Kilometern werden beim Umrechnen gerundet („Von“ ab-, „Bis“ aufgerundet); hin und her schalten kann den Bereich um ein bis zwei Messpunkte erweitern.

## Geplant

- **Mehrere Dateien** (Mehrtagestouren, unterbrochene Aufzeichnung), automatische „Summe bis Vortag“
- Behandlung zeitlich **überlappender** Dateien
- **Feedback-Link** und GitHub-Link auf der Startseite
- **GitHub-Hosting-Seite** einrichten
- Ab der Beta: Backup-Dateien umbenennen, **keine Kompatibilität** mit älteren Backups
- Presets im Detail gestalten (in der Beta), Look auch im Layout-Backup sichern

## Change Index

> Die Datumsangaben vor dem 7. Oktober 2026 wurden nachträglich zugeordnet und können um einen Tag abweichen.

### alpha_20261009_03 (2026-10-09)
**Hauptfeature: Design-Presets für die Overlays.**
- **Fünf Looks**, die Form, Schrift und Farben ändern: **Classic** (wie bisher), **Modern** (Schrift schwebt, dunkler Verlauf), **Edgy** (schräge Ecke, Rahmen in Akzentfarbe, technische Schrift), **Fancy** (Serifen, Pastell, Papierkarten mit Innenlinie), **Unplugged** (Pillen wie die Website, Überschrift mit Logo)
- Neuer Bereich „Design-Presets“ in den Reitern **Fullscreen** und **Seitenleiste**, beide gespiegelt: eine Wahl gilt für beide
- **Eigene Farben:** Akzentfarbe und Deckkraft, **eigene Presets** speichern, umbenennen und löschen (im Browser gespeichert)
- Gilt für die Vorschau, die Zeitvorschau und alle Exporte (PNG, PNG-Sequenz, MOV)
- Ziffern haben in den neuen Looks eine feste Breite, damit beim Hochzählen nichts springt
- Classic sieht genau aus wie bisher

### alpha_20261009_02 (2026-10-09)
**Animierte Radfahrer-Szene als Vorschau-Hintergrund.**
- **Startseite:** Im Fenster „Seitenleiste“ bei „Was drin steckt“ fährt beim Darüberfahren ein Radfahrer durch die Landschaft (kleines Easter Egg)
- **Zeitvorschau:** Neuer Hintergrund „Radfahrer (animiert)“, damit man sieht, wie die Seitenleiste auf einem Video wirkt. Der Export bleibt unverändert und transparent.
- Behoben: dunkle Ränder an den Beispiel-Fenstern der Startseite
- Die Szene pausiert, wenn sie nicht sichtbar ist, und steht still bei der Systemeinstellung „Bewegung reduzieren“

### alpha_20261009_01 (2026-10-09)
**Neues Logo und Einstellungen für das Zahlenformat.**
- **Neues Logo** (Ring mit Welle) auf der Startseite, in der App-Leiste und als Browser-Icon
- **Einstellungen** (Zahnrad oben rechts): **Dezimalzeichen** (Punkt oder Komma) und **Tausendertrennzeichen** (aus, Punkt oder Komma). Standard: Punkt, kein Tausendertrennzeichen. Die Wahl gilt überall (App, Vorschauen und erzeugte Overlays) und wird im Browser gespeichert. CSV-Dateien bleiben unverändert.
- Zahleneingaben (Summe bis Vortag, Kilometermarken) verstehen beide Schreibweisen
- Behoben: Der Hell/Dunkel-Schalter löste im Data-Viewer einen Fehler aus
- Hinweis: Overlays zeigen jetzt standardmäßig einen Punkt statt eines Kommas als Dezimalzeichen

### alpha_20261008_01 (2026-10-08)
**Neues Aussehen: Das Tool heißt jetzt OverlayUnplugged (früher Track Viewer).**
- **Neues Design-System:** helle Verläufe in Weiß mit hellblauem Akzent, Dunkelmodus in Schwarz bis Dunkelgrau, runde Pillen-Elemente
- **Hell/Dunkel-Schalter** (automatisch, hell, dunkel), merkt sich die Wahl im Browser
- **Neue Startseite** mit Kurzinfos, Beispiel-Animationen und „Zur App“
- **Seitenleiste links ein- und ausklappbar**, Reiter mit gleitendem Marker
- **Rohdaten** öffnen jetzt als Fenster über einen Knopf in der Seitenleiste (der Reiter entfällt)
- **Schriften** Sora und Cormorant Garamond eingebettet (SIL OFL)
- Funktionen, Zahlen und Layout-Backups unverändert

### alpha_20261007_03 (2026-10-08)
**Hauptfeature: Export der Seitenleiste als PNG-Sequenz oder MOV-Video mit Transparenz.**
- **Export** (offline, ohne Bibliothek): PNG-Sequenz als ZIP (1 fps), MOV „Animation“ (QuickTime RLE) und MOV aus PNG-Bildern, jeweils mit Vor- und Nachteilen sowie Info-Tooltip. In DaVinci Resolve getestet.
- **Neuer Reiter „Data-Viewer“** mit Diagrammen (u. a. Kalorienverlauf) und Zeitbereich-Markierung
- **Übernahme des Zeitbereichs** aus dem Data-Viewer in die Seitenleiste mit einem Klick
- **Zeitvorschau mit Regler** in der Seitenleiste, mit Abspielen
- **Umrechnung des Zeitbereichs** beim Wechsel zwischen Uhrzeit, Zeit nach Start und Kilometermarke (Seitenleiste und Fullscreen)
- Optionskarten gleich groß, Vorteile leicht grün, Nachteile leicht rot
- Behoben: Anzeige „-0,00“ im Kilometer-Modus
- Entfernt: der WebM-Prototyp (WebM erwies sich für DaVinci als ungeeignet)

### alpha_20261007_02 (2026-10-07)
- **Lizenz AGPL-3.0-or-later**, Footer mit Version
- **Layout-Backup** (Export/Import) für Fullscreen und Seitenleiste, mit Abgleich der App-Version

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

[GNU Affero General Public License, Version 3 oder später (AGPL-3.0-or-later)](https://www.gnu.org/licenses/agpl-3.0.html). Copyright (C) 2026 der-kellermann.

Die eingebetteten Schriften stehen unter der [SIL Open Font License 1.1](https://openfontlicense.org).
