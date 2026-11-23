---
name: conflux-ds-guidelines-gen
description: >-
  Usala quando l'utente vuole documentare le regole di un design system o di una design library in Figma, perché designer nuovi (ed eventualmente Claude) lavorino rispettando come il file è costruito: naming di pagine, layer, componenti, proprietà, token, flussi e schermate, e le procedure di lavoro. Produce un pacchetto di documenti da un'unica base di regole: il Regolamento (regole con ID, per chi deve rimanere sul pezzo e per l'IA), la Guida di onboarding (narrativa, per chi entra nel progetto), le Violazioni (l'elenco di ciò che nel file di oggi non segue le regole e va corretto) e il file Start, che indica l'ordine di lettura. Trigger: "documento di onboarding del design system", "onboardare i designer sulla library", "regole del DS", "linee guida tecniche del file Figma", "convenzioni di naming della library", "documento di riferimento per Claude sul design system", "aggiungi una regola al regolamento", "riallinea il regolamento al file", o un link figma.com a una library con la richiesta di estrarne le regole. Vale anche quando l'utente vuole aggiungere una regola di processo a un regolamento già esistente o verificare se il regolamento è ancora allineato al file. NON serve a costruire o modificare componenti in Figma, a fare una critica visiva o di accessibilità di schermate, né a generare codice dal design.
---

# Conflux DS Guidelines Gen — dal file Figma al Regolamento e alla Guida di onboarding

Questa skill trasforma un design system in Figma in un pacchetto di documenti markdown che vivono nella stessa cartella e si aggiornano sempre insieme.

- **Il Regolamento** (`02_Regole.md`) contiene le regole, ognuna con un ID stabile. Il designer lo consulta per ricordarsi come si fa una cosa. Se il team usa un'IA, l'IA lo legge prima di qualunque lavorazione sul file.
- **La Guida di onboarding** (`01_Onboarding.md`) accompagna chi entra nel progetto: mappa del file, flusso di lavoro, compiti tipici, errori da evitare. La Guida non riscrive le regole: le riassume in una riga e rimanda all'ID del Regolamento.
- **Le Violazioni** (`03_Violazioni.md`) sono l'elenco di ciò che nel file di oggi non segue le regole: errori, incoerenze, elementi mancanti. Ogni riga indica la forma corretta, l'azione e la precauzione da prendere prima di correggere, e il documento porta la data dell'ultima analisi. Le Violazioni sono un'istantanea e invecchiano: per questo stanno fuori dal Regolamento.
- **Il file Start** (`00_Start.md`) spiega a chi riceve il pacchetto cosa contiene ogni file, in che ordine leggerlo e come darlo a un'IA, se qualcuno vuole farlo.

I documenti servono anche quando nessuno usa un'IA: il pacchetto può essere solo materiale condiviso fra designer. Per questo ogni documento si spiega da solo, e nessun documento presuppone che esista un `CLAUDE.md` nel progetto o che l'IA sia coinvolta nella gestione del design system.

Il motivo dei documenti separati è che i lettori hanno bisogni opposti. Chi consulta una regola, persona o IA, la vuole atomica, decidibile e senza prosa. Un designer nuovo ha bisogno di contesto e di un percorso. Il rimando per ID tiene ogni regola in un posto solo, così una modifica non può far divergere i documenti.

## Chi è l'owner

L'**owner** è il designer che ha la responsabilità del design system e richiama la skill. L'owner risolve i conflitti, fornisce i fatti che il file non contiene e approva le regole che la skill decide da sola. Una regola scelta o scritta dall'owner porta `Fonte: owner`, e nessuna rigenerazione la cancella o la riscrive senza chiederglielo.

## Chi decide cosa

L'owner deve prendere il minor numero possibile di decisioni. La skill decide da sola ciò che può decidere con buona accuratezza, e porta all'owner solo i punti che il file e gli standard non chiudono.

**La skill decide da sola in tre casi:**

