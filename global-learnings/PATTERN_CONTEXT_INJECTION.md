# Architectural Pattern: Context Injection Firewall (Type: LEGISLATIVE)

**ID:** PATTERN-001
**Status:** PROVEN
**Author:** Viron Orchestrator
**Context:** Antigravity / Agentic IDE
**Synergy:** Workspace Rules + Project Law + Sub-Agent Bootstrapping

## 1. Das Problem: "Flüchtiges Wissen" & "Context Blindness"

KI-Agenten leiden unter "Out of Sight, Out of Mind".

- **Risk:** Agenten ignorieren Regeln, die tief in der Dateistruktur vergraben sind (`.agent/rules/policy.md`).
- **Failure Mode:** "Halluzinierte Compliance" – Der Agent _glaubt_, er kennt die Regeln, hat sie aber nie gelesen.
- **Root Cause:** Der System-Prompt ist statisch, das Projekt-Wissen ist dynamisch.

## 2. Die Lösung: "Always-On" Hierarchie (The Injection Stack)

Wir nutzen den Mechanismus der IDE, der `workspace-rule.md` _immer_ injiziert, um eine unumgängliche "Legislative" zu etablieren.

### Die Architektur der Hierarchie

1.  **Layer 0 (Hardware/System):** `<identity>`
    - Unveränderlich. Definiert die Physik des Agenten.
    - **Meta-Info:** OS, Zeit, Tools.

2.  **Layer 1 (The Firewall - Legislative):** `.agent/rules/workspace-rule.md`
    - **Trigger:** `always_on`
    - **Funktion:** Verfassung. Muss kurz sein (Token-Kosten), aber absolut.
    - **Crucial Hook:** Enthält "Pointer" auf Layer 2 ("You MUST read PROJECT_RULES.md").
    - **Synergy:** Verbindet das statische System mit dem dynamischen Projekt.

3.  **Layer 2 (The Law Book - Specifics):** `PROJECT_RULES.md`
    - **Inhalt:** Tech Stack, Token Limits, Coding Style.
    - **Access:** On-Demand (Lazy Loading).
    - **Enforcement:** Durch Layer 1 erzwungen ("Read First").

4.  **Layer 3 (The Executive):** `.agent/workflows/*.md`
    - **Trigger:** Manual (`/release`).
    - **Funktion:** Führt Befehle aus ("Turbo Mode").
    - **Check:** Muss gegen Layer 1 validieren ("Ist das erlaubt?").

## 3. Implementierung & Wartung

### Code: The Firewall

**File:** `.agent/rules/workspace-rule.md`

```yaml
---
trigger: always_on
---
# 🛡️ FIREWALL & GOVERNANCE

1.  **SINGLE SOURCE OF TRUTH**:
  You act strictly according to [PROJECT_RULES.md](PROJECT_RULES.md).
  Read this file IMMEDIATELY at the start of any session.

2.  **NO HALLUCINATED PACKAGES**: Never install libraries without checking `package.json` first.

3.  **SCOPE LOCK**: You are jailed in `./`. Accessing `../` is FORBIDDEN.

4.  **ACTIONISM GUARD**: No `write` operations in `PLANNING` mode.
```

### Protocol: Maintenance

- **Wann ändern?** Nur bei fundamentalen System-Updates (z.B. Wechsel von npm zu bun).
- **Wer ändert?** Nur der Architect (User). Agenten dürfen Layer 1 NICHT anfassen (Self-Preservation).

## 4. Synergetische Potenziale (Beyond Basic Compliance)

- **Sub-Agent Bootstrapping:**
  - Erstelle `TEMP_CONTEXT.md` (Auszug aus Layer 2).
  - Starte Sub-Agent mit: "READ TEMP_CONTEXT.md FIRST".
  - **Effekt:** Sofortige Compliance ohne "Search Overhead".
- **Cross-IDE Compatibility:**
  - Workspace Rules funktionieren auch in VS Code / Cursor (via `.cursorrules`).
  - Pattern ist universell übertragbar.

## 5. Risk Assessment

- **Token Bloat:** Wenn Layer 1 zu lang wird, verliert der Agent den Fokus auf den User-Input. -> Keep it < 20 Zeilen.
- **Rule Conflict:** Wenn Layer 1 "A" sagt und Layer 2 "B", gewinnt Layer 1 (Always On). -> Sync erforderlich.
