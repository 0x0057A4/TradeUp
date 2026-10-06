# Trade Up

Isometrisches Wirtschafts- und Fabrikaufbau-Spiel im Browser (Three.js, WebGL).

## Stand: Phase 4 – Erste Produktion & Kuriere

- **Phase 1:** Startlevel **Garage** (16 × 48 Kacheln), isometrische Kamera, Hover und Auswahl
- **Phase 2:** Spielfigur mit A*-Pathfinding (die Test-Blöcke wurden in Phase 4 durch den Bau-Modus ersetzt)
- **Phase 3:** Produkt-Layout-Designer als 2D-Fenster über der Garage:
  - Produkt-Raster 4 × 4 (16 Kacheln), 8 Bauteile in Tetris-Formen per Drag & Drop (Maus und Touch)
  - Bauteile drehen, verschieben, entfernen, Rückgängig/Wiederholen
  - Hitze-Berechnung: Bauteile heizen direkt angrenzende Kacheln auf, Kühlkörper kühlen; liegt mehr Hitze auf einem Teil als seine Toleranz, ist es überhitzt (rot)
  - Designs als **Blaupause** speichern (im Browser, bleibt nach dem Neuladen erhalten), laden, umbenennen, duplizieren, löschen
- **Phase 4:** Erste Produktion & Kuriere:
  - **Baumenü** (`B`): Hauptlager (seit Phase 7a: 2 × 2, beliebig viele, jedes weitere 1.500 €), Kiste (1 × 1) und Schrank (2 × 1) als Zwischenlager, Werkbank und Montagetisch (je 2 × 1) mit Vorschau, Drehen und Zugangspfeil; Gebäude, die jemanden einsperren würden, lassen sich nicht bauen
  - **Kuriere** tragen Rohstoffe und Bauteile vom Hauptlager in die Zwischenlager (Grundwert 5 Items pro Gang, Ausrüstung addiert sich: Sackkarre +4, Hubwagen +10) und Fertiges aus den Ausgabefächern zurück; Kurier-Stufen (Hände, Sackkarre, Hubwagen) sind vorbereitet
  - **Arbeiter** holen Material nur aus den verknüpften Zwischenlagern und produzieren: Werkbank = Bauteile aus Metall, Kunststoff, Silizium; Montagetisch = Produkte nach einer Blaupause (überhitzte Blaupausen: 30 % Ausschuss)
  - **Halle bereinigen**: baut alles ab, Maschinen und Items kommen ins Depot; „Aufbau wiederherstellen“ stellt alles zurück
  - Info-Fenster per Klick auf ein Gebäude, Lager-Fenster (`I`), Personal, Spieltempo (`P`, `1`–`3`), automatischer Spielstand im Browser

- **Phase 7b:** Logistik & Lagerlimits:
  - **Importzone** (3 × 2, an einer Hallenwand, die erste ist kostenlos): Rohstoffe bestellen mit Menge und Rhythmus (einmalig, jede Minute, alle 2 / 5 Minuten, täglich 8:00, jede Minute bis Sollmenge). Der Lieferwagen kommt nach 15 s, bezahlt wird beim Abladen; was nicht passt, wird abgewiesen und nicht berechnet. Der Sofort-Einkauf und „automatisch nachkaufen“ im Kontor entfallen.
  - **Exportzone** (2 × 2, die erste ist kostenlos): Ware „Für Aufträge“ geht an einen angenommenen Auftrag, sobald die ganze Menge dort liegt; Ware „Verkaufen“ wird verkauft. Der Abholwagen kommt alle 30 s. Der Knopf „Liefern“ im Kontor entfällt.
  - **Volumen**: Rohstoff und kleines Bauteil 1, 2 × 2-Bauteil 2, 2 × 3-Bauteil 3, Produkt 4. Kiste 10, Schrank 25, Hauptlager 300, Zonen 60. Volle Lager nehmen nichts mehr an, das Band staut sich bis zur Station („Stau – Produktion steht“). Warnung ab 80 % (gelb) und bei 100 % (rot), mit Hinweis im HUD.
  - **Max per Zahl** im Lager-Fenster (Zahl eintippen, Enter): Bänder, Greifarme, Arbeiter und Kuriere liefern nur bis Max.
  - **Smart-Verteiler** (liefert nur dorthin, wo das Ziel am Ende der Strecke Platz hat), **Überlauf-Ventil** (geradeaus, bei vollem Ziel zur Seite), **Mülltonne** (vernichtet, pro Ware einstellbar).
  - Kuriere tragen grundsätzlich 5 Items pro Gang; Ausrüstung und Forschung addieren sich.
  - **Nachtrag:**
    - **Verteiler-Puffer**: Splitter, Smart-Verteiler und Überlauf-Ventil haben ein eigenes kleines Lager von 30 Items; das Info-Fenster zeigt „Puffer: n / 30“ mit den Items darin.
    - **Hauptlager-Regeln** wie beim Schrank: pro Ware ⇣ Annahme, ⇡ Abgabe und Max (Zahl eintippen, ↺ zurück auf Automatik). So lassen sich die 300 Volumen bedarfsgerecht verteilen; abgewiesene Ware geht ins nächste Hauptlager. Nimmt kein Hauptlager eine wartende Ware an, meldet das HUD „kein Lager für …“.
    - **Lager überall anbindbar**: Bänder dürfen ein Lager von allen Seiten anfahren. Kuriere entnehmen und liefern vorn am Pfeil – liegt dort ein Bandteil, ist der Zugang blockiert (Hinweis im Info-Fenster).
    - **Exportzone an der Wand** mit Gittertor; das Tor fährt hoch, wenn der Abholwagen kommt.
    - **Weiterbauen** (`E`) öffnet das Baumenü im Reiter „Bänder“ mit dem Fließband als Werkzeug – genau wie Bau → Bänder → Fließband.

