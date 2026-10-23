# max-bitnode/hermes-skills — Git & PR Best Practices

## Branching Strategy

Jeder logisch unabhängige Change → **eigener Branch** + **eigenes PR**.
- Feature: `feat/<kurze-beschreibung>`
- Bugfix: `fix/<issue-nummer>-<beschreibung>`
- Improvement: `improve/<beschreibung>`
- Kein Force-Push auf shared branches.

## Commit-Konvention (Conventional Commits)

```
<type>(<scope>): <Beschreibung>

- feat: neue Funktionalität
- fix: Bugfix
- docs: Dokumentation
- refactor: Code-Struktur ohne Verhaltensänderung
- test: Tests hinzufügen/ändern
- chore: Wartungsaufgaben (Dependencies, CI)
```

Beispiele:
- `feat(remote-access-setup): add Windows autostart support`
- `fix(config.yaml): preserve existing signing secret`

## Pull Request Richtlinien

1. **Ein PR = ein logischer Change.** Keine gemischten Features/Fixes.
2. **Review-Pflicht vor Merge.** Kein Self-Merge ohne zweite Augen.
3. **Tests vor PR-Erstellung:** `python -m py_compile <script>.py` für Python-Skripte, Syntax-Check für Markdown.
4. **Keine Secrets im Code:** Keine Passwörter, Hashes, API-Keys, Tokens oder Signing-Secrets. Werte nur als „gesetzt/geändert" kennzeichnen.
5. **CHANGELOG.md aktualisieren** bei signifikanten Änderungen (neue Features, Breaking Changes).
6. **PR-Beschreibung enthält:**
   - Was wurde geändert und warum?
   - Verifikationsschritte (Syntax-Check, Tests, Live-Test)
   - Geänderte Dateien mit kurzen Beschreibungen der Delta

## Review-Prozess

1. Autor erstellt PR und wartet auf Genehmigung.
2. Reviewer prüft: Code-Qualität, Security, Testabdeckung, CHANGELOG.
3. Bei Bedarf: Feedback → Author fixt → neuer Push → erneute Review.
4. Nach Freigabe: Merge (Squash-Merge empfohlen für saubere Historie).

## Repository-Struktur

```
max-bitnode/hermes-skills/
├── AGENTS.md          # Diese Datei — Git-Best-Practices
├── CONTRIBUTING.md    # Langform mit Beispielen (optional)
├── README.md          # Skill-Tap Dokumentation
├── LICENSE            # MIT-Lizenz
└── skills/
    └── <skill-name>/
        ├── SKILL.md   # Skill-Dokumentation
        └── scripts/   # Helper-Skripte (Python, bash, ...)
```

## Sicherheitshinweise

- **Keine Credentials im Repository:** `.env`-Dateien, Token, Passwörter, private Keys gehören nie in den Code.
- **Secrets rotieren:** Bei Verdacht auf Kompromittierung sofort rotieren und PR mit Bereinigung erstellen.
- **Private Repos:** Nur autorisierte Personen haben Push-Rechte; Forks sind öffentlich sichtbar.

## Workflow für Änderungen

1. Branch vom aktuellen `main` erstellen.
2. Code ändern + Tests/Syntax-Checks durchführen.
3. Commit mit Conventional Commit Message.
4. PR erstellen und beschreiben (siehe oben).
5. Auf Review-Freigabe warten.
6. Nach Merge: Branch löschen, `main` pullen für nächste Arbeit.
