# Conflux Design System Guidelines Generator

Nome per l'installazione: `conflux-ds-guidelines-gen`.

> **Versione 0.2.0, in rifinitura.** La skill è in uso ma cambia spesso. È stata provata su un file Figma reale, e le correzioni emerse dalla prova sono in corso.

## A cosa serve

La skill documenta le regole di un design system o di una design library in Figma. Le regole servono ai designer che entrano nel progetto, e a un'IA se il team ne usa una, per lavorare rispettando come il file è costruito.

La skill copre il naming di pagine, layer, componenti, proprietà e token, l'organizzazione di flussi e schermate, e le procedure di lavoro del team.

## Cosa produce

La skill scrive quattro documenti markdown in una cartella. I quattro documenti nascono da un'unica base di regole e si aggiornano sempre insieme.

| File | Contenuto | Per chi |
| --- | --- | --- |
| `00_Start.md` | Cosa contiene il pacchetto, in che ordine leggerlo, come darlo a un'IA | Chi riceve il pacchetto |
| `01_Onboarding.md` | La Guida di onboarding: mappa del file, flusso di lavoro, compiti tipici, errori da evitare | Chi entra nel progetto |
| `02_Regole.md` | Il Regolamento: ogni regola con un ID stabile | Chi lavora sul file, e l'IA |
| `03_Violazioni.md` | Ciò che nel file di oggi non segue le regole, con la forma corretta e l'azione da fare | Chi mantiene il design system |

## Come funziona

La skill lavora con l'owner, cioè il designer responsabile del design system. La skill decide da sola tutto ciò che può decidere con buona accuratezza, e chiede all'owner solo i punti che il file e gli standard non chiudono.

1. **Impostazione.** La skill chiede il link al file Figma, la cartella dei documenti, la lingua e il modo in cui il pacchetto verrà condiviso.
2. **Analisi del file.** La skill legge il file Figma in sola lettura e ricava le convenzioni dominanti, cioè le forme seguite da almeno due terzi degli elementi. Gli elementi che deviano finiscono nelle Violazioni.
3. **Intervista all'owner.** La skill chiede il contesto, fa scegliere la regola dove nel file convivono due forme, e raccoglie i fatti che solo il team conosce. In chiusura mostra un Elenco di revisione con le regole decise da sola, e l'owner toglie o corregge ciò che non vuole.
4. **Stesura.** La skill scrive i quattro documenti. Nel Regolamento entrano solo regole approvate dall'owner.

Oltre alla creazione del pacchetto, la skill ha altre due modalità:

- **Aggiungi regola**: l'owner porta una regola nuova o corregge una regola esistente, e la skill aggiorna i documenti;
- **Riallinea**: il file Figma è cambiato, e la skill confronta il Regolamento con il file e propone gli aggiornamenti.

## Cosa serve

- Claude Code, con la skill installata come spiegato nel [README del repository](../../README.md).
- Il server MCP ufficiale di Figma collegato a Claude Code, e il plugin Figma per Claude Code, che fornisce la skill `figma-use` usata nell'analisi.
- Accesso in lettura al file Figma del design system.

## Come si avvia

In Claude Code basta chiedere, per esempio:

- "Prepara il documento di onboarding per il design system in questo file Figma", con il link al file;
- "Aggiungi una regola al regolamento del design system";
- "Riallinea il regolamento al file Figma".
