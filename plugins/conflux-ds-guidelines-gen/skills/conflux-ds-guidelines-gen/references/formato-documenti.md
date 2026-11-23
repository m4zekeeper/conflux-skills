# Formato dei documenti

Questo file definisce il formato della regola, la terminologia tecnica e la struttura dei quattro file della cartella. I testi fissi qui sotto vanno tradotti nella lingua scelta dall'owner. I nomi presi dal file Figma restano nella forma originale.

In tutti i file markdown un paragrafo e un punto di lista occupano una riga sola, senza a capo forzati.

**Tabelle.** Molti visualizzatori di markdown mostrano il testo grezzo, con le barre verticali in vista, quando una tabella non ha la forma attesa. Ogni tabella dei documenti rispetta quindi quattro condizioni:

- la tabella parte dalla prima colonna, senza rientro, e non sta mai dentro un punto di lista;
- una riga vuota la precede e una riga vuota la segue;
- la seconda riga è quella dei trattini, e ogni riga ha lo stesso numero di celle dell'intestazione;
- una barra verticale dentro una cella si scrive `\|`, anche dentro il codice. Esempio: `Size=sm\|md\|lg`. I valori di variante contengono quasi sempre barre verticali, quindi la condizione vale in quasi ogni tabella di questi documenti.

**Nomi del file in codice.** Ogni nome presente nel file Figma si scrive in codice inline, esattamente come compare nel file, in tutti i documenti: pagine e sezioni (`✦ Components`, `Playground`), frame e Section con un nome (`Top Bars [Components]`), componenti (`Badge`), proprietà e valori (`Size=sm`), variabili e stili (`bg/surface`), nomi di layer, stati delle Section, e le forme scorrette prese dal file (`Size=Small`). Il criterio è uno solo: un nome in codice si cerca nel file e si trova così com'è. Non vanno in codice i termini di Figma e della sua interfaccia (Section, pannello Assets, Dev Mode, instance swap), i concetti generici ("il componente", "un badge" come tipo di elemento) e i nomi di prodotti che non sono nomi del file (iOS, Material, il nome del design system). Nei titoli non si usa il codice inline: i titoli descrivono, non citano nomi del file. Nelle tabelle il codice segue la stessa regola del testo.

**Note Attenzione.** Un avvertimento su un'azione che produce danni se ignorata sta in una nota separata dal testo, non dentro un paragrafo o un punto di lista. La nota è una citazione che si apre con l'etichetta in grassetto, tradotta nella lingua del documento: `> **Attenzione.** <testo>`. Il testo dice cosa non fare o cosa controllare, e perché, in non più di tre frasi, e non contiene elenchi. Al massimo due note per sezione: oltre, smettono di farsi notare. I punti in cui la nota è prevista sono indicati nei modelli qui sotto.

## Terminologia tecnica

Il lessico di Figma e dei design system è nato in inglese, e molti termini non hanno un equivalente esatto in altre lingue. Una traduzione letterale che in italiano significa un'altra cosa confonde designer e IA più di un termine lasciato in inglese.

**La regola.** Un termine tecnico si traduce solo quando esiste un equivalente d'uso consolidato nel settore con lo stesso significato. In tutti gli altri casi resta in inglese, in carattere `codice` solo quando è un nome del file o un valore, secondo *Nomi del file in codice*. Il termine scelto entra nella seconda tabella del Glossario e da lì non cambia più.

