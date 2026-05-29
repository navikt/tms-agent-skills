# Copilot customizations for team min-side

[![CI](https://github.com/navikt/tms-copilot/actions/workflows/tms-copilot-sync.yml/badge.svg)](https://github.com/navikt/tms-copilot/actions/workflows/tms-copilot-sync.yml)
![Markdown](https://img.shields.io/badge/docs-Markdown-informational?logo=markdown)
![GitHub Actions](https://img.shields.io/badge/automation-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

Dette repoet samler gjenbrukbare Copilot customizations som team min-side kan bruke direkte, og dele videre til andre repoer ved behov.

## Formål

Repoet er et dokumentasjons- og innholdsrepo for Copilot-tilpasninger. Målgruppen er utviklere som vedlikeholder agentinstruksjoner, og som trenger:

- tydelige skills for konkrete arbeidsflyter
- en enkel måte å oppdatere skills på tvers av repoer
- et felles sted for å videreutvikle instruksjonene

## Skills i repoet

Alle skills ligger under `.github/skills/`, med egen `SKILL.md` per skill.

- `caveman`: ultra-komprimert kommunikasjonsmodus
- `grill-me`: strukturert intervju for å stressteste planer
- `issue-planner`: avklaring og opprettelse av issues fra templates
- `readme-update`: oppdatering av README/repo-dokumentasjon
- `write-a-skill`: opprette nye skills med riktig struktur

## Flyt for synk av skills

```mermaid
flowchart LR
    A[Endring i dette repoet] --> B[".github/workflows/tms-copilot-sync.yml"]
    B --> C[Synk .github/skills/** til målrepo]
    C --> D[Oppretter PR kun ved endringer]
```

Repoet inneholder en reusable workflow for å kopiere `.github/skills/**` til teamrepoer:

```yaml
name: Skills Sync

on:
  schedule:
    - cron: '0 7 * * 1'
  workflow_dispatch:

jobs:
  sync:
    uses: navikt/tms-copilot/.github/workflows/tms-copilot-sync.yml@main
    permissions:
      contents: write
      pull-requests: write
```

Workflowen kopierer bare skill-mapper, oppretter PR bare når noe faktisk er endret, og lar eventuelle ekstra lokale skills i målrepoet ligge urørt.

## Utvikling

Dette repoet publiserer ikke en egen app med lokal URL. For oppdatert oversikt over automatisering og tilgjengelige workflows, bruk `gh workflow list` eller se `.github/workflows/`.

## For Nav-ansatte

Kontakt teamet i [#team-minside på Slack](https://nav-it.slack.com/app_redirect?channel=team-minside).