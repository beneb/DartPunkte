# TODO: Dart-Zähler 301

Stand: 2026-10-12. Alle 5 Schritte umgesetzt und geprüft (auch auf Android + Firefox). Offen sind die Prüfungen oben und die Punkte unter „Als Nächstes“.

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

## Als Nächstes

- [ ] **GitHub Pages fertig einrichten.** Repo `beneb/DartPunkte` ist angelegt und
      gepusht. Offen sind die Punkte in [`todo_github.md`](todo_github.md):
  - [ ] Pages einschalten (Settings → Pages → Deploy from a branch → `main` / root)
  - [ ] `https://beneb.github.io/DartPunkte/` auf dem Handy testen und installieren
        (Android Chrome/Firefox: Menü ⋮ → „App installieren“ bzw. „Zum
        Startbildschirm hinzufügen“; iPhone Safari: Teilen → „Zum Home-Bildschirm“)
  - [ ] GitHub-Profil: echten Namen bei „Public profile“ entfernen
  - [ ] Zwei-Faktor-Anmeldung einrichten, Recovery-Codes speichern
- [ ] **Entscheiden: Notizen öffentlich lassen?** `TODO.md`, `todo_github.md`,
      `PLAN-dartzaehler.md` und `GIT-GRUNDLAGEN.md` sind im öffentlichen Repo lesbar.
      Falls nicht gewünscht: in `.gitignore` aufnehmen und mit
      `git rm --cached …` aus dem Repo nehmen (bleiben lokal erhalten). Sollen sie auch
      aus der Historie verschwinden, ist ein `git push --force` nötig.
- [ ] **Offline spielbar (Service Worker).** Ohne ihn startet die App ohne Internet
      nur zufällig aus dem Browser-Cache.
  - [ ] Neue Datei `sw.js` (ca. 30 Zeilen): speichert `index.html`,
        `manifest.webmanifest`, `icon-192.png`, `icon-512.png` beim ersten Öffnen
  - [ ] Strategie **network-first**: mit Internet immer den neuesten Stand von GitHub
        holen, nur ohne Netz die gespeicherte Kopie nehmen. So kommen Updates nach
        `git push` weiterhin beim nächsten Öffnen an
  - [ ] Service Worker in `index.html` anmelden (`navigator.serviceWorker.register`)
  - [ ] Geprüft: App einmal mit Internet öffnen, dann Flugmodus → App startet trotzdem
  - [ ] Geprüft: Änderung pushen → erscheint beim nächsten Öffnen mit Internet
- [ ] **iPhone-Icon:** `<link rel="apple-touch-icon" href="icon-192.png">` in den
      `<head>` von `index.html`, sonst zeigt iOS ein Bildschirmfoto als Icon -> EB kann es testen?
- [ ] **git wie:** wie kann ich mir am besten ein git diff anschauen von allen meinen änderungen, ist terminal ausreichend?