| Termine inglese | Nel documento | Motivo |
| --- | --- | --- |
| tone (colore semantico) | "colore semantico", oppure `Tone` se è il nome di un asse | "Tono" in italiano indica una sfumatura di colore o un registro di voce, non un ruolo semantico. |
| intent | "colore semantico", oppure `Intent` se è il nome di un asse | "Intento" non ha questo uso nel settore. |
| emphasis | enfasi | Equivalente consolidato. |
| component, instance, variant, property | componente, istanza, variante, proprietà | Equivalenti consolidati e usati anche nell'interfaccia di Figma. |
| override, detach, slot, scope, mode, token, auto layout | invariati | Il calco italiano ("sovrascrittura", "stacco", "modalità") non è usato con questo significato, o è ambiguo. |
| Section (nodo di Figma) | Section, con la maiuscola e senza codice | "Sezione" si confonde con le sezioni di pagine del file (es. `✦ Components`). È un termine di Figma, non un nome del file, quindi non va in codice. |
| handoff | handoff | "Consegna" è ammesso solo nel senso generico di consegnare un lavoro. |
| leading, trailing | `Leading`, `Trailing` | "Iniziale" e "finale" perdono il riferimento al verso di lettura. |
| touch target, tap target | touch target | "Area tappabile" è un calco dall'inglese *tappable*, senza uso nel settore. |

La tabella è un punto di partenza. Per ogni termine nuovo applica la regola e, nel dubbio, lascia il termine in inglese e aggiungilo al Glossario.

## Domini e ID

Ogni regola ha un ID formato da prefisso di dominio e numero a due cifre: `NAM-04`. Il numero non dice nulla sull'importanza: è solo l'ordine di inserimento.

| Prefisso | Dominio |
| --- | --- |
| `GEN` | Regole generali: lingue, valori fissi, temi di consegna, ruoli |
| `FON` | Fonti ammesse: da dove si prendono istanze, stili, icone, immagini e altri asset |
| `NAM` | Naming di pagine, Section, schermate, layer, componenti e proprietà |
| `TOK` | Token, variabili e stili: quale usare, come crearne di nuovi |
| `CMP` | Uso dei componenti nelle schermate |
| `LIB` | Creazione, modifica, deprecazione e pubblicazione nella library |
| `WRK` | Organizzazione dei file di lavoro: flussi, stati delle Section, esplorazione, componenti locali |
| `CNT` | Contenuti: copy e dati delle schermate |
| `ACC` | Accessibilità |
| `HND` | Annotazioni e handoff |

Un dominio senza regole non compare nel Regolamento.

## Formato della regola

```markdown
#### NAM-04 · Assi di variante: nomi e ordine dei valori

- **Regola:** Gli assi di variante di un componente nuovo o modificato usano questi nomi, in quest'ordine: Type, Style, Size, State, Selected. I valori di Size sono `xs`, `sm`, `md`, `lg`, `xl`, in minuscolo e in ordine crescente.
- **Ambito:** library, componenti nuovi o modificati. Elementi esistenti: alla prossima modifica.
- **Corretto:** `Size=xs|sm|md|lg|xl`
- **Scorretto:** `Size=Small|Default|Large`
- **Eccezioni:** I componenti sotto `✦ Apple Platform` e `✦ Google Material 3 Platform` seguono la terminologia del sistema operativo.
- **Verifica:** Nel pannello proprietà del component set, i nomi degli assi e l'ordine dei valori corrispondono alla regola.
- **Elementi esistenti:** Alcuni elementi del file non rispettano questa regola: elenco e correzioni in `03_Violazioni.md`, alla voce NAM-04.
- **Perché:** Un nome di asse diverso per lo stesso concetto obbliga chi usa il componente a ricordare un'eccezione per ogni componente.
- **Fonte:** owner
```

Indicazioni per ogni campo:

- **Regola.** Una o più frasi imperative e decidibili. Se la regola contiene un elenco di valori ammessi, l'elenco sta nella regola, anche in forma di tabella. Una tabella non sta dentro il campo: interrompe l'elenco dei campi subito dopo il campo Regola, con una riga vuota prima e una dopo, e l'elenco riprende dal campo successivo. Il campo Regola la cita con "secondo la tabella qui sotto". Una struttura su più righe, come l'albero dei layer di un componente o i frame di primo livello di una pagina, sta allo stesso modo in un blocco di codice dichiarato `text`, e il campo Regola la cita con "secondo la struttura qui sotto". Esempio:

