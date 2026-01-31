# PATTERN: IDE-Disk-Synchronisation & Git-Sicherheit

Diese Erkenntnisse stammen aus einer wissenschaftlichen Testreihe (Project remotion-studio, Jan 2026) zur Untersuchung von Race-Conditions in AI-IDE-Umgebungen.

## 🔬 Kern-Erkenntnisse

### 1. Physisches Gate (Sofortiges Schreiben)

- **Beobachtung**: Tools wie `write_to_file` oder `replace_file_content` schreiben Daten **sofort** physisch auf die Festplatte, noch bevor der Nutzer in der UI auf "Annehmen" klickt.
- **Konsequenz**: Andere Systemprozesse (Compiler, Git, Server) sehen die Änderungen bereits im "Pending"-Zustand.

### 2. Rollback-Mechanismus (Reject)

- **Beobachtung**: Klickt ein Nutzer auf "Ablehnen" (Reject), führt die IDE automatisch einen Rollback der Datei auf den vorherigen physischen Stand durch.
- **Wichtig**: Dieser Rollback ist ein Dateisystem-Event, kein Git-Event.

### 3. Die Race-Condition (Turn-Separation)

- **Gefahr**: Wenn ein Agent im selben Turn eine Datei ändert UND einen `git commit` sendet, kann Git die Datei committen, während sie auf Disk existiert (H1), der Nutzer sie aber später verwirft (H2).
- **Resultat**: Ein inkonsistentes Repository (Datei ist im Commit, aber lokal gelöscht).
- **Lösung**: **Strikte Turn-Separation**. Git-Befehle dürfen erst im nächsten Turn gesendet werden, nachdem der Nutzer die Dateiedits bestätigt hat.

### 4. Das Timeline-Problem (Agenten-Blindheit)

- Agenten haben kein Live-Signal über UI-Interaktionen (Klicks).
- Informationen über Rejects müssen forensisch (durch Erneutes Lesen der Datei) erlangt werden.

## 🛡️ Sicherheits-Standards (Global)

1. **Keine destruktiven Git-Befehle** (`reset --hard`, `clean -fd`, `push --force`) ohne explizite Nutzer-Einwilligung.
2. **Turn-Separation** bei Git-Operationen ist Pflicht.
3. **Forensische Prüfung**: Nach einem Turn mit Edits sollte der Agent den Zustand der Dateien prüfen, bevor er von einem Erfolg ausgeht.

_Dokumentierte Version: v1.0 | Viron Intelligence System_
