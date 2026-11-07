# TODO: Dart-Zähler 301

Stand: 2026-10-12. Alle 5 Schritte umgesetzt und geprüft (auch auf Android + Firefox). Offen sind nur die Punkte unter „Später“.

Details zu jedem Schritt in `PLAN-dartzaehler.md`.

## Umsetzung

- [x] **Schritt 1 – Startbildschirm:** Spieler hinzufügen/entfernen/sortieren, Mischen,
      Platzhalternamen, Namen merken, Wechsel zum Spielbildschirm
  - [x] Geprüft im Browser
- [x] **Schritt 2 – Spiel:** Ziffernblock, Validierung, Punkteabzug, Spielerwechsel,
      Bust, Statuszeile, aktiver Spieler hervorgehoben und ins Bild gescrollt
  - [x] Geprüft im Browser
- [x] **Schritt 3 – Rückgängig und Speichern:** mehrstufiges Rückgängig,
      automatisches Speichern/Fortsetzen, „Neues Spiel“ mit Rückfrage
  - [x] Geprüft im Browser
- [x] **Schritt 4 – Spielende:** Finish-Dialog, Plätze, Rangliste, Revanche
  - [x] Geprüft im Browser
- [x] **Schritt 5 – Handy-Feinschliff:** Wake Lock, kein Doppeltipp-Zoom, kein
      Pull-to-refresh, Test auf Android + Firefox
  - [x] Geprüft auf dem Android-Handy in Firefox

- [x] **Einzelpfeil-Eingabe:** jeder der 3 Pfeile wird einzeln eingetragen (0–60 bzw.
      gültige Pfeilwerte), Überwurf setzt die Aufnahme zurück
  - [ ] Geprüft im Browser
- [x] **Double/Triple:** Umschalt-Buttons D/T (hellblau) links und rechts der Anzeige; Anzeige
      zeigt nur das Ergebnis; nach D/T beginnt die nächste Ziffer eine neue Zahl
  - [ ] Geprüft im Browser

## Offene Anforderungen

- [ ] **Keine Bildschirmdrehung:** Die Dart-App darf sich auf dem Handy nicht ins
      Querformat drehen. Eine normale Webseite kann das nicht hart sperren, daher:
      Web-App-Manifest mit `"orientation": "portrait"` (wirkt als installierte App,
      v. a. Android) plus CSS-Hinweis „Bitte Handy hochkant halten“ im Querformat
      (`@media (orientation: landscape) and (max-height: 500px)`)
  - [x] CSS-Hinweis im Querformat (`#rotate-hint` in `index.html`)
  - [ ] CSS-Hinweis geprüft auf dem Handy
  - [x] Manifest mit `"orientation": "portrait"` (`manifest.webmanifest`, Icons
        `icon-192.png`/`icon-512.png`, Link im `<head>`)
  - [ ] Manifest geprüft: nach GitHub Pages in Chrome „App installieren“, über das
        Icon starten, Handy drehen → bleibt hochkant (Firefox zum Vergleich testen)
- [x] **Ziffernblock wie beim Telefon:** oben `1 2 3`, dann `4 5 6`, `7 8 9`, unten
      `⌫ 0 OK` (bisher wie beim Taschenrechner mit `7 8 9` oben)
  - [ ] Geprüft im Browser

- [x] **Tasten reagieren sofort:** Ziffernblock und D/T lösen beim Berühren aus
      (`pointerdown` statt `click`), Tipps in die Lücken zählen für die nächste Taste,
      Aufblitzen + kurzes Vibrieren als Rückmeldung
  - [ ] Geprüft auf dem Handy

## Später

- [ ] Seite kostenlos auf GitHub Pages ins Internet stellen, damit sie per URL
      erreichbar ist und als Icon auf den Startbildschirm gelegt werden kann.
      Schritt-für-Schritt-Anleitung (Konto anlegen ohne echten Namen und private
      E-Mail, Git umstellen, pushen, Pages einschalten): [`todo_github.md`](todo_github.md)
- [ ] Optional: installierbare Offline-App (PWA) mit Manifest und Service Worker
