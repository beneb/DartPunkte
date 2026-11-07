# Git und GitHub am Beispiel von DartPunkte

Eine Einführung für den Einstieg. Alle Beispiele beziehen sich auf dieses Projekt.

---

## 1. Was ist was?

| Begriff | Was es ist | Bei dir |
|---|---|---|
| **Git** | Ein Programm auf deinem PC, das sich jede Version deiner Dateien merkt | Git für Windows |
| **Repository (Repo)** | Ein Projektordner, dessen Versionen Git verwaltet. Die Historie steckt im versteckten Unterordner `.git` | `D:\dev\claudeCodeProjekte\code\DartPunkte` |
| **GitHub** | Eine Webseite, die eine Kopie deines Repos online aufbewahrt | `https://github.com/beneb/DartPunkte` |
| **GitHub Pages** | Ein Dienst von GitHub, der aus dem Repo eine Webseite macht | `https://beneb.github.io/DartPunkte/` |

Git funktioniert auch ganz ohne GitHub. GitHub ist nur der Ort, an dem eine Kopie
liegt, die andere sehen können.

---

## 2. Die drei Orte deines Projekts

```
   DEIN PC                                  INTERNET
  ┌─────────────────────────────┐          ┌──────────────────────────┐
  │  DartPunkte (Ordner)        │          │  GitHub                  │
  │                             │  push →  │  github.com/beneb/       │
  │  index.html, LICENSE, ...   │          │  DartPunkte              │
  │  .git  ← alle Commits       │  ← pull  │  (heißt bei Git "origin")│
  └─────────────────────────────┘          └────────────┬─────────────┘
                                                        │ baut automatisch
                                                        ▼
                                           ┌──────────────────────────┐
                                           │  GitHub Pages            │
                                           │  beneb.github.io/        │
                                           │  DartPunkte/             │
                                           │  ← hier spielen Freunde  │
                                           └──────────────────────────┘
```

Wichtig: Die Kopien gleichen sich **nicht von selbst** ab. Was du lokal änderst, kommt
erst mit `git push` auf GitHub.

---

## 3. Ein Commit ist ein Schnappschuss

Ein **Commit** speichert den Stand aller Dateien zu einem bestimmten Zeitpunkt, mit
einer kurzen Beschreibung, deinem Namen und der Uhrzeit. Die Commits reihen sich
aneinander:

```
  ●──────────────●──────────────●   ← main (dein Zweig)
  ba1ac69        a3f…           7c2…
  "Dart-Zähler"  "Zurück-Knopf" "Farben"
                                ▲
                                HEAD = hier stehst du gerade
```

- Jeder Commit hat eine eindeutige Kennung, z. B. `ba1ac69`.
- **main** ist der Name deines Zweigs (Branch). Mehr Zweige brauchst du vorerst nicht.
- Zu jedem alten Commit kannst du zurückschauen. Darum ist Git eine Art
  „Rückgängig-Knopf für ganze Projekte“.

Dein Repo hat zurzeit genau **einen** Commit. Die 17 alten Commits haben wir beim
Neuanfang bewusst verworfen, weil dein echter Name und deine Yahoo-Adresse darin standen
(siehe Abschnitt 8).

---

## 4. Vom Ändern zum Commit: die drei Bereiche

Git arbeitet lokal mit drei Bereichen:

```
  ┌──────────────────┐   git add    ┌──────────────────┐  git commit  ┌──────────────────┐
  │  Arbeitsordner   │ ───────────► │  Staging-Bereich │ ───────────► │  Repo (.git)     │
  │                  │              │                  │              │                  │
  │  hier bearbeitest│              │  „das kommt in   │              │  fest gespeichert│
  │  du die Dateien  │              │  den nächsten    │              │  als Commit      │
  │                  │              │  Commit“         │              │                  │
  └──────────────────┘              └──────────────────┘              └──────────────────┘
```

Der Staging-Bereich ist wie ein Einkaufskorb: Du legst hinein, was in den nächsten
Commit soll. So kannst du auch nur einen Teil deiner Änderungen committen.