````markdown
- **Regola:** Una pagina di componente ha due frame di primo livello e una Section per le parti interne, secondo la struttura qui sotto.

```text
❖ Top Bars
├── Top Bars [Components]
├── Top Bars [Examples]
└── _Unpublished Components   (Section)
```

- **Ambito:** library. Elementi esistenti: correggere.
````
- **Ambito.** Dove vale: library, file di lavoro, schermata, token, componente nuovo, componente esistente. Quando il file ha elementi che violano la regola, il campo chiude con l'azione decisa per loro: "Elementi esistenti: correggere", "alla prossima modifica" oppure "tollerare". L'azione è una decisione e resta vera finché qualcuno non la cambia; la modalità Riallinea la rilegge da qui invece di ricalcolarla.
- **Corretto / Scorretto.** Esempi concreti, con nomi realistici del file. Sono il campo che riduce di più gli errori: non ometterli quando la regola riguarda un nome o un valore.
- **Eccezioni.** Le eccezioni ammesse dalla regola, elencate. Se non ce ne sono, il campo si omette. Gli elementi che oggi violano la regola non sono eccezioni ammesse: vanno nelle Violazioni.
- **Verifica.** Come si controlla in Figma che la regola è rispettata.
- **Elementi esistenti.** Il rimando fisso alle Violazioni, presente solo quando le Violazioni hanno almeno un elemento per questa regola. Il testo è sempre lo stesso e non contiene nomi né conteggi, così resta vero mentre l'elenco si accorcia. Il campo dice anche a chi corregge un elemento esistente dove trovare la forma corretta.
- **Da creare.** Presente solo quando la regola cita un componente, uno stile o una variabile che il file non contiene ancora. Il testo è sempre lo stesso: "Questa regola cita elementi che il file non contiene ancora: elenco in `03_Violazioni.md`, alla voce Elementi da creare."
- **Perché.** Facoltativo. Si scrive quando il motivo non è evidente e aiuta a decidere i casi che la regola non nomina. Per una regola con `Fonte: standard`, il campo nomina lo standard.
- **Fonte.** Quattro valori:
  - `file`: convenzione dominante dedotta dal file, oppure forma del file raccomandata in un conflitto minore, approvata dall'owner nell'Elenco di revisione;
  - `documentazione del file`: regola scritta o adottata dal team nel materiale del file, e approvata nell'Elenco di revisione;
  - `standard`: regola di default presa da uno standard esterno o dalla pratica corrente del settore, compreso il pacchetto per i file di lavoro e la forma raccomandata in un conflitto minore quando il file non la usa, e approvata nell'Elenco di revisione;
  - `owner`: regola che l'owner ha scelto in una domanda, ha scritto come regola libera, ha confermato dopo una delega, oppure ha corretto nell'Elenco di revisione.

## `02_Regole.md`

```markdown
# Regolamento — <nome del design system>

## Come si usa questo documento
## Glossario
### Nomi del file
### Termini tecnici
## Mappa del file
## Regole
### Regole generali (GEN)
#### GEN-01 · <titolo della regola>
…un titolo di livello 3 per ogni dominio presente, nell'ordine della tabella dei domini, e sotto ogni dominio un titolo di livello 4 per ogni regola…
## Checklist

---

## Dati per l'aggiornamento
```

Il Regolamento non ha frontmatter: i dati che la skill usa per aggiornare il pacchetto stanno nella sezione *Dati per l'aggiornamento*, l'ultima del documento. Così la prima cosa che si vede aprendo il file, in qualunque visualizzatore, è il titolo.

I domini hanno titoli di livello 3 e le regole titoli di livello 4, così l'indice del documento mostra le regole dentro il loro dominio.

### Testo fisso di "Come si usa questo documento"

Questa sezione vale per chiunque consulti il Regolamento, persona o IA, e va riportata integralmente, tradotta nella lingua del documento. `<persona di riferimento>` è la persona indicata nella regola sui ruoli come riferimento per i casi non coperti; se la regola non ne indica una, è l'owner.

