# Conflux Design System Guidelines Generator

Nome per l'installazione: `conflux-ds-guidelines-gen`.

> **Versione 0.2.0, in rifinitura.** La skill è in uso ma cambia spesso. È stata provata su un file Figma reale, e le correzioni emerse dalla prova sono in corso.

## A cosa serve

La skill documenta le regole di un design system o di una design library in Figma. Le regole servono ai designer che entrano nel progetto, e a un'IA se il team ne usa una, per lavorare rispettando come il file è costruito.

La skill copre il naming di pagine, layer, componenti, proprietà e token, l'organizzazione di flussi e schermate, e le procedure di lavoro del team.

La skill lavora con l'owner, cioè il designer responsabile del design system.

## Cosa fa, in dettaglio

### Analisi del file Figma

- Legge la struttura delle pagine: prefissi, sezioni, ordine e pagine di servizio come esplorazioni, changelog e mirror di piattaforma.
- Legge variabili e collection: nomi, mode, alias, scope, description e code syntax. Distingue i token primitivi dai token semantici.
- Legge gli stili di testo, colore, effetto e griglia, e ne ricava la convenzione di nome e la scala.
- Legge componenti e proprietà: nomi, assi di variante, ordine dei valori, proprietà booleane, di testo, instance swap e slot, description.
- Riconosce i nomi con più significati, per esempio un asse `Type` che in un componente indica il colore semantico e in un altro la forma.
- Distingue la documentazione scritta dal team da quella del kit di partenza, e chiede all'owner quale delle due descrive il lavoro del team.
- Segnala le istanze che vengono da library esterne e i componenti che non esistono più nel file.
- Legge i file di lavoro con flussi e schermate, se esistono, e ne ricava le convenzioni di naming e gli stati delle Section.

### Regole

- Considera una forma una convenzione quando la seguono almeno due terzi degli elementi, e riporta sempre il conteggio.
- Chiede all'owner solo i conflitti, i fatti che il file non contiene e le scelte che cambiano variabili già usate dallo sviluppo.
- Propone regole di default per le pratiche di lavoro: fonti ammesse, naming dei layer, detach, token, creazione e deprecazione dei componenti, accessibilità secondo WCAG 2.2 AA.
- Propone le regole per l'organizzazione dei file di lavoro anche quando quei file non esistono ancora.
- Dà a ogni regola un ID stabile, un dominio e una fonte: file, documentazione del file, standard o owner.

### Manutenzione dei documenti

- **Modalità "Aggiungi regola"**: formalizza una regola nuova o corretta, controlla duplicati e contraddizioni, conta gli elementi del file che la violano e assegna l'ID.
- **Modalità "Riallinea"**: ripete l'analisi sul file cambiato, segnala regole non più rispettate, convenzioni nuove e violazioni risolte, e aggiorna i documenti dopo la conferma dell'owner.
- Converte le cartelle create da versioni precedenti della skill.

## Cosa non fa

- Non modifica di propria iniziativa le regole decise dall'owner: segnala la differenza e chiede.
- Non modifica il file Figma: l'analisi è in sola lettura, e le correzioni elencate nelle Violazioni restano al team.
- Non costruisce componenti, non fa critiche visive o di accessibilità delle schermate e non genera codice.
- Non lavora senza l'owner: l'owner risponde alle domande della skill, e una regola entra nel Regolamento solo dopo la sua approvazione.
- Nei gruppi con più di 300 componenti, stili o variabili lavora su statistiche e su un campione, e lo dichiara nelle Violazioni.

## Cosa produce

La skill scrive quattro documenti markdown in una cartella. I quattro documenti nascono da un'unica base di regole e si aggiornano sempre insieme.

| File | Contenuto | Per chi |
| --- | --- | --- |
| `00_Start.md` | Cosa contiene il pacchetto, in che ordine leggerlo, come darlo a un'IA | Chi riceve il pacchetto |
| `01_Onboarding.md` | La Guida di onboarding: mappa del file, flusso di lavoro, compiti tipici, errori da evitare | Chi entra nel progetto |
| `02_Regole.md` | Il Regolamento: ogni regola con un ID stabile | Chi lavora sul file, e l'IA |
| `03_Violazioni.md` | Ciò che nel file di oggi non segue le regole, con la forma corretta e l'azione da fare | Chi mantiene il design system |

## Requisiti

- Claude Code, con la skill installata come spiegato nel [README del repository](../../README.md).
- Il server MCP ufficiale di Figma collegato a Claude Code, e il plugin Figma per Claude Code, che fornisce la skill `figma-use` usata nell'analisi.
- Accesso in lettura al file Figma del design system.

## Come si avvia

In Claude Code basta chiedere, per esempio:

- "Prepara il documento di onboarding per il design system in questo file Figma", con il link al file;
- "Aggiungi una regola al regolamento del design system";
- "Riallinea il regolamento al file Figma".

## Come funziona

La creazione del pacchetto segue quattro passi.

1. **Impostazione.** La skill chiede il link al file Figma, la cartella dei documenti, la lingua e il modo in cui il pacchetto verrà condiviso.
2. **Analisi del file.** La skill legge il file Figma e ne ricava le convenzioni. Gli elementi che deviano dalle convenzioni finiscono nelle Violazioni.
3. **Intervista all'owner.** La skill chiede il contesto, fa scegliere la regola dove nel file convivono due forme, e raccoglie i fatti che solo il team conosce. In chiusura mostra un Elenco di revisione con le regole decise da sola, e l'owner toglie o corregge ciò che non vuole.
4. **Stesura.** La skill scrive i quattro documenti. Nel Regolamento entrano solo regole approvate dall'owner.
