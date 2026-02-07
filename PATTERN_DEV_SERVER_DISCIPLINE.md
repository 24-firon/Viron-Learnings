# PATTERN: DEV SERVER DISCIPLINE

**Context:** Local Development Workflow.
**Status:** MANDATORY (ZERO TOLERANCE).

## 1. THE SINGLE PORT POLICY

**Never** run more than one instance of `pnpm dev`.
If `localhost:3000` is busy, **KILL IT**. Do not switch to 3001.

## 2. THE VISUAL AUDIT PROTOCOL

Before telling the user "It works", you must verify:

- **Port:** Are you on 3000?
- **Animation:** Does it play from Frame 0? (Or is it paused on black?)
- **Brightness:** Is the exposure set to at least 1.5 for metallic objects?

## 3. ASSET INGESTION

When requesting assets:

- Be specific: "I need a ZIP file."
- Be reactive: Do not wait for files that aren't there. If missing, use placeholders (e.g. `Color("hotpink")`) to prove the code works first.
