# Track Viewer – Video Overlay Website

Ein kleines Browser-Tool, das **FIT- und GPX-Dateien** (Radfahren, Garmin, Wahoo & Co.) einliest, auswertet und daraus **Overlays als PNG** erzeugt, etwa für Endcards, Instagram-Beiträge oder als Seitenleiste in einem Video.

Das Tool besteht aus **einer einzigen HTML-Datei** (`fit-viewer.html`). Es gibt keinen Server und kein Konto. Deine Dateien werden **nur lokal im Browser** verarbeitet und nirgendwohin hochgeladen.

**Aktuelle Version:** `alpha_20261007_02` (steht auch im Footer der Seite) · **Lizenz:** [AGPL-3.0](LICENSE)

> ## ⚠️ Hinweis: Vibe-Coding-Projekt
> Dieses Projekt ist **„vibe-coded“**: Es wurde von einem Programmier-Anfänger gemeinsam mit einer KI (Claude von Anthropic) in einem Dialog entwickelt.
>
> - **Es kann ungenau oder fehlerhaft sein.** Nicht alles wurde unabhängig überprüft, vieles wurde nur in einer simulierten Umgebung getestet, nicht auf allen Geräten und Browsern.
> - **Berechnete Werte können von deinem Gerät oder von Plattformen wie Garmin Connect und Strava abweichen**, besonders bei Höhenmetern, Bewegungszeit und Kalorien (siehe [Bekannte Einschränkungen](#bekannte-einschränkungen)).
> - **Prüfe wichtige Zahlen selbst**, bevor du sie veröffentlichst.
> - Die Nutzung erfolgt auf eigene Verantwortung, es gibt keine Gewähr.

---

## Was kann das Tool?

Das Tool hat links eine Seitenleiste (Upload und Quicklook) und rechts drei Reiter: **Fullscreen**, **Seitenleiste** und **Rohdaten**. Am Handy steht alles untereinander.

### Fullscreen
Ein Overlay in voller Bildgröße, gedacht für Endcards und Instagram-Beiträge.
- **Zusammenfassung eines Zeitraums** (einklappbar): Auswahl per **Uhrzeit**, **Zeit nach Start** oder **Kilometermarke** (von/bis), mit Kärtchen für Strecke, Höhenmeter, Bewegungszeit, Pause, Tempo, Puls, Leistung, Kadenz und Kalorien
- **Overlay-Vorschau direkt darunter**, danach die Einstellungen
- Formate **16:9**, **1:1** und **9:16**, Auflösung 720p bis 2160p, optional transparenter Hintergrund
- **Layout-Schema mit Drag & Drop**: bis zu 3 Hauptfelder und 4 Zeilen, gestrichelte leere Plätze zeigen die maximale Anzahl (pro Zeile 3 Felder bei 16:9 und 1:1, 2 bei 9:16)
- Eigene Feldnamen, Titel und „Summe bis Vortag“ (Werte der Vortage trägst du von Hand ein)
- **Layout sichern (Backup):** im Browser speichern oder als Datei exportieren und importieren
- Export als **PNG**

### Seitenleiste
Ein Overlay für den linken oder rechten Rand eines Videos, das die Werte eines **gewählten Zeitraums** zeigt.
- **Zeitraum von/bis** per Uhrzeit, Zeit nach Start oder Kilometermarke, einklappbar und mit denselben Zusammenfassungskärtchen wie im Fullscreen. Standard ist die ganze Aktivität, vorne abschneiden ist möglich. Die Auswahl ist **unabhängig** vom Fullscreen-Reiter.
- Startzustand („Von 0 bis 0“): alle Werte 0, Herzfrequenz „-“
- Breite **Schmal (1/5)**, **Normal (1/4)** oder **Breit (1/3)**, links oder rechts
- **Overlay-Vorschau oben**, Einstellungen und Layout darunter
- Layout-Schema mit 7 Zeilen und gestrichelten Plätzen: höchstens 2 Felder nebeneinander (bei „Schmal“ 1)
- Eigene Überschrift, eigene Feldnamen und „Summe bis Vortag“ (grau neben dem Wert)
- **Layout sichern (Backup)** wie im Fullscreen, mit eigenem Speicher
- Export als **PNG** in voller Bildgröße mit transparentem Hintergrund, zum Drüberlegen im Schnittprogramm

### Rohdaten
- Alle Messpunkte als Tabelle, mit frei wählbarem Zeilenbereich (maximal 1000 Zeilen gleichzeitig)
- **CSV-Download** aller Zeilen

## Layout-Backup

In beiden Overlay-Reitern gibt es unter dem Layout-Schema den Bereich **„Layout sichern (Backup)“**. Zu jeder Funktion gibt es ein Info-Symbol **(i)** mit einer kurzen Erklärung.

- **Im Browser speichern / Gespeichertes laden:** Das Layout liegt im Speicher des Browsers (`localStorage`) und wird beim nächsten Öffnen automatisch geladen. Das gilt nur für das jeweilige Gerät und den jeweiligen Browser und geht verloren, wenn die Browserdaten gelöscht werden.
- **Als Datei exportieren:** JSON-Datei mit Datum und Uhrzeit im Namen, z. B. `trackviewer-layout-fullscreen_2026-10-07_11-52-03.json`. So lassen sich mehrere Stände aufheben und Layouts auf andere Geräte mitnehmen.
- **Datei importieren:** Nur Backups des passenden Reiters werden angenommen. Defekte oder fremde Dateien werden abgelehnt, Inhalte werden bereinigt.
- **Gesichert wird:** Layout, Feldnamen, Format bzw. Position und Breite, Auflösung (Fullscreen zusätzlich Hintergrund und Pause-Zusatzzeile).
- **Nicht gesichert wird:** Titel, Werte und „Summe bis Vortag“. Es werden keine Messdaten gespeichert.
- Ist der Browser-Speicher gesperrt (z. B. im privaten Modus), bleiben Export und Import nutzbar.

### Versions-Abgleich
Jedes Backup enthält die Version der Seite, mit der es erstellt wurde. Passt sie nicht zur geladenen Seite, erscheint eine **Fehlermeldung**: Das Layout wird so gut wie möglich angewendet, es kann aber sein, dass nicht alles wiederhergestellt wird. Die Meldung nennt die **GitHub-Version, die du für dieses Backup nutzen solltest** (bei einem älteren Backup die ältere Version, bei einem neueren Backup die neuere).

## Versionen

Das Schema lautet **`alpha_JJJJMMTT_NN`**:
- `JJJJMMTT` ist das Datum des letzten GitHub-Uploads (ISO 8601)
- `NN` ist die laufende Nummer der Uploads an diesem Tag (`01`, `02`, …)

Die Version steht im Footer der Seite und in den Layout-Backups. Zu jeder Version gehört bei GitHub ein **Release mit gleichnamigem Tag**, damit sich ein älterer Stand leicht wiederfinden lässt (Repository → Releases).

## So benutzt du es

1. Datei `fit-viewer.html` im Browser öffnen (oder die gehostete Seite aufrufen).
2. Links eine **FIT- oder GPX-Datei** auswählen oder hineinziehen.
3. Im Reiter **Fullscreen** oder **Seitenleiste** den Zeitraum wählen, das Layout anpassen und das **PNG herunterladen**.
4. Optional: das Layout im Browser speichern oder als Datei exportieren.

## Technik und Datenschutz

- Eine einzige HTML-Datei mit reinem JavaScript, ohne Build-Schritt
- Eigener FIT-Parser (Messpunkte sowie Session- und Lap-Daten) und GPX-Parser
- Externe Bibliotheken, jeweils mit fester Version:
  - [SortableJS](https://sortablejs.github.io/Sortable/) 1.15.2 für Drag & Drop
  - [html2canvas](https://html2canvas.hertzen.com/) 1.4.1 für den PNG-Export
- **Keine Datenübertragung:** Deine FIT-/GPX-Dateien bleiben im Browser. Im Browser-Speicher liegt nur das Layout.
- Downloads nutzen den normalen Browser-Download. In der Claude-Umgebung, in der die Seite entwickelt wird, läuft er zusätzlich über die Plattform-Funktion.

## Bekannte Einschränkungen

- **Höhenmeter** werden mit einer Schwelle von 3 m berechnet (Messrauschen wird ignoriert). Bei der ganzen Aktivität nutzt das Tool die Werte des Geräts, sofern vorhanden.
- **Kalorien** speichert das Gerät nur pro Runde und gesamt. Für Teilzeiträume werden sie anteilig **geschätzt**.
- **Bewegungszeit** zählt Zeit mit mindestens 1 km/h. Andere Plattformen rechnen anders.
- Unterstützt werden nur **FIT und GPX** (kein TCX oder KML).
- Der **Browser-Speicher** gilt nur pro Gerät und Browser und kann gelöscht werden oder gesperrt sein. Als Sicherung dient der Export als Datei.
- Backups aus einer **anderen Version** der Seite können unvollständig wiederhergestellt werden.
- Die Seitenleiste exportiert bisher nur ein **Standbild**, kein laufendes Overlay.

## Geplant

- Diagramm mit Zeitregler
- Live-Overlay synchron zum Video und Export als WebM mit Transparenz
- Mehrere Dateien auf einmal, automatische Summen über mehrere Tage
- Design-Presets und eigene Farben
- Weniger Scrollen im Rohdaten-Reiter

## Change Index

> Die Datumsangaben vor dem 7. Oktober 2026 wurden nachträglich zugeordnet und können um einen Tag abweichen. Versionsnummern gibt es seit `alpha_20261007_01`.

### alpha_20261007_02 – 2026-10-07
- **Lizenz:** AGPL-3.0-or-later, Lizenz-Hinweis am Anfang der HTML-Datei, LICENSE-Datei im Repository
- Footer nennt die Lizenz

### alpha_20261007_01 – 2026-10-07
- **Layout-Backup** für Fullscreen und Seitenleiste, jeweils getrennt:
  - Im Browser speichern und laden, beim Öffnen wird ein gespeichertes Layout automatisch geladen
  - Export als JSON-Datei mit Datum und Uhrzeit im Namen
  - Import mit Prüfung (richtiger Reiter, lesbare Datei, keine neuere Dateiversion) und Bereinigung der Inhalte
  - Gesichert werden Layout, Feldnamen, Format/Position/Breite und Auflösung, nicht Titel, Werte oder „Summe bis Vortag“
- **Versionierung:** Footer mit Version, Schema `alpha_JJJJMMTT_NN`
- **Versions-Abgleich** beim Laden eines Backups: Fehlermeldung mit Hinweis auf die passende GitHub-Version, das frühere Format `alpha_TTMMJJJJ` wird weiter erkannt
- **Info-Tooltips (i)**- Eigener FIT-Parser (Messpunkte sowie Session- und Lap-Daten) und GPX-Parser
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
- Weniger Scrollen im Rohdaten-Reiter

## Change Index

> Die Datumsangaben vor dem 7. Oktober 2026 wurden nachträglich zugeordnet und können um einen Tag abweichen.

### 2026-10-07
- **Reiter-Reihenfolge:** Fullscreen, Seitenleiste, Rohdaten. Fullscreen ist beim Öffnen aktiv.
- **Seitenleiste:** Zeitraum von/bis wie im Fullscreen (unabhängige Auswahl, vorne abschneiden möglich), einklappbar, mit Zusammenfassungskärtchen
- **Seitenleiste:** Vorschau steht oben, Einstellungen, Layout und Werte darunter
- **Fullscreen:** Zusammenfassung kompakter und einklappbar, Vorschau direkt darunter, Einstellungen danach
- **Layout-Schema:** gestrichelte leere Plätze zeigen die maximale Anzahl pro Zeile (Fullscreen: 3 Hauptfelder, pro Zeile 3/3/2 je nach Format; Seitenleiste: 2 bzw. 1), Fehlermeldung bei Überschreitung
- Auswahlfeld „Angabe als“ nicht mehr abgeschnitten, einheitliche Höhe der Eingabefelder
- **Seitenleiste:** Startzustand („Von 0 bis 0“) mit Nullwerten und „-“ bei der Herzfrequenz
- **Seitenleiste:** Breite Schmal (1/5), Normal (1/4), Breit (1/3)
- **Seitenleiste:** neuer Reiter mit Overlay für den Rand eines Videos (links/rechts, Layout-Schema mit 7 Zeilen, „Summe bis Vortag“, PNG mit transparentem Hintergrund)
- **Umbenennung:** Reiter heißen „Fullscreen“ und „Seitenleiste“ (Dateinamen der Exporte entsprechend)
- **Fullscreen:** Auswahl per Kilometermarke (von/bis), „Aktivitätsdauer“ heißt jetzt „Zeit nach Start“
- **Karten:** Beschriftung oben, Wert unten, Karten einer Zeile sind gleich hoch
- Behoben: Kilometereingabe wurde beim Verlassen des Feldes als Zeit umformatiert

### 2026-10-04 bis 2026-10-06
- **Formate** 1:1 und 9:16 für Fullscreen, jedes Format merkt sich sein Layout
- **Layout der Seite:** Seitenleiste mit Upload und Quicklook, Reiter am Computer, einspaltig am Handy
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

# Lizenz

Dieses Projekt steht unter der **GNU Affero General Public License v3.0 oder neuer** (AGPL-3.0-or-later), siehe [LICENSE](LICENSE).

Kurz gesagt: Du darfst das Tool nutzen, verändern und weitergeben. Wenn du eine veränderte Version weitergibst oder als Dienst im Netz anbietest, musst du sie ebenfalls unter der AGPL mit Quellcode zur Verfügung stellen. Das Tool darf also nicht verschlossen werden. Das ist keine Rechtsberatung, maßgeblich ist der Lizenztext.

Die Bibliotheken SortableJS und html2canvas werden von einem CDN geladen und nicht mitgeliefert. Sie stehen unter eigenen Lizenzen (nach meinem Stand jeweils MIT, bitte auf den Projektseiten gegenprüfen).

Copyright (C) 2026 der-kellermann