- **Convenzione dominante.** Il file segue una forma con almeno due terzi degli elementi, il caso non è un conflitto secondo `references/analisi-figma.md`, *Come si deduce una convenzione*, e la forma non viene solo da materiale del fornitore che il team non segue. Gli elementi che deviano vanno nelle Violazioni.
- **Standard o pratica consolidata.** Uno standard esterno (WCAG 2.2 AA, linee guida di Apple o di Material, formato DTCG) o la pratica corrente del settore dà una sola risposta realistica. Le regole di questo tipo sono le regole di default di `references/intervista.md`, Blocco 3.
- **Conflitto minore.** Un conflitto che riguarda pochi elementi, secondo la soglia di `references/analisi-figma.md`, *Come si deduce una convenzione*. La skill applica la raccomandazione e porta il conflitto nell'Elenco di revisione, con l'alternativa.

**L'owner decide in quattro casi, con una domanda:**

- **Contesto.** Quale materiale del file descrive come lavora il team, se la library segue gli aggiornamenti del kit da cui deriva, la piattaforma primaria e il tema di consegna.
- **Conflitti.** I casi che `references/analisi-figma.md`, *Come si deduce una convenzione*, definisce come conflitto: nessuna forma raggiunge i due terzi, un nome ha più significati, la forma dominante contraddice uno standard. I conflitti minori sono esclusi, perché li decide la skill.
- **Lacune.** Fatti che solo il team conosce: lingue, ruoli, strumenti di handoff, uso dei componenti di forma nativa.
- **Costo alto.** Una scelta che cambia il nome o il code syntax di variabili che hanno già un code syntax, segno che lo sviluppo può usarle.

**Ogni decisione della skill passa dall'owner nell'Elenco di revisione**, a fine intervista. L'owner legge l'elenco e toglie o corregge le voci che non vuole. Leggere un elenco costa all'owner molto meno che rispondere a una domanda per regola, e permette comunque di intercettare una deduzione sbagliata.

Per ogni domanda di decisione la skill propone un'opzione raccomandata e ne spiega il motivo. Le domande di fatto non hanno raccomandazione (vedi `references/intervista.md`, *Regole di conduzione*). Quando l'owner delega ("scegli tu"), la skill applica la raccomandazione e la mostra per conferma prima di registrarla.

## Le tre modalità

Capisci dalla richiesta quale modalità serve. Se nella cartella indicata esiste già un `02_Regole.md`, la modalità Crea non si usa: proponi Riallinea o Aggiungi regola.

**Cartelle di una versione precedente.** Una cartella può contenere i documenti con i nomi di una versione precedente della skill: `README.md`, `onboarding.md`, `regolamento.md`, `eccezioni.md` oppure `violazioni.md`. In quel caso proponi all'owner di rinominarli con i nomi attuali prima di procedere, e aggiorna i rimandi nei testi. Se il Regolamento o le Violazioni hanno un frontmatter, sposta i dati nella forma attuale: nel Regolamento la sezione *Dati per l'aggiornamento*, nelle Violazioni la riga "Data dell'analisi" (vedi `references/formato-documenti.md`).

**Dati per l'aggiornamento mancanti.** Se il Regolamento non ha la sezione *Dati per l'aggiornamento*, o la sezione manca di qualche campo, non fermarti e non inventare i valori. Ricava dal file Figma l'URL e il nome del design system. Per `id_ritirati`, proponi gli ID che mancano nella sequenza di ogni dominio, e chiedi all'owner se ce ne sono altri: un ID ritirato che era l'ultimo del suo dominio non lascia buchi. Chiedi all'owner in un pannello tutti gli altri campi mancanti, poi riscrivi la sezione.

| Modalità | Quando | Cosa produce |
| --- | --- | --- |
| **Crea** | Primo pacchetto per un design system | I quattro file della cartella |
| **Aggiungi regola** | L'owner porta una regola nuova o corregge una esistente | Regolamento, Guida e Violazioni aggiornati |
| **Riallinea** | Il file Figma è cambiato e il Regolamento potrebbe non descriverlo più | Report delle differenze, poi i file aggiornati dopo conferma |

