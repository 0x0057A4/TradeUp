# Trade Up

Isometrisches Wirtschafts- und Fabrikaufbau-Spiel im Browser (Three.js, WebGL).

## Stand: Phase 3 – Der Produkt-Layout-Designer

- **Phase 1:** Startlevel **Garage** (16 × 48 Kacheln), isometrische Kamera, Hover und Auswahl
- **Phase 2:** Spielfigur mit A*-Pathfinding, Test-Blöcke per `Shift` + Klick
- **Phase 3:** Produkt-Layout-Designer als 2D-Fenster über der Garage:
  - Produkt-Raster 4 × 4 (16 Kacheln), 8 Bauteile in Tetris-Formen per Drag & Drop (Maus und Touch)
  - Bauteile drehen, verschieben, entfernen, Rückgängig/Wiederholen
  - Hitze-Berechnung: Bauteile heizen direkt angrenzende Kacheln auf, Kühlkörper kühlen; liegt mehr Hitze auf einem Teil als seine Toleranz, ist es überhitzt (rot)
  - Designs als **Blaupause** speichern (im Browser, bleibt nach dem Neuladen erhalten), laden, umbenennen, duplizieren, löschen

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
| Figur hinschicken | Linksklick |
| Test-Block setzen / entfernen | `Shift` + Linksklick |
| Kamera auf die Figur | `Leertaste` |
| Layout-Designer öffnen / schließen | Knopf in der Infobox, `L`, `Esc` |

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
- **Abschnitt 2c – Layout-Designer** (`const LAYOUT`, `const BAUTEILE`): Größe des Produkt-Rasters und der Bauteil-Katalog mit Form, Stufe, Hitze, Kühlung, Toleranz und Farbe.

## Aufbau der Datei

Das Spiel ist bewusst eine einzige Datei (`index.html`), damit es auch in der Claude-Liveansicht läuft. Die Abschnitte im Skript sind nummeriert und nach Zuständigkeit beschriftet (3D-Agent, Logik-Agent, UI/UX-Agent).
