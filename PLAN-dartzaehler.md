# Plan: Dart-Zähler 301

Einfacher Dart-Zähler als einzelne HTML-Seite, optimiert für das Handy
(Android + Firefox, Hochformat). Minimalistisch: nur Name und Restpunkte.

## Spielregeln

- Start bei **301**, rückwärts zählen, **kein Double-Out**. Rest 1 ist normal spielbar.
- **2–8 Spieler**, Namen werden vor dem Spiel eingetragen.
- Eingabe pro **Aufnahme** (Summe der 3 Darts), erlaubt: 0–180, außer den unmöglichen
  Summen 163, 166, 169, 172, 173, 175, 176, 178, 179.
- **Bust:** Aufnahme > Restwert → Aufnahme zählt nicht, Restwert bleibt, nächster Spieler.
- Genau 0 → Spieler ist fertig und bekommt den nächsten Platz.
- Nach jedem Finish, solange noch mindestens 2 Spieler übrig sind, ein Dialog:
  **„Weiterspielen um Platz N“** oder **„Spiel beenden“**. Fertige Spieler werden
  danach übersprungen. Bleibt nur ein Spieler übrig, endet das Spiel automatisch.
- **Revanche:** gleiche Spieler, Reihenfolge um eins rotiert (der bisher Zweite beginnt).

## Bildschirme

### Startbildschirm

```
┌─────────────────────┐
│   🎯 301            │
├─────────────────────┤
│ [Anna      ] ↑ ↓ ✕  │
│ [Ben       ] ↑ ↓ ✕  │
│ [Spieler 3 ] ↑ ↓ ✕  │  ← Platzhalter, wenn leer
│ + Spieler hinzufügen│  ← verschwindet bei 8
├─────────────────────┤
│ 🔀 Mischen          │
│ [   Spiel starten ] │
└─────────────────────┘
```

- Immer mindestens 2 Felder (✕ ausgeblendet bei 2), höchstens 8.
- Leere Namen → „Spieler N“. Doppelte Namen erlaubt. Maximal 15 Zeichen.
- Zuletzt verwendete Namen sind vorausgefüllt.

### Spielbildschirm

```
┌─────────────────────┐
│ ☰ Menü        ↶     │  ← Menü (Neues Spiel), Rückgängig
├─────────────────────┤
│ ▶ Anna         141  │  ← Spielerliste, scrollt bei Bedarf,
│   Ben          301  │    aktiver Spieler hervorgehoben
│   Carla        256  │
├─────────────────────┤
│ Anna: 60 → Rest 141 │  ← Statuszeile (letzte Eingabe / Überworfen!)
│          [  45 ]    │  ← aktuelle Eingabe
│  7    8    9        │
│  4    5    6        │  ← Ziffernblock, fest unten
│  1    2    3        │
│  ⌫    0    OK       │
└─────────────────────┘
```

- Pro Spieler nur Name und Restpunkte. Fertige Spieler zeigen ihren Platz.
- Aktiver Spieler wird automatisch ins Bild gescrollt.
- Statuszeile: „Anna: 60 → Rest 141“ bzw. „Ben: 45 → Überworfen!“ (rot).
- Ziffernblock-Tasten mindestens ca. 60 px hoch.
- „Neues Spiel“ im Menü fragt zur Sicherheit nach.

### Spielende

- Rangliste, Knöpfe **„Revanche“** und **„Neues Spiel“** (zurück zum Startbildschirm,
  Namen vorausgefüllt).
- Rückgängig ist auch aus dem Finish-Dialog heraus möglich.

## Optik und Verhalten

- Immer **dunkel**, hoher Kontrast. Akzent **grün** (aktiver Spieler), **rot** für Bust.
- Systemschriften, Ziffern mit `font-variant-numeric: tabular-nums`.
- Keine Statistik, keine Vibration, keine Töne.
- **Wake Lock** hält den Bildschirm an, solange ein Spiel läuft (ohne Schalter,
  stillschweigend ohne Wirkung, wenn nicht unterstützt).
- Kein Zoom durch Doppeltippen (`touch-action: manipulation`), kein Pull-to-refresh
  (`overscroll-behavior: none`).

## Technik

- **Eine einzige `index.html`** mit eingebettetem CSS und JavaScript, keine externen
  Dateien, kein CDN, kein Build-Schritt. Muss als lokale Datei (`file://`) laufen.
- **Zustand:** Spielernamen + Liste der Aufnahmen (nur Zahlen) + Entscheidungen im
  Finish-Dialog. Der Spielstand (Restpunkte, wer dran ist, Plätze) wird bei jeder
  Änderung aus dieser Liste **neu berechnet**.
- **Rückgängig** = letzten Eintrag entfernen, beliebig weit.
- **Speichern:** Nach jeder Änderung in `localStorage` (Spielstand und zuletzt
  verwendete Namen). Beim Öffnen wird ein laufendes Spiel ohne Nachfrage fortgesetzt.
  Alle Zugriffe in `try/catch` – ohne `localStorage` läuft die Seite trotzdem.
- Die **Spiellogik** steht als reine Funktionen (ohne DOM-Zugriff) in einem eigenen
  `<script>`-Abschnitt, damit sie mit einem Node-Skript geprüft werden kann.

## Testen

- Spiellogik: Node-Skript im Scratchpad (nicht im Repo).
- Oberfläche: an jedem Haltepunkt im Browser am PC, zum Schluss auf dem Android-Handy
  in Firefox.

## Schritte

1. **Startbildschirm:** Spieler hinzufügen/entfernen/sortieren, Mischen, Platzhalter-
   namen, Namen merken, „Spiel starten“ wechselt zu einem (noch leeren) Spielbildschirm.
2. **Spiel:** Ziffernblock, Validierung, Punkteabzug, Spielerwechsel, Bust, Statuszeile,
   Hervorhebung und Auto-Scroll des aktiven Spielers.
3. **Rückgängig und Speichern:** mehrstufiges Rückgängig, automatisches Speichern und
   Fortsetzen, „Neues Spiel“ im Menü mit Rückfrage.
4. **Spielende:** Finish-Dialog (weiterspielen/beenden), Plätze, Rangliste, Revanche
   mit rotiertem Startspieler.
5. **Handy-Feinschliff:** Wake Lock, Zoom und Pull-to-refresh abstellen, Test auf dem
   Android-Gerät in Firefox.
