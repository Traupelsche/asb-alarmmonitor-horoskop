# Alarm Monitor Horoskop

Eine kleine, statische Web-App, die täglich um 05:00 Uhr lokal ein neues, zufälliges Horoskop aus einer CSV-Datei anzeigt. Zusätzlich wird neben dem Horoskop ein QR‑Code angezeigt, der zu einer Feedback-Seite führt.

## Features
- Tägliche, deterministische Zufallsauswahl aus `horoskop.csv`
- Tageswechsel um 05:00 Uhr (lokale Zeit); automatischer Reload genau zu diesem Zeitpunkt
- Automatischer Dark-/Light‑Mode via `prefers-color-scheme`
- QR‑Code neben dem Horoskop, verlinkt auf `feedback.html`
- Feedback-Seite öffnet das E‑Mail‑Programm mit vorbefülltem Betreff und Nachricht

## Projektstruktur
```
.
├── index.html         # Startseite (Horoskop + QR-Code)
├── index.css          # Styles inkl. Dark-Mode
├── index.js           # Logik: CSV laden, Auswahl, Auto-Reload, QR setzen
├── horoskop.csv       # Datenquelle (Überschrift;Text)
├── feedback.html      # Feedback-Formular (mailto:)
└── feedback.css       # Styles für Feedback-Seite
```

## CSV-Format
- Trennzeichen: Semikolon `;`
- Erste Zeile (Header) wird erkannt und übersprungen
- Jede weitere Zeile: `Überschrift;Text`

Beispiel:
```
Überschrift;Text
Tageshoroskop;Heute ist euer Tag! Zumindest bis der Melder geht.
Spruch des Tages;Ein guter Tag, um den Kollegen daran zu erinnern, dass 'gleich zurück' relativ ist.
```

## Funktionsweise der Auswahl
- Die Auswahl ist „willkürlich“, aber pro Tag stabil (deterministisch)
- Der Tageswechsel findet um 05:00 Uhr lokaler Zeit statt (nicht um Mitternacht)
- Ein Timer lädt die Seite genau um 05:00 neu, sodass automatisch das neue Horoskop erscheint

## Lokal starten
Da `fetch` genutzt wird, sollte die Seite über einen lokalen Webserver geöffnet werden (nicht via `file://`).

- Python (3.x):
  ```bash
  python3 -m http.server 8000
  ```
  Öffne dann: http://localhost:8000

- Node (serve):
  ```bash
  npx serve
  ```

## Deployment-Hinweise
- Statisches Hosting (z. B. GitHub Pages, Netlify, Vercel) funktioniert problemlos
- Achte darauf, dass `horoskop.csv` im selben Verzeichnis wie `index.html` liegt (fetch via relative URL)

## Feedback-Konfiguration
- In `feedback.html` wird ein `mailto:` Link erzeugt
- Passe die Zieladresse bei Bedarf in `feedback.html` an (Variable `to`, aktuell `feedback@example.com`)

## Anpassungen
- Dark-Mode-Farben in `index.css` und `feedback.css`
- QR‑Bildgröße: `index.html` (`#feedback-qr` width/height)
- Tageswechselzeit (aktuell 05:00): `dayKeyWithCutoff(5)` und `scheduleDailyReload(5)` in `index.js`
- Layout: Bootstrap-Grid in `index.html`

## Lizenz
Füge bei Bedarf eine LICENSE-Datei hinzu (z. B. MIT). Teile mir mit, welche Lizenz du bevorzugst, dann ergänze ich sie.