- Il Regolamento contiene le regole per creare, modificare e nominare gli elementi del design system <nome> e dei file di lavoro che lo usano. Ogni regola ha un ID, che la Guida di onboarding e le Violazioni citano.
- Le regole prevalgono su ciò che si osserva nel file. Il file contiene elementi che violano le regole: sono elencati in `03_Violazioni.md`, con la forma corretta, e non vanno presi come modello.
- Prima di scrivere un nome, controlla il Glossario e la regola di naming dell'elemento. Un nome che non è nel Glossario non si inventa per analogia.
- Quando nessuna regola copre il caso, chiedi a <persona di riferimento> prima di decidere. Non dedurre una regola nuova dal file.
- Alla fine di un lavoro, esegui la Checklist.
- Questo documento si modifica solo tramite l'owner. Una regola nuova o una correzione si propone all'owner.
- La sezione *Dati per l'aggiornamento*, in fondo al documento, serve alla skill che aggiorna il pacchetto: non va tolta né modificata a mano.

Sotto l'elenco, un testo per l'IA, sempre presente anche quando il team non prevede di usarla:

> Se sei un'IA che lavora su questo design system, il tuo compito è uno di questi due.
>
> - **Se crei, modifichi o nomini un elemento nel file**, leggi l'intero Regolamento prima di cominciare. Quando nessuna regola copre il caso, fermati e chiedi alla persona con cui lavori. Alla fine esegui la Checklist e riporta per ID le regole che non hai potuto rispettare, con il motivo.
> - **Se rispondi a una domanda sul design system**, usa solo ciò che sta nei documenti di questa cartella. Cita l'ID di ogni regola che usi e riportane il testo. Prima di indicare un elemento del file come esempio, controlla che non compaia in `03_Violazioni.md`. Se nessuna regola copre il caso, dillo e indica <persona di riferimento>. Non dedurre una regola dal file e non presentarne una come se esistesse.

### Glossario

Due tabelle.

- **Nomi del file.** Il nome canonico di ogni elemento che i documenti citano: sezioni e pagine del file, collection, stati delle Section, componenti di supporto, marcatori nei nomi. Per ogni nome, una riga che dice cos'è. Il nome sta in codice inline, come in tutti i documenti. Il nome canonico è quello presente nel file Figma, con la stessa grafia. Quando una regola impone un nome diverso, il nome canonico è quello imposto dalla regola, e la corrispondenza con il nome di oggi sta solo nelle Violazioni, nella riga dell'elemento. Così il Glossario resta vero anche dopo la correzione. La Mappa del file segue lo stesso criterio. Un elemento che non esiste ancora (vedi le Violazioni, *Elementi da creare*) compare con il nome che avrà, e la riga dice cos'è senza dire che è disponibile.
- **Termini tecnici.** I termini del lessico di Figma e dei design system usati nei documenti, con la forma scelta secondo *Terminologia tecnica*.

### Mappa del file

Una tabella delle sezioni e delle pagine del file con tre colonne: nome, contenuto, e se la pagina è una fonte ammessa per istanze e stili (sì / no / solo per un uso preciso). Le pagine "no" sono quelle di esplorazione, di backup, le schermate dimostrative e le pagine di servizio. La documentazione di un fornitore di kit si indica come tale.

### Checklist

Due elenchi, ognuno con gli ID delle regole verificate: *Prima di consegnare una schermata* e *Prima di pubblicare una modifica alla library*. Ogni voce è una domanda chiusa. Esempio: "Ogni schermata ha un nome nel formato `CODE-NNN Screen Name`? (NAM-18)".

### Dati per l'aggiornamento

L'ultima sezione del Regolamento. Una linea orizzontale la separa dalla Checklist, preceduta e seguita da una riga vuota: senza la riga vuota prima, il markdown trasforma la riga di testo sopra la linea in un titolo. Sotto il titolo, una nota fissa, tradotta nella lingua del documento, e poi la tabella dei dati:

