# Conflux Skills

Skill di Claude per i processi di design UX e UI di Conflux. Nascono dal lavoro quotidiano dello studio e sono pensate per i designer del team. Il repository è un progetto indipendente, sviluppato da un designer di Conflux e non gestito ufficialmente dallo studio.

Le skill si installano in Claude Code come plugin. Il repository funziona da catalogo: lo si aggiunge una volta, poi si installano le skill che servono.

## Skill disponibili

| Skill | A cosa serve | Versione |
| --- | --- | --- |
| [conflux-ds-guidelines-gen](plugins/conflux-ds-guidelines-gen/README.md) | Documenta le regole di un design system in Figma e produce Regolamento, Guida di onboarding e Violazioni | 0.1.0 |

## Installazione

Servono Claude Code installato e un terminale. I comandi si scrivono nel terminale, non nella chat di Claude.

Aggiungi il catalogo `conflux-skills`, una volta sola:

```bash
claude plugin marketplace add m4zekeeper/conflux-skills
```

Installa la skill che ti serve, per esempio:

```bash
claude plugin install conflux-ds-guidelines-gen@conflux-skills
```

Riavvia Claude Code. Da quel momento la skill è disponibile in tutti i progetti.

## Aggiornamento

Quando esce una versione nuova di una skill, scarica il catalogo aggiornato:

```bash
claude plugin marketplace update conflux-skills
```

Poi aggiorna la skill e riavvia Claude Code:

```bash
claude plugin update conflux-ds-guidelines-gen@conflux-skills
```

La versione installata e quella pubblicata si confrontano nella tabella *Skill disponibili*.

## Per chi mantiene il repository

Ogni skill ha una copia di lavoro sul computer di chi la sviluppa, e il repository riceve una copia a ogni pubblicazione. Le modifiche vanno sempre dalla copia di lavoro al repository: un file modificato direttamente su GitHub viene sovrascritto alla pubblicazione successiva.

A ogni pubblicazione si alza il numero di versione in `plugins/<skill>/.claude-plugin/plugin.json` e nella tabella *Skill disponibili*. Senza una versione nuova, Claude Code non propone l'aggiornamento a chi ha già installato la skill.