## Spiel starten

**Lokal:** `index.html` per Doppelklick im Browser öffnen. Es wird eine Internetverbindung benötigt, weil Three.js von `unpkg.com` geladen wird.

**Online über GitHub Pages:**
1. Im Repository auf *Settings → Pages* gehen.
2. Unter *Build and deployment* bei *Source* „Deploy from a branch“ wählen.
3. Branch `main` und Ordner `/ (root)` auswählen, speichern.
4. Nach ein bis zwei Minuten ist das Spiel unter `https://0x0057a4.github.io/TradeUp/` erreichbar.

Die leere Datei `.nojekyll` sorgt dafür, dass GitHub Pages die Dateien unverändert ausliefert.

## Steuerung

| Aktion | Eingabe |
|---|---|
| Kachel hervorheben | Maus bewegen |
| Kachel auswählen / abwählen | Linksklick |
| Auswahl aufheben | `Esc` |
| Kamera verschieben | rechte (oder mittlere) Maustaste ziehen, `W A S D`, Pfeiltasten |
| Zoomen | Mausrad |
| Kachel auswählen | Linksklick auf freien Boden (deine Figur „Du“ läuft selbst, wie alle Mitarbeiter) |
| Gebäude-Info öffnen | Linksklick auf ein Gebäude |
| Baumenü öffnen / schließen | Knopf „Bauen“, `B` |
| Gebäude aufstellen | Karte im Baumenü wählen, Linksklick (mit `Shift` mehrere) |
| Gebäude drehen | `R` oder Rechtsklick (ohne zu ziehen) |
| Abriss-Werkzeug | `X`, dann Gebäude anklicken |
| Lager-Fenster | Knopf „Lager“, `I` |
| Pause / Tempo 1×, 2×, 3× | `P`, `1`, `2`, `3` |
| Kamera zu dir („Du“) | `Leertaste` |
| Layout-Designer öffnen / schließen | Knopf in der Infobox, `L`, `Esc` |
| Fließband in die Hand | `F` |
| Bandstück wählen / ganze Bandgruppe wählen | Einfachklick / Doppelklick auf ein Band |
| Gewähltes Band weiterbauen | `E`, dann Ziel anklicken |
| ⇣ Import verknüpfen: Lager, aus dem eine Station ihr Material holt (Station oder Lager gewählt) | `V`, dann das andere Gebäude anklicken |
| ⇡ Export verknüpfen: Lager, in das eine Station ihre Erzeugnisse bringt | `G`, dann das andere Gebäude anklicken |
| Mitarbeiter an eine Station setzen | Mitarbeiter mit gedrückter linker Maustaste auf Werkbank, Montagetisch oder Forschungsstation ziehen (Kuriere werden dabei Arbeiter) |
| Abreißen ohne Werkzeug | `Entf`: ausgewähltes Gebäude bzw. Band (Einzelstück, ganze Gruppe oder Mehrfachauswahl), sonst das, worauf die Maus zeigt |
| Mehrere Teile wählen | `Strg` + Klick auf Gebäude und Bänder (nochmal: wieder heraus), oder mit der linken Maustaste einen Rahmen ziehen (mit `Strg`: dazu) |
| Auswahl kopieren / einfügen | `Strg+C` / `Strg+V`: die Kopie hängt an der Maus, `R` dreht, Klick stellt auf (mit `Shift` mehrmals), `Esc` bricht ab. Kopiert werden Typ, Drehung, Rezept, Lagerregeln, Band-Einstellungen und Verknüpfungen innerhalb der Kopie, kein Inhalt |
| Greifarm-Nehmer / -Geber | Nehmer (roter Ring) holt aus dem Gebäude hinter sich aufs Band, mit Auswahl des Items; Geber (grüner Ring) gibt vom Band in das Gebäude vor sich |
| Testgeld und alles freischalten | Einstellungen (`O`) → Reiter „Entwicklung“ |
| Einstellungen (Tastenkürzel, Grafik) | Knopf „Optionen“, `O` |
| Rezepte (Werkbank und Designer-Entwürfe), 📌 anheften | Knopf „Rezepte“, `Z` |
| Station finden, die eine Ressource herstellt | Klick auf die Ressource in einem angehefteten Rezept |