```markdown
> **Attenzione.** Questa sezione serve alla skill che aggiorna il pacchetto, e non va tolta né modificata a mano. Se un dato è cambiato, per esempio l'owner, chiedi all'owner di aggiornare il pacchetto.

| Campo | Valore |
| --- | --- |
| design_system | <nome del design system> |
| figma_file | <URL del file della library> |
| file_di_lavoro | <URL, separati da virgola, oppure "nessuno"> |
| lingua | <codice lingua> |
| distribuzione | cartella-condivisa, repository, project oppure solo-owner |
| owner | <nome e cognome dell'owner> |
| persona_che_approva | <nome e cognome, oppure ruolo, se diverso dall'owner; altrimenti "owner"> |
| piattaforma_primaria | ios, android oppure web |
| tema_di_consegna | chiaro, scuro oppure entrambi |
| kit | segue-aggiornamenti, solo-team oppure nessun-kit |
| materiale_del_team | <tipi di materiale che descrivono come lavora il team, separati da virgola, oppure "nessuno"> |
| id_ritirati | <ID separati da virgola, oppure "nessuno"> |
```

I nomi dei campi restano in questa forma in ogni lingua, perché la skill li cerca per nome. Un salvataggio in Google Docs può scriverli con una barra rovesciata prima del trattino basso, per esempio `design\_system`: la skill li legge ignorando quella barra.

## `01_Onboarding.md`

```markdown
# Guida di onboarding — <nome del design system>

> **I codici fra parentesi, come (NAM-18), rimandano al Regolamento.** Ogni codice è l'ID di una regola in `02_Regole.md`. Qui la regola è riassunta in una frase, nel Regolamento trovi il testo completo con gli esempi. Se hai aperto questo file per primo, parti da `00_Start.md`, che spiega il pacchetto e l'ordine di lettura.

## A cosa serve questo design system
## Prima di iniziare
## Come è fatto il file
## Come si lavora
## Compiti tipici
## Correggere un componente esistente
## Errori da evitare
## Quando una regola non basta
```

La nota in apertura è un testo fisso: va riportata integralmente, tradotta nella lingua del documento.

Contenuto delle sezioni:

- **A cosa serve questo design system.** Il prodotto, le piattaforme, chi è l'owner. Se la library deriva da un kit di un fornitore, dillo qui, e di' quali pagine sono documentazione del fornitore. Pochi paragrafi.
- **Prima di iniziare.** Le library da abilitare, i file da conoscere, dove si trovano i documenti del pacchetto, a chi chiedere l'accesso.
- **Come è fatto il file.** La Mappa del file raccontata: cosa si trova in ogni sezione, quali pagine si usano tutti i giorni. Le pagine che non vanno mai usate come fonte di componenti e stili si nominano in una nota Attenzione alla fine della sezione, con il motivo e l'ID della regola. Esempio: "> **Attenzione.** Non prendere componenti da `✦ Applications Screens`, da `Playground` o da `Cover`: le istanze lì sono configurate per un esempio, o sono prove. I componenti si prendono solo dal pannello Assets (FON-01)."
- **Come si lavora.** Il percorso di un lavoro dal brief alla consegna: dove si esplora, come si organizza una pagina di flusso, quali stati attraversa una Section, come si consegna. Ogni passaggio cita gli ID delle regole che lo governano. Se i file di lavoro non esistono ancora, questa sezione spiega anche come crearli.
- **Compiti tipici.** Da tre a sei procedure passo per passo, scelte fra quelle che il nuovo designer farà davvero: creare una schermata, configurare un componente, proporre una modifica a un componente, creare un componente nuovo, proporre un token nuovo, esplorare. Ogni passo cita l'ID della regola che applica.
- **Correggere un componente esistente.** La procedura per portare a regola un componente elencato nelle Violazioni: trovare la forma corretta nelle Violazioni, leggere la Precauzione della riga e fare il controllo che indica, chiedere l'ok alla persona che approva le modifiche, pubblicare con la descrizione della modifica, segnalare la correzione all'owner, che toglie la riga dalle Violazioni. Il significato di `nessuna` sta nel passo della procedura. I controlli richiesti da `controlla le istanze` e `avvisa lo sviluppo` stanno in una nota Attenzione subito dopo quel passo: "> **Attenzione.** Con Precauzione `controlla le istanze`, le istanze esistenti possono perdere gli override o cambiare aspetto: guarda dove l'elemento è usato prima di correggerlo. Con `avvisa lo sviluppo`, lo sviluppo usa già il nome o il code syntax: avvisalo prima di cambiarlo."
- **Errori da evitare.** Gli errori che le regole prevengono, in una riga ciascuno, sempre nella stessa forma: l'errore, due punti, cosa fare al suo posto, l'ID fra parentesi. Quando l'errore riguarda un nome o un valore, la riga riporta sia la forma scorretta sia quella corretta. Esempi: "`Size=Small|Default|Large`: usa la scala abbreviata, per esempio `Size=sm|md|lg` (NAM-09)." e "Icona colorata con `text/*`: usa `fg/*` (TOK-03)." Comprende le forme scorrette da non replicare, senza dire quali elementi le usano oggi.
- **Quando una regola non basta.** A chi si chiede, come si propone una regola nuova all'owner.

