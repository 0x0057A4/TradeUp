# Trade Up

Isometrisches Wirtschafts- und Fabrikaufbau-Spiel im Browser (Three.js, WebGL).

## Stand: Phase 1 – Technisches Fundament & Bau-Raster

- Startlevel **Garage** mit einem Raster von 16 × 48 Kacheln
- Isometrische Kamera (orthografisch), verschieben und zoomen
- Hover-Rahmen folgt der Maus, Linksklick wählt eine Kachel aus
- Infobox oben links zeigt Kachel unter der Maus und Auswahl

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

## Selbst anpassen

Alles, was du ändern darfst, steht in `index.html` in Blöcken mit der Überschrift **KONFIGURATION**:

- **Bedienoberfläche** (im `<style>`-Bereich ganz oben): Farben, Schriften und Abstände der Infobox als CSS-Variablen.
- **Abschnitt 1 – 3D & Grafik** (`const GRAFIK`): Farben der Szene, Kamerawinkel, Zoomgrenzen, Licht, Schatten, Fugenbreite.
- **Abschnitt 2 – Raster & Logik** (`const LEVELS`): Name und Größe der Level. Ein neues Gebäude ist ein weiterer Eintrag in der Liste.

## Aufbau der Datei

Das Spiel ist bewusst eine einzige Datei (`index.html`), damit es auch in der Claude-Liveansicht läuft. Die Abschnitte im Skript sind nummeriert und nach Zuständigkeit beschriftet (3D-Agent, Logik-Agent, UI/UX-Agent).