Alle Tastenkürzel außer `Esc`, `Leertaste`, `Strg+C`/`Strg+V` und den Pfeiltasten lassen sich im Einstellungsmenü neu belegen (seit Phase 7a). Der Browser merkt sich die Belegung.

### Im Layout-Designer

| Aktion | Eingabe |
|---|---|
| Bauteil platzieren | aus der Leiste ins Raster ziehen (Klick = an der ersten freien Stelle einsetzen) |
| Drehen | `R` oder Rechtsklick (beim Ziehen oder auf ein ausgewähltes Teil) |
| Verschieben | liegendes Teil ziehen oder auswählen und Pfeiltasten |
| Entfernen | aus dem Raster ziehen, Doppelklick oder `Entf` |
| Rückgängig / Wiederholen | `Strg+Z` / `Strg+Y` |
| Hitze-Ansicht | `H` |

## Selbst anpassen

Alles, was du ändern darfst, steht in `index.html` in Blöcken mit der Überschrift **KONFIGURATION**:

- **Bedienoberfläche** (im `<style>`-Bereich ganz oben): Farben, Schriften und Abstände der Infobox als CSS-Variablen.
- **Abschnitt 1 – 3D & Grafik** (`const GRAFIK`): Farben der Szene, Kamerawinkel, Zoomgrenzen, Licht, Schatten, Fugenbreite.
- **Abschnitt 2 – Raster & Logik** (`const LEVELS`, `const LOGIK`): Name und Größe der Level, Laufgeschwindigkeit und Pathfinding.
- **Abschnitt 2c – Layout-Designer** (`const LAYOUT`, `const BAUTEILE`): Größe des Produkt-Rasters und der Bauteil-Katalog mit Form, Stufe, Hitze, Kühlung, Toleranz, Farbe sowie Rezept und Zeit an der Werkbank.
- **Abschnitt 2d – Produktion & Logistik** (`const PRODUKTION`, `ROHSTOFFE`, `GEBAEUDE_TYPEN`, `KURIER_STUFEN`): Startbestand, Gebäudegrößen und Fassungsvermögen, Item-Volumen (`volumenProdukt` usw.), Montagezeiten, Ausschussquote, Mitarbeiterzahl, Kurier-Grundwert (`kurierTraglast`) und die Kurier-Stufen (Zusatz-Traglast, Tempo, Ladezeit).
- **Abschnitt 11i – Import- und Exportzone** (`const ZONEN`): Lieferzeit, Abholintervall, Rhythmen und Startplätze der Zonen.

## Aufbau der Datei

Das Spiel ist bewusst eine einzige Datei (`index.html`), damit es auch in der Claude-Liveansicht läuft. Die Abschnitte im Skript sind nummeriert und nach Zuständigkeit beschriftet (3D-Agent, Logik-Agent, UI/UX-Agent).