## Modalità Crea

### Passo 1 — Impostazione

Raccogli con `AskUserQuestion` ciò che non è già nella richiesta. Le voci con opzioni (file di lavoro, lingua, distribuzione) sono domande del pannello. Le voci a testo libero (link, cartella, nome e cognome dell'owner) si chiedono nel campo libero dello stesso pannello.

- il link al file Figma del design system;
- se esistono già file di lavoro (i file con flussi e schermate di prodotto) e, se esistono, i loro link;
- la cartella in cui scrivere i documenti (proponi `<cartella del progetto cliente>/design-system/`);
- la lingua dei documenti, che è la lingua del team che li userà. I nomi presi dal file Figma (pagine, componenti, proprietà, token) restano sempre nella forma originale;
- come verranno condivisi i documenti (vedi *Distribuzione* in fondo);
- il nome e il cognome dell'owner, che i documenti citano come riferimento per le domande e le modifiche.

**Le persone si citano con nome e cognome.** La regola vale per ogni persona che i documenti nominano: l'owner, la persona che approva, la persona di riferimento per i casi non coperti. Se una risposta dà solo il nome, chiedi una volta il cognome e spiega il motivo: un nome da solo diventa ambiguo quando il team cresce o il pacchetto passa ad altre persone. Se l'owner preferisce non indicarlo, accetta la risposta. Se l'owner indica un ruolo invece di una persona, per esempio "il PM del progetto", i documenti citano il ruolo, che resta vero anche quando la persona cambia.

**Se i file di lavoro non esistono ancora**, la skill non lascia scoperta la loro organizzazione. Il Regolamento deve comunque contenere le regole che permettono ai designer di creare quei file in modo coerente con la library: pagine dei flussi, nomi delle schermate, stati delle Section, esplorazione, componenti locali, consegna. Queste regole arrivano nell'Elenco di revisione come pacchetto di default, costruito sulle convenzioni della library (vedi `references/intervista.md`, *File di lavoro assenti*).

### Passo 2 — Analisi del file

Leggi `references/analisi-figma.md` e segui la procedura. L'analisi è in sola lettura: durante questa skill non si modifica nulla nel file Figma.

L'analisi produce un **inventario delle convenzioni**: per ogni ambito (pagine, componenti, proprietà, token, stili) la convenzione dominante, quante volte compare, e le deviazioni con il nome degli elementi che deviano. L'inventario segnala anche i nomi che hanno più significati (per esempio un asse `Type` che in alcuni componenti indica il colore semantico e in altri la forma) e l'origine della documentazione trovata nel file. L'inventario resta un appunto di lavoro e non va nei documenti finali.

L'inventario e gli elenchi delle deviazioni si salvano in una cartella di lavoro accanto alla cartella dei documenti, con il nome `<cartella dei documenti>-lavoro/`. La cartella di lavoro non fa parte del pacchetto e non si condivide.

Prima di passare all'intervista, mostra all'owner una sintesi dell'inventario: cosa hai letto, cosa non sei riuscito a leggere e perché. Un'analisi parziale dichiarata vale più di un'analisi che sembra completa e non lo è.

### Passo 3 — Intervista all'owner

Leggi `references/intervista.md`. L'intervista ha quattro blocchi, in quest'ordine:

1. **Contesto.** Uno o due pannelli chiedono quale materiale del file descrive come lavora il team, se la library segue gli aggiornamenti del kit, la piattaforma primaria e il tema di consegna. Le risposte decidono quali convenzioni del file valgono come convenzioni del team, e su quale piattaforma si basano le raccomandazioni.
2. **Conflitti.** Dove nel file convivono due forme per la stessa cosa, o lo stesso nome ha più significati, l'owner decide quale è la regola. Ogni opzione dice quanti elementi del file finirebbero fuori regola. I conflitti minori non diventano domande: vanno nell'Elenco di revisione.
3. **Lacune.** Per le aree di processo che dipendono dal team, chiedi all'owner la regola. Le altre aree di processo le copre la skill con regole di default.
4. **Elenco di revisione.** Mostra all'owner in un unico elenco tutte le regole decise dalla skill, con i gruppi elencati in `references/intervista.md`, *Contenuto dell'elenco*. L'owner toglie o corregge ciò che non vuole.

L'owner può aggiungere regole libere in qualunque momento dell'intervista. Una regola libera si formalizza con il formato di `references/formato-documenti.md` e si rilegge con l'owner prima di registrarla. Se la regola cita un componente, uno stile o una variabile, verifica che esista nel file. Se non esiste, dillo all'owner: l'elemento mancante entra nelle Violazioni come elemento da creare.

Se una risposta contraddice una risposta precedente o una regola già raccolta, mostra le due regole affiancate e chiedi quale prevale. Prima di comporre l'Elenco di revisione, confronta fra loro le regole che hanno lo stesso ambito e risolvi allo stesso modo ogni contraddizione rimasta.

### Passo 4 — Stesura

Leggi `references/formato-documenti.md` e scrivi i quattro file. Prima di consegnarli, esegui la *Verifica di stesura* e poi il *Controllo di qualità* qui sotto.

I conteggi dei documenti si ricavano dagli elenchi salvati nella cartella di lavoro, non dalla memoria dell'intervista. Ogni lettura del file durante la stesura segue le regole di `references/analisi-figma.md`, *Come leggere molte pagine*.

**Verifica di stesura.** La stesura rilegge il file e può trovare ciò che l'intervista non ha visto. Prima della consegna raccogli in un pannello, con le regole di conduzione di `references/intervista.md`, tre tipi di punti:

- le decisioni che la stesura richiede e che né le risposte dell'owner né l'Elenco di revisione hanno fissato, per esempio la forma corretta di un elemento o il valore di una variabile. Ognuna è una domanda di decisione, con la raccomandazione e l'impatto;
- i conteggi cambiati rispetto all'Elenco di revisione approvato, ognuno con il valore mostrato all'owner e quello corretto;
- le domande già risposte in cui un conteggio cambiato inverte il confronto fra le opzioni. Queste domande si ripresentano.

Prima di inserire una decisione nel pannello, verifica se un fatto del file o del funzionamento di Figma la chiude già. In quel caso la decisione non è una domanda, e si dichiara alla consegna fra le tue interpretazioni. Esempio: una proprietà booleana di Figma può solo mostrare o nascondere un layer, quindi una proprietà che fa questo resta booleana.

Una scelta dell'owner nella Verifica di stesura porta `Fonte: owner`, come ogni risposta dell'intervista. Se la verifica non trova nulla, dillo all'owner in una riga e passa alla consegna. Un documento consegnato non contiene mai una decisione in attesa o una proposta da confermare.

Alla consegna mostra all'owner, in un messaggio e non in un file del pacchetto, quattro cose:

- l'elenco delle regole con ID e fonte;
- le **scelte che non corrispondono al file com'è oggi**: per ogni regola violata dal file, quanti elementi la violano e la precauzione che la correzione richiede;
- i punti rimasti senza regola per scelta dell'owner;
- le tue interpretazioni delle risposte dell'owner.

Se il report di consegna va salvato, si salva nella cartella di lavoro.

## Modalità Aggiungi regola

1. Leggi `02_Regole.md`, `01_Onboarding.md` e `03_Violazioni.md` dalla cartella.
2. Riformula la richiesta dell'owner nel formato regola. Se la richiesta contiene parole non decidibili ("possibilmente", "prioritariamente", "quando serve"), chiedi il criterio che le rende decidibili.
3. Cerca nel Regolamento le regole con lo stesso ambito. Se la regola nuova duplica una regola esistente, proponi di modificare quella esistente. Se la contraddice, mostra le due regole affiancate e chiedi quale prevale.
4. Se la regola cita un elemento del file, verifica che esista. Se la regola riguarda qualcosa di osservabile nel file, conta quanti elementi oggi la violano, e dillo all'owner prima di registrarla. Gli elementi che la violano vanno nelle Violazioni con l'azione prevista da `references/intervista.md`, *Ambito e azione predefiniti*, e la regola prende il rimando fisso alle Violazioni (vedi `references/formato-documenti.md`).
5. Assegna il primo ID libero del dominio. Un ID ritirato non si riusa (vedi `id_ritirati` nella sezione *Dati per l'aggiornamento* del Regolamento).
6. Aggiorna la Guida di onboarding se la regola tocca un compito tipico, un errore da evitare o la checklist.
7. Mostra all'owner il testo della regola e le righe cambiate negli altri file prima di scriverle.

Una regola modificata conserva il suo ID. Una regola abrogata esce dal Regolamento e il suo ID entra in `id_ritirati`.

## Modalità Riallinea

1. Leggi i file della cartella e ripeti l'analisi del Passo 2 sul file Figma. Per decidere quale materiale vale come materiale del team usa le risposte del Blocco 1 registrate nella sezione *Dati per l'aggiornamento* del Regolamento, senza richiederle.
2. Confronta l'inventario nuovo con il Regolamento e prepara un report con quattro gruppi: regole che il file non rispetta più, convenzioni nuove che nessuna regola copre, pagine o componenti nuovi da inserire nella mappa, righe delle Violazioni che sono state sistemate.
3. Per le regole con `Fonte: owner` non proporre modifiche di iniziativa: segnala la divergenza e chiedi.
4. Le convenzioni nuove passano da un Elenco di revisione ridotto, con le stesse regole del Blocco 4 di `references/intervista.md`. I conflitti nuovi diventano domande, salvo i conflitti minori, che entrano nell'Elenco di revisione ridotto.
5. Dopo la conferma dell'owner aggiorna i file e riscrivi le Violazioni con la nuova data. L'azione di ogni riga viene dal campo Ambito della regola, non si ricalcola. Togli il rimando fisso dalle regole che non hanno più violazioni, e aggiungilo a quelle che ne hanno di nuove.

## Controllo di qualità

I documenti possono essere letti da persone e da IA che non conoscono il progetto e non hanno le istruzioni dell'owner. Ogni documento deve quindi bastare a se stesso. Prima di consegnare, verifica ogni punto e correggi ciò che non passa.

- **Un nome per ogni cosa.** Ogni pagina, componente, stato e collection compare con lo stesso nome e la stessa grafia in tutti i documenti. Il nome canonico è quello presente nel file Figma, oppure quello che una regola impone quando lo cambia; in questo caso la corrispondenza con il nome di oggi sta solo nelle Violazioni. Il Glossario del Regolamento elenca i nomi canonici. Esempio di errore da evitare: "Ready for Dev" in una sezione e "Ready for dev" in un'altra.
- **I nomi del file sono in codice, e solo loro.** Ogni nome elencato nel Glossario, alla voce *Nomi del file*, compare in codice inline in tutti i documenti, titoli esclusi; nessun termine di Figma, concetto generico o nome di prodotto è in codice. La regola sta in `references/formato-documenti.md`, *Nomi del file in codice*.
- **Nessun calco dei termini tecnici.** Un termine tecnico inglese si traduce solo se l'equivalente nella lingua del documento ha lo stesso significato nel settore. Altrimenti resta in inglese. Esempio di errore da evitare: "tone" tradotto con "tono", che in italiano indica una sfumatura o un registro e non il colore semantico. La regola completa e gli esempi stanno in `references/formato-documenti.md`, *Terminologia tecnica*.
- **Ogni regola è decidibile.** Davanti a un caso concreto, la regola dice sì o no senza interpretazione. Se ammette eccezioni, le elenca.
- **Nessuno stato nel Regolamento e nella Guida.** Una frase che diventerà falsa senza che nessuno modifichi il documento va nelle Violazioni o fuori dai documenti. Esempi: "oggi il Badge usa ancora State", "da decidere", conteggi di componenti. Il rimando fisso alle Violazioni è ammesso, perché resta vero finché la regola ha violazioni.
- **Nessuna regola duplicata nella Guida.** La Guida riassume in una riga e cita l'ID.
- **Ogni regola ha la fonte.** `file`, `documentazione del file`, `standard` o `owner`.
- **Gli ID sono unici e i rimandi esistono.** Ogni ID citato nella Guida, nella checklist e nelle Violazioni esiste nel Regolamento. Ogni regola con righe nelle Violazioni porta il rimando fisso, e ogni rimando fisso punta a una sezione esistente delle Violazioni. Il Riepilogo delle Violazioni ha una riga per ogni sezione, e i suoi numeri corrispondono alle righe delle tabelle.
- **Ogni elemento citato esiste o è nelle Violazioni.** Un componente, uno stile o una variabile citati da una regola, o dalla forma corretta di una riga delle Violazioni, esistono nel file oppure compaiono nelle Violazioni come elementi da creare. Un elemento da creare non si descrive mai come disponibile: la regola che lo cita porta il campo *Da creare*.
- **Le tabelle si leggono in ogni visualizzatore.** Ogni tabella rispetta le quattro condizioni di `references/formato-documenti.md`, *Tabelle*: nessun rientro e nessuna tabella dentro un punto di lista, righe vuote prima e dopo, stesso numero di celle in ogni riga, barre verticali nelle celle scritte `\|`.
- **I dati per l'aggiornamento sono completi.** Il Regolamento chiude con la sezione *Dati per l'aggiornamento*, preceduta da una linea orizzontale, con la nota fissa e tutti i campi della tabella. Le Violazioni hanno la riga "Data dell'analisi" subito sotto il titolo. Nessun documento ha frontmatter.
- **Le regole non si contraddicono.** Nessuna regola contraddice un'altra, e ogni esempio *Corretto* rispetta tutte le regole del Regolamento, non solo la propria.
- **Ogni regola è passata dall'owner.** Una regola entra nel Regolamento solo se viene da una risposta dell'owner, oppure se l'owner l'ha lasciata nell'Elenco di revisione. Una tua interpretazione di una risposta dell'owner si dichiara nel report di consegna.

## Distribuzione

La cartella è l'unica fonte. Qualunque copia dei documenti fuori dalla cartella (un Project di claude.ai, un Google Doc, una pagina Notion) si rigenera dalla cartella e non si modifica a mano. Una modifica fatta su una copia non arriva mai al Regolamento.

Alla prima esecuzione chiedi all'owner come verranno condivisi i documenti, e registra la scelta nella sezione *Dati per l'aggiornamento* del Regolamento (`distribuzione`):

- **`cartella-condivisa`**: la cartella sta su un servizio condiviso come Google Drive o Dropbox, e i colleghi la leggono da lì.
- **`repository`**: la cartella è un repository Git condiviso.
- **`project`**: i documenti vengono caricati in un progetto condiviso di uno strumento IA, per esempio un Project di claude.ai o un notebook di NotebookLM.
- **`solo-owner`**: solo l'owner usa i documenti, e ai colleghi arrivano copie leggibili.

La skill non dà per scontato che i colleghi usino un'IA. Il file Start spiega in ogni caso come darle il pacchetto. Se l'owner chiede che l'IA legga il Regolamento in automatico in un progetto che ha già un `CLAUDE.md`, proponi la riga da aggiungere a quel file e scrivila solo dopo l'ok dell'owner.

Alla fine di ogni modalità ricorda all'owner quali copie vanno riallineate, in base al valore di `distribuzione`.