La Guida non ripete il testo delle regole. Una regola si cita con una frase di riassunto e il suo ID, per esempio: "Le schermate si nominano con codice di flusso e numero a passi di dieci (NAM-18)."

## `03_Violazioni.md`

Le Violazioni sono l'elenco di ciò che nel file di oggi non segue le regole del Regolamento, e quindi richiede un intervento: errori, incoerenze fra elementi simili, elementi che le regole citano e che il file non contiene. Le legge chi corregge un componente, a mano o con l'aiuto di un'IA, e le legge chi deve sapere quali elementi non prendere come modello.

```markdown
# Violazioni del Regolamento — <nome del design system>

Data dell'analisi: <AAAA-MM-GG>.

Questo documento elenca ciò che nel file, alla data dell'analisi, non segue le regole del Regolamento: nomi e forme sbagliati, incoerenze fra elementi simili, elementi che le regole citano e che il file non contiene. Ogni riga indica la forma corretta e l'azione prevista. Gli elementi elencati non vanno presi come modello. Una riga si toglie quando l'elemento è stato corretto. Ogni sezione porta l'ID e il titolo di una regola di `02_Regole.md`.

Nelle tabelle, la colonna Azione dice se e quando l'elemento si corregge. La colonna Precauzione dice cosa controllare prima di correggerlo, perché la correzione può cambiare le schermate che usano l'elemento o il codice che lo cita.

## Riepilogo
## Copertura dell'analisi
## Elementi da creare
## Difetti del file senza regola
## <ID della regola> · <titolo della regola>
…una sezione per ogni regola che ha violazioni, nell'ordine del Regolamento…
```

- **Riepilogo.** Una tabella con una riga per sezione del documento, nello stesso ordine delle sezioni. Le colonne sono: la sezione, il numero di righe, l'azione, e quante righe hanno Precauzione `nessuna`, `controlla le istanze` e `avvisa lo sviluppo`. Le righe con Azione `tollerare` contano nel numero di righe ma in nessuna colonna di Precauzione. Una riga di gruppo conta come una riga. *Elementi da creare* compare con il solo numero di elementi. Sotto la tabella, una frase dà i totali per Precauzione. Il Riepilogo serve a decidere da dove cominciare: le righe con Precauzione `nessuna` si correggono senza altri controlli.

| Sezione | Righe | Azione | nessuna | controlla le istanze | avvisa lo sviluppo |
| --- | --- | --- | --- | --- | --- |
| NAM-04 · Nomi delle parti interne | 16 | correggere | 16 | 0 | 0 |