Abkürzung: `git commit -am "..."` legt alle **schon bekannten** Dateien in den Korb und
committet sie in einem Rutsch. Ganz neue Dateien musst du einmal mit `git add`
hinzufügen.

---

## 5. Der tägliche Ablauf

```
  1. Dateien ändern          (z. B. Claude ändert index.html)
         │
  2. git status              Was hat sich geändert?
  3. git diff                Wie genau? (zeigt die Zeilen)
         │
  4. git add index.html      In den Korb legen
  5. git commit -m "..."     Schnappschuss machen
         │
  6. git push                Auf GitHub hochladen
         │
  7. 1–2 Minuten warten      GitHub Pages aktualisiert die Seite
```

Ein echtes Beispiel aus diesem Projekt:

```
git status
git add todo_github.md
git commit -m "todo_github: erledigte Schritte abgehakt"
git push
```

**So liest du `git status`:**

| Meldung | Bedeutung |
|---|---|
| `nothing to commit, working tree clean` | Alles committet, nichts zu tun |
| `Changes not staged for commit` | Geändert, aber noch nicht im Korb |
| `Changes to be committed` | Im Korb, bereit für `git commit` |
| `Untracked files` | Neue Datei, die Git noch nicht kennt |
| `Your branch is ahead of 'origin/main' by 1 commit` | Lokal gibt es einen Commit, der noch nicht auf GitHub ist → `git push` |
| `Your branch is up to date with 'origin/main'` | Lokal und GitHub sind gleich |

---

## 6. Push und Pull

```
  lokal                                GitHub (origin)
  ●──●──●──●  main                     ●──●──●  main
           ▲                                  ▲
           du bist 1 Commit voraus

             ── git push ──►

  ●──●──●──●  main                     ●──●──●──●  main
                                       jetzt gleich
```

- **`git push`**: lokale Commits nach GitHub schicken.
- **`git pull`**: Commits von GitHub holen. Brauchst du nur, wenn auf GitHub etwas
  Neues liegt, z. B. weil du direkt auf github.com eine Datei bearbeitet hast oder von
  einem anderen PC aus arbeitest.
- `-u origin main` war nur beim allerersten Push nötig. Seitdem weiß Git, wohin
  `git push` gehen soll.

**Anmeldung:** Beim ersten Push hat sich der *Git Credential Manager* im Browser bei
GitHub angemeldet. Windows merkt sich das, du musst dich nicht jedes Mal neu anmelden.

---

## 7. Was öffentlich ist

Dein Repo ist **Public**. Jeder kann auf GitHub alles lesen, was gepusht wurde:

- alle Dateien im Repo, auch `TODO.md`, `todo_github.md`, `PLAN-dartzaehler.md` und
  diese Datei
- die Historie, also alle Commits mit Name, E-Mail-Adresse und Beschreibung

Damit dabei nichts Privates sichtbar wird:

- Deine Commits tragen `beneb <1087589+beneb@users.noreply.github.com>`. Das ist eine
  Ersatzadresse von GitHub, deine echte Adresse bleibt verborgen.
- Eingestellt ist das nur für dieses Projekt (`git config` ohne `--global`). In
  anderen Projekten würde Git weiter `Benedikt Banas <banasb@yahoo.de>` verwenden.
- In den GitHub-Einstellungen blockiert „Block command line pushes that expose my email“
  jeden Push, der die Yahoo-Adresse enthält. Das ist ein Sicherheitsnetz.

**Dateien gar nicht erst veröffentlichen:** Trägst du Dateinamen in eine Datei namens
`.gitignore` ein, ignoriert Git sie. Sie bleiben auf deinem PC, landen aber nie in
einem Commit.

> Achtung: Was einmal gepusht wurde, bleibt in der Historie sichtbar, auch wenn du die
> Datei später löschst. Passwörter, private Daten und Ähnliches deshalb nie committen.

---

## 8. Was wir beim Einrichten gemacht haben

Zum Nachlesen, falls du das bei einem anderen Projekt wiederholen willst:

