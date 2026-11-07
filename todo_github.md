# TODO: Veröffentlichen auf GitHub Pages

Ziel: Den Dart-Zähler kostenlos unter `https://beneb.github.io/DartPunkte/` erreichbar
machen, ohne echten Namen und private E-Mail-Adresse preiszugeben.

Gehört zu `TODO.md` → „Später“.

## 1. Was GitHub wissen will

- **Pflicht:** E-Mail-Adresse (nur zur Bestätigung und für Benachrichtigungen, bleibt
  privat), Passwort, **Benutzername** (öffentlich, steckt in der URL)
- **Nicht nötig:** echter Name, Adresse, Telefonnummer, Geburtsdatum, Zahlungsdaten.
  Der kostenlose Plan reicht für GitHub Pages.
- Tipp: Für noch weniger Spuren eine eigene E-Mail-Adresse nur für GitHub verwenden

## 2. Konto anlegen

- [x] Auf **github.com** auf **Sign up** klicken
- [x] E-Mail, Passwort und **Benutzername** eingeben. Am besten einen Nickname wählen,
      der nicht den echten Namen enthält → `beneb`
- [x] Bilderrätsel lösen und den Code aus der Bestätigungsmail eingeben
- [x] Fragen zu Team und Interessen überspringen, **Free**-Plan wählen

## 3. Privatsphäre einstellen

Oben rechts auf das Profilbild klicken, dann **Settings**.

- [ ] **Public profile:** Name leer lassen oder Nickname eintragen; Bio, Ort, Firma und
      Website leer lassen (offen: zuletzt stand dort noch der echte Name)
- [x] **Emails:** Haken bei **„Keep my email addresses private“** setzen
- [x] Die angezeigte **noreply-Adresse** notieren
      → `1087589+beneb@users.noreply.github.com`
- [x] Optional: Haken bei **„Block command line pushes that expose my email“** setzen.
      Dann lehnt GitHub jeden Push mit der echten Adresse ab (Achtung, siehe Schritt 5)
- [ ] **Password and authentication:** Zwei-Faktor-Anmeldung mit einer Authenticator-App
      einrichten (verlangt GitHub früher oder später ohnehin)
- [ ] **Recovery-Codes sicher speichern**, sonst ist das Konto bei Handyverlust weg

## 4. Git auf dem PC umstellen

Damit künftige Commits Nickname und noreply-Adresse tragen. Mit `--global` gilt das für
alle Projekte auf diesem PC. Ohne `--global` (im Projektordner ausgeführt) gilt es nur
für DartPunkte.

- [x] Ausgeführt (ohne `--global`, nur für DartPunkte):
      ```
      git config user.name "beneb"
      git config user.email "1087589+beneb@users.noreply.github.com"
      ```

## 5. Alte Commits: einmal entscheiden

Die bisherigen Commits tragen noch `Benedikt Banas <banasb@yahoo.de>`, und die
entfernte Geburtstagsnachricht steht noch in der Historie.

- **Variante A – so lassen:** Name und Yahoo-Adresse sind dann über die Historie
  öffentlich einsehbar. Wurde mit der Yahoo-Adresse registriert *und* in Schritt 3 das
  Blockieren aktiviert, lehnt GitHub den Push ab. Dann entweder das Blockieren
  abschalten oder Variante B nehmen.
- **Variante B – neu anfangen (empfohlen, solange noch nichts gepusht ist):** Ersetzt
  alle Commits durch einen einzigen mit Nickname und noreply-Adresse. Die alte Historie
  ist danach **unwiderruflich** weg. Nur nach Schritt 4 und mit sauberem Arbeitsstand
  ausführen.

- [x] Variante gewählt: **B**
- [x] Bei Variante B, im Projektordner:
      ```
      git checkout --orphan neu
      git add -A
      git commit -m "Dart-Zähler"
      git branch -D main
      git branch -m main
      ```
- [x] Prüfen, dass nur noch Nickname und noreply-Adresse auftauchen:
      ```
      git log --format="%an <%ae>"
      ```

## 6. Repo anlegen und pushen

- [x] Auf github.com oben rechts auf **+** klicken, dann **New repository**
- [x] Name `DartPunkte`, **Public**, *ohne* README, `.gitignore` und Lizenz, dann
      **Create repository**
- [x] Bedenken: Im öffentlichen Repo sind auch `PLAN-dartzaehler.md`, `TODO.md` und
      diese Datei lesbar
- [x] Vor dem ersten Push den Platzhalter `NICKNAME` im Urheberhinweis durch den echten
      Nickname ersetzen: in `LICENSE`, `index.html` (Kommentar oben und Zeile
      „© 2026 …“ auf dem Startbildschirm) und in den Metadaten der Icons (Claude
      bitten, die Icons mit dem Nickname neu zu erzeugen)
- [x] Im Projektordner:
      ```
      git remote add origin https://github.com/beneb/DartPunkte.git
      git push -u origin main
      ```
- [x] Beim ersten Push öffnet sich ein Browserfenster zur Anmeldung (Git Credential
      Manager, bei Git für Windows dabei). Danach merkt sich Windows den Login.
- Stolperstein (gelöst): Push scheiterte mit „No anonymous write access“. Ursache war
  ein Eintrag `[url "https://:@github.com"] insteadOf = https://github.com` in
  `~/.gitconfig`, der leere Zugangsdaten mitschickt. Entfernt mit
  `git config --global --remove-section "url.https://:@github.com"`, außerdem
  `credential.helper` von `store` auf `manager` gestellt.

## 7. GitHub Pages einschalten

- [ ] Im Repo auf **Settings**, dann links auf **Pages**
- [ ] Source: **Deploy from a branch**, Branch **main**, Ordner **/ (root)**, dann **Save**
- [ ] Nach 1–2 Minuten testen: `https://beneb.github.io/DartPunkte/`
- [ ] Auf dem Handy öffnen und **„Zum Startbildschirm hinzufügen“** wählen
- [ ] Link an die Freunde schicken (Spielstände bleiben je Browser lokal)
- Updates danach: einfach `git push`

## Was am Ende öffentlich ist

- Nickname, der Code sowie `PLAN-dartzaehler.md`, `TODO.md` und `todo_github.md`
- Variante B: ein Commit mit Nickname und noreply-Adresse
- Variante A: zusätzlich die alte Historie mit echtem Namen und Yahoo-Adresse