- **Copertura dell'analisi.** Cosa l'analisi ha controllato e cosa no, con le regole che possono avere violazioni non elencate.
- **Elementi da creare.** Componenti, stili o variabili citati dalle regole o dalle forme corrette delle Violazioni e assenti dal file, ognuno con il nome che avrà e gli ID delle regole che lo citano. Ogni elemento porta il tipo: `nuovo`, se non è mai esistito, oppure `da ricreare`, se nel file ci sono istanze di un componente principale eliminato.
- **Difetti del file senza regola.** Difetti che nessuna regola copre ma che l'analisi ha trovato: refusi nei nomi, description che contraddicono i valori, elementi duplicati. Stessa tabella delle sezioni per regola, senza ID.
- **Una sezione per regola.** Il titolo della sezione è l'ID e il titolo della regola, così il rimando fisso del Regolamento punta a una sezione precisa. Ogni sezione ha una tabella:

| Elemento | Pagina | Forma attuale | Forma corretta | Azione | Precauzione |
| --- | --- | --- | --- | --- | --- |
| `Badge` | `❖ Badge` | `State=Error\|Neutral\|…` | `Type=Brand\|Neutral\|…` | correggere | controlla le istanze |

- **Precauzione** dice cosa controllare prima di correggere. I valori sono quattro:
  - `nessuna` quando la correzione cambia solo un nome di componente, una description, l'ordine dei valori di un asse o lo scope di una variabile. Nessuna schermata e nessuna riga di codice dipendono da questi dati;
  - `controlla le istanze` quando la correzione rinomina o rimuove proprietà o valori di variante, cambia un valore, una geometria o un alias, toglie un elemento dalla pubblicazione o lo rimuove. Le istanze esistenti possono perdere gli override o cambiare aspetto, quindi prima si guarda dove l'elemento è usato;
  - `avvisa lo sviluppo` quando la correzione cambia il nome di una variabile o il suo code syntax, perché lo sviluppo può usarli già nel codice;
  - `—` quando l'Azione è `tollerare`, perché l'elemento non si corregge.