1. **GitHub-Konto** `beneb` angelegt, E-Mail auf privat gestellt.
2. **Git für dieses Projekt umgestellt:**
   ```
   git config user.name "beneb"
   git config user.email "1087589+beneb@users.noreply.github.com"
   ```
3. **Historie neu angefangen:** Alle alten Commits wurden durch einen einzigen ersetzt.
   ```
   git checkout --orphan neu      neuer Zweig ohne Vorgeschichte
   git add -A                     alle Dateien in den Korb
   git commit -m "..."            erster Commit
   git branch -D main             alten Zweig mit alter Historie löschen
   git branch -m main             neuen Zweig in "main" umbenennen
   ```
4. **Repo auf GitHub angelegt** und verbunden:
   ```
   git remote add origin https://github.com/beneb/DartPunkte.git
   git push -u origin main
   ```
5. **Stolperstein:** Der Push scheiterte zuerst mit „No anonymous write access“. Ein
   alter Eintrag in `C:\Users\piont\.gitconfig` hat leere Zugangsdaten mitgeschickt.
   Nach dem Entfernen kam das Anmeldefenster und der Push klappte.

---

## 9. Die wichtigsten Befehle

**Nur anschauen, ändert nichts:**

| Befehl | Was er zeigt |
|---|---|
| `git status` | Was ist geändert, was im Korb, ist GitHub aktuell? |
| `git diff` | Geänderte Zeilen, die noch nicht im Korb sind |
| `git diff --staged` | Geänderte Zeilen, die im Korb sind |
| `git log --oneline` | Liste aller Commits, ein Commit pro Zeile |
| `git show ba1ac69` | Was genau in diesem Commit geändert wurde |
| `git remote -v` | Mit welchem GitHub-Repo das Projekt verbunden ist |

**Verändern, im Alltag üblich:**

| Befehl | Was er tut |
|---|---|
| `git add <datei>` | Datei in den Korb legen |
| `git commit -m "..."` | Korb als Commit speichern |
| `git commit -am "..."` | Alle bekannten geänderten Dateien committen |
| `git push` | Commits nach GitHub schicken |
| `git pull` | Commits von GitHub holen |

**Vorsicht, können Arbeit unwiderruflich löschen:** `git reset --hard`,
`git checkout -- <datei>`, `git restore`, `git clean`, `git push --force`. Nur
benutzen, wenn du genau weißt, was passiert, oder vorher nachfragen.

---

## 10. Wenn etwas schiefgeht

| Problem | Lösung |
|---|---|
| Commit-Nachricht vertippt, noch **nicht** gepusht | `git commit --amend -m "neue Nachricht"` |
| Datei versehentlich in den Korb gelegt | `git restore --staged <datei>` (die Änderung bleibt erhalten) |
| `git push` meldet `rejected … fetch first` | Auf GitHub liegt etwas Neues. Erst `git pull`, dann `git push` |
| Push meldet „push declined due to email privacy restrictions“ | Ein Commit enthält die Yahoo-Adresse. `git log --format="%an <%ae>"` prüfen und nachfragen |
| Webseite zeigt alten Stand | 1–2 Minuten warten, dann im Browser neu laden. Auf dem Handy notfalls den Cache leeren |
| Unsicher, was los ist | `git status` ausführen und die Ausgabe Claude zeigen |

---

## Kleines Glossar

- **Branch (Zweig):** eine Linie von Commits. Bei dir gibt es nur `main`.
- **Clone:** ein Repo von GitHub auf einen PC kopieren, z. B. auf einen zweiten Rechner.
- **Commit:** ein gespeicherter Schnappschuss mit Beschreibung.
- **HEAD:** der Commit, auf dem du gerade stehst.
- **origin:** der Spitzname für dein Repo auf GitHub.
- **origin/main:** der Stand von `main` auf GitHub, wie Git ihn zuletzt gesehen hat.
- **Remote:** eine entfernte Kopie des Repos, hier GitHub.
- **Staging-Bereich:** der „Korb“ für den nächsten Commit.
