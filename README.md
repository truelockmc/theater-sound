# Soundboard – Setup & Konfiguration

## Dateistruktur

```
soundboard/
├── index.html          ← Startseite (Boards-Übersicht)
├── board.html          ← Soundboard-Ansicht
├── config.json         ← Konfiguration (hier alles einstellen)
└── audio/
    └── Momo/           ← Audiodateien hier rein
        ├── Donner.mp3
        ├── Baby weinen.opus
        └── ...
```

## Audiodateien ablegen

Kopiere alle Audiodateien aus deinem Momo-Ordner nach `audio/Momo/`.
Die Dateinamen müssen exakt mit den `"file"`-Einträgen in `config.json` übereinstimmen.

## config.json bearbeiten

### Szenen und Sounds zuordnen

```json
{
  "scenes": [
    {
      "number": "1",
      "name": "Szene 1 – Das Amphitheater",
      "sounds": [
        { "file": "Donner.mp3", "label": "Donner" },
        { "file": "Baby weinen.opus", "label": "Baby weint" }
      ]
    },
    {
      "number": "7.1",
      "name": "Szene 7.1 – Die grauen Herren",
      "sounds": [
        { "file": "Graue Herren Alarm.wav", "label": "Graue Herren Alarm" }
      ]
    }
  ]
}
```

- `number`: Beliebige Zahl oder Dezimalzahl (z.B. `"1"`, `"7.1"`, `"12"`)
- `name`: Optionaler Szenentitel
- `label`: Anzeigename des Sounds im Board (kann kürzer als der Dateiname sein)

### Einen Sound in mehreren Szenen

Einfach denselben `"file"`-Eintrag in mehreren Szenen verwenden:

```json
{ "file": "vecna clock.flac", "label": "Vecna Clock" }
```

→ Der Sound wird in beiden Szenen angezeigt und teilt sich denselben Audioplayer
  (wenn er in Szene 1 läuft und du in Szene 3 draufklickst, stoppt er dort).

### Weiteres Board hinzufügen

```json
{
  "boards": [
    { "id": "momo", "title": "Momo", ... },
    {
      "id": "faust",
      "title": "Faust",
      "description": "J. W. v. Goethe – Faust",
      "color": "#6a8fc8",
      "audioPath": "audio/Faust/",
      "scenes": [ ... ]
    }
  ]
}
```

## Hosten

### Lokal testen (empfohlen)
```bash
# Python
python3 -m http.server 8080
# dann: http://localhost:8080
```
```bash
# Node
npx serve .
```

### GitHub Pages
1. Repository erstellen, alle Dateien pushen
2. Settings → Pages → Branch: main
3. URL: `https://username.github.io/repo-name/`

### Netlify / Vercel
Einfach den Ordner draggen → fertig.

## Bedienung

| Aktion | Beschreibung |
|--------|-------------|
| Klick auf Sound-Karte | Abspielen |
| Klick auf laufenden Sound | Fade-Out (2 Sek.) |
| ↺ Loop | Loop an/aus (wirkt sofort) |
| Chip im Top-Bar | Sound anzeigen / stoppen |
| STOP ALL | Alle laufenden Sounds fade-stoppen |
| Punkte rechts | Schnellnavigation zu Szene |