- **Azione** ha tre valori: `correggere` (l'elemento si sistema), `alla prossima modifica` (l'elemento si porta a regola quando qualcuno lo modifica per altri motivi), `tollerare` (l'elemento resta così per scelta). L'azione predefinita di ogni regola sta in `references/intervista.md`, *Ambito e azione predefiniti*.
- **Raggruppa le violazioni di massa.** Quando una regola è violata da più di 10 elementi dello stesso tipo nello stesso modo (per esempio il separatore di tutte le description), scrivi una riga sola con il gruppo e il conteggio, invece di una riga per elemento.

La riga "Data dell'analisi" è un testo fisso, tradotto nella lingua del documento, con la data nella forma AAAA-MM-GG. Sta sempre subito sotto il titolo, perché la skill la legge da lì e chi legge capisce subito quanto è aggiornato l'elenco. Le Violazioni non hanno frontmatter.

Le Violazioni si rigenerano per intero a ogni Riallinea.

## `00_Start.md`

Il file Start spiega il pacchetto a chi lo riceve. Non presuppone che il lettore usi un'IA né che il progetto abbia un `CLAUDE.md`.

```markdown
# Documentazione del design system <nome>

Questa cartella contiene le regole del design system <nome> (file Figma: <URL>). L'owner è <nome e cognome dell'owner>: le modifiche ai documenti passano dall'owner.

## Cosa contiene, in ordine di lettura

- `00_Start.md` — questo file.
- `01_Onboarding.md` — la Guida per chi entra nel progetto. Si legge subito dopo questo file.
- `02_Regole.md` — il Regolamento: le regole, ognuna con un ID. Si consulta quando si ha un dubbio e prima di consegnare.
- `03_Violazioni.md` — ciò che nel file oggi non rispetta le regole (errori, incoerenze, elementi mancanti), con la forma corretta. Si consulta prima di prendere un componente come modello e quando si corregge un componente.

## Come leggere i codici delle regole

I codici come NAM-18 che compaiono nei documenti sono gli ID delle regole di `02_Regole.md`. La sigla dice di cosa parla la regola, il numero è solo l'ordine di inserimento.

| Sigla | Di cosa parla |
| --- | --- |
| GEN | Regole generali: lingue, temi di consegna, ruoli |
| FON | Da dove si prendono componenti, stili, icone e immagini |
| NAM | Nomi di pagine, Section, schermate, layer, componenti e proprietà |
| TOK | Token, variabili e stili |
| CMP | Uso dei componenti nelle schermate |
| LIB | Creare, modificare e pubblicare elementi nella library |
| WRK | Organizzazione dei file di lavoro |
| CNT | Copy e dati delle schermate |
| ACC | Accessibilità |
| HND | Annotazioni e handoff |

## Come si aggiorna

I documenti si aggiornano solo tramite l'owner. Una copia di questi file fuori da questa cartella non si modifica a mano: si rigenera da qui.

> **Attenzione.** Non modificare questi documenti a mano e non modificarli in Google Docs: al salvataggio Google Docs cambia la forma del testo e rompe le tabelle.

## Consultare i documenti con un'IA

Un assistente IA può rispondere alle tue domande su questi documenti mentre lavori, così non devi cercare la regola a mano. Va bene qualunque strumento che risponda a partire dai file che gli dai, per esempio:

- uno strumento che risponde solo dalle fonti caricate e le cita, come NotebookLM;
- un progetto con documenti in ChatGPT, Claude o Gemini, con questi file caricati nella sua conoscenza;
- un assistente che legge direttamente questa cartella, come Claude Code, che resta allineato ai file senza bisogno di ricaricarli.

In ogni caso dagli tutti e quattro i file, e chiedigli di seguire la sezione "Come si usa questo documento" del Regolamento.

Alcune domande che puoi fare:

- "<domanda su un nome, per esempio: Come si nomina la schermata di errore del login?>"
- "<domanda su una pratica di lavoro, per esempio: Posso staccare un'istanza per cambiare un testo?>"
- "<domanda su un elemento delle Violazioni, per esempio: Posso prendere Badge come modello per un componente nuovo?>"
- "<domanda su un token, per esempio: Che token uso per lo sfondo di una card?>"

L'IA risponde citando l'ID della regola che applica. Se una risposta non cita nessun ID, controlla nel Regolamento prima di seguirla. Quando i documenti cambiano, ricarica i file nuovi nello strumento, a meno che lo strumento legga direttamente la cartella.

## Lavorare in Figma con un'IA

Se usi un assistente IA che modifica i file Figma di questo progetto, per esempio Claude Code con il connettore Figma, dagli `02_Regole.md` e `03_Violazioni.md` prima di chiedergli qualunque modifica. Chiedigli anche di leggere per intero la sezione "Come si usa questo documento" del Regolamento. Con Claude Code puoi aggiungere al `CLAUDE.md` del tuo progetto la riga: "Prima di lavorare in Figma su <nome>, leggi `<percorso della cartella>/02_Regole.md` e `03_Violazioni.md`."
```

Le domande d'esempio si scrivono per il design system specifico, con nomi reali presi dal file. Una delle domande chiede se un elemento esistente si può prendere come modello, e quell'elemento è scelto fra quelli presenti nelle Violazioni: così il designer scopre che l'IA controlla anche quel documento. Con distribuzione `project` la prima frase della sezione dice che il team ha già un progetto con questi documenti, e indica a chi chiedere l'accesso.

La tabella della legenda contiene solo le sigle dei domini presenti nel Regolamento, nello stesso ordine. Le descrizioni sono un testo fisso, tradotto nella lingua del documento.

`<percorso della cartella>` dipende dalla distribuzione. Con `repository` è il percorso della cartella dentro il repository. Con `cartella-condivisa` il percorso cambia da un computer all'altro: il testo non scrive un percorso, e dice invece "il percorso in cui questa cartella è sincronizzata sul tuo computer".
