# Intervista all'owner

L'intervista porta all'owner solo le decisioni che la skill non può prendere da sola. Le decisioni che la skill prende da sola arrivano all'owner tutte insieme, nell'Elenco di revisione a fine intervista. Il criterio che separa i due gruppi sta in `SKILL.md`, *Chi decide cosa*.

L'intervista si conduce con `AskUserQuestion`. Il campo libero del pannello resta sempre disponibile per le regole che l'owner vuole aggiungere.

## Limiti del pannello

`AskUserQuestion` ammette al massimo quattro domande per pannello e quattro opzioni per domanda, più il campo libero. L'header di ogni domanda ha al massimo 12 caratteri. Quando un blocco ha più di quattro domande, usa più pannelli. Quando una domanda avrebbe più di quattro opzioni, tieni come opzioni le tre forme più frequenti e raccogli le altre in una quarta opzione, "Un'altra forma", che rimanda al campo libero.

## Regole di conduzione

- **Prima i dati, poi la domanda.** Ogni domanda su una convenzione riporta il conteggio dell'inventario. Esempio: "Lo stato di selezione è espresso con `Selected=False|True` in 1 componente, con `Active` in 6 e con `State=Active` in 7. Quale forma è la regola per i componenti nuovi?"
- **Domande di fatto e domande di decisione.** Una domanda di fatto chiede come stanno le cose o come lavora oggi il team, per esempio se i file di lavoro esistono o chi approva le modifiche. Una domanda di decisione chiede quale regola adottare fra più forme possibili.
- **Le domande di decisione hanno una raccomandazione.** La prima opzione è quella che raccomandi, marcata "(Recommended)", e la sua descrizione dice il motivo in una frase. La raccomandazione segue gli standard attuali del settore e le convenzioni della piattaforma primaria, e si appoggia alla convenzione dominante del file quando questa è già corretta.
- **Le domande di fatto non hanno una raccomandazione.** Le opzioni si presentano senza preferenza. Quando l'analisi ha già una risposta probabile, quella risposta è la prima opzione e la sua descrizione dice "dedotto dal file" con l'indizio. Se la risposta dell'owner è che il team non ha ancora una pratica, segue una domanda di decisione con la raccomandazione.
- **Nelle domande a scelta multipla ogni voce dichiara se è raccomandata.** Ogni voce raccomandata porta "(Recommended)", non solo la prima. Una voce senza il segno dice nella descrizione perché non è raccomandata.
- **Ogni opzione dice il suo impatto sul file, con una di tre formule.** Le formule sono: "Finiscono fuori regola N <elementi>: <i primi nomi>."; "Nessun elemento fuori regola."; "Impatto non misurato: <motivo>." L'ultima formula vale, per esempio, quando la regola riguarda file di lavoro che non esistono ancora.
- **La raccomandazione dichiara il suo costo.** Se un'altra opzione valida mette fuori regola meno elementi, il motivo della raccomandata dice perché il costo maggiore vale. Esempio: "`Tone` (Recommended) — `Type` porta già due significati. Finiscono fuori regola 7 componenti, contro i 5 dell'opzione `Type`."
- **Una decisione per domanda.** Una domanda che chiede due decisioni produce una risposta ambigua.
- **La delega si risolve con la raccomandazione.** Quando l'owner risponde "scegli tu" o "suggerisci tu", spiega la raccomandazione con il motivo, poi chiedi conferma nel pannello successivo, con tutte le raccomandazioni delegate fino a quel momento.
- **Le parole vaghe si chiudono subito.** Se l'owner risponde con "di solito", "preferibilmente", "se possibile", chiedi nel pannello successivo il criterio che decide il caso: quando si fa altrimenti, e chi lo decide.
- **Una scelta contro la raccomandazione si conferma una volta.** Quando l'owner sceglie un'opzione non raccomandata, scrivi nel pannello successivo il rischio concreto in una frase e chiedi conferma prima di registrare la regola.
- **Le contraddizioni si risolvono subito.** Se una risposta contraddice una risposta precedente o una regola già raccolta, mostra le due affiancate nel pannello successivo e chiedi quale prevale.
- **Un'opzione non selezionata non è un'esclusione.** In una domanda a scelta multipla, una voce lasciata fuori può essere un'esclusione voluta o una dimenticanza. Una voce non selezionata che appartiene a un'area fondamentale torna nell'Elenco di revisione con una regola di default, oppure, se l'area non ha un default, con la domanda a tre opzioni di *Copertura*. Una voce non selezionata fuori dalle aree fondamentali torna nell'Elenco di revisione, nel gruppo *Decisioni rimaste aperte*, quando lascia elementi del file senza una regola e senza un'azione. La raccomandazione dice cosa succede a quegli elementi.
- **Ciò che l'owner cita deve esistere.** Se una regola dell'owner cita un componente, uno stile, una variabile o una pagina, verifica che esista nel file. Se non esiste, dillo subito: l'elemento entra nelle Violazioni come elemento da creare, e la regola lo cita con il nome che avrà.
- **Le regole dell'owner si rileggono.** Dopo aver formalizzato una regola libera, mostrala all'owner nel formato definitivo, senza ID, prima di registrarla. L'ID si assegna alla stesura. Se la regola non è decidibile perché manca un valore, per esempio gli stati di un componente da creare, chiedi quel valore nello stesso pannello della rilettura, con una raccomandazione.
- **Si chiede solo ciò che manca.** Ciò che la skill può decidere secondo *Chi decide cosa* non diventa una domanda: va nell'Elenco di revisione. Se la documentazione del team contiene già una regola, la regola va nell'Elenco di revisione con `Fonte: documentazione del file`. La documentazione del fornitore di un kit vale come risposta solo se l'owner, nel Blocco 1, ha detto che il team la adotta.
- **Le tue interpretazioni si dichiarano.** Quando una regola nasce da una tua lettura della risposta dell'owner e non dalle sue parole, segnalalo nel report di consegna.

## Formati e separatori

Questa sezione vale per ogni testo con più campi: description di variabili, componenti e stili, nomi composti di pagine, schermate e Section.

**Description.** Il formato di riferimento per i token, quello del Design Tokens Community Group (DTCG), tratta la description come testo libero senza campi interni. Il percorso del token e l'alias si leggono già dal nome, dal code syntax e dal valore. Per questo il formato delle description è una regola di default: "La description contiene solo lo scopo dell'elemento." La regola va nell'Elenco di revisione con `Fonte: standard`.

Il formato delle description diventa un conflitto del Blocco 2 in due casi: il file usa con costanza un formato a più campi, oppure usa un separatore che non rispetta i tre criteri qui sotto. La domanda ha come opzione raccomandata il solo scopo. L'alternativa è il formato a più campi, con un separatore che rispetta i tre criteri.

**Separatori.** Quando servono più campi, il separatore si sceglie in quest'ordine:

1. **Dal file.** Se l'analisi trova un formato e un separatore usati con costanza, quello è il candidato.
2. **Verifica del separatore del file.** Il separatore deve rispettare tre criteri: è un carattere ASCII, digitabile da qualunque tastiera; non compare nel testo libero dei campi che separa; resta leggibile nei tooltip e nei pannelli di Figma. Se il separatore del file non rispetta un criterio, l'opzione lo dice con il rischio concreto e propone ` | `. Esempi di separatori che non rispettano i criteri: il punto centrale `·`, che non è ASCII e non si digita; il trattino ` - ` e il trattino lungo ` – `, che si confondono con i trattini del testo libero.
3. **Solo se il file non ha un formato, o l'owner scarta quello del file,** proponi ` | ` (barra verticale fra spazi). Il separatore ` | ` è una scelta che rispetta i tre criteri, non uno standard di settore: presentalo come tale.

Se l'owner sceglie un separatore che non rispetta i tre criteri, scrivi il rischio concreto nel pannello successivo e chiedi conferma prima di registrare la regola.

## Blocco 1 — Contesto

Il Blocco 1 viene subito dopo la sintesi dell'inventario e prima di ogni altra domanda. Le sue risposte servono a tutti i blocchi successivi: decidono quali convenzioni del file la skill può usare e su quale piattaforma si basano le raccomandazioni. Contiene domande di fatto, in uno o due pannelli.

- **Materiale che descrive come lavora il team.** L'analisi distingue quattro tipi di materiale: pagine introduttive, frame di documentazione nelle pagine dei componenti, description dei componenti, schermate dimostrative. Per ogni tipo presente nel file chiedi se descrive come lavora il team. Le opzioni sono tre: "Sì, l'ha scritto il team"; "Sì, è del fornitore del kit ma il team lo adotta"; "No, è materiale del fornitore che il team non segue". La classificazione dell'analisi è la prima opzione, con l'indizio che la sostiene. I tipi con la stessa classificazione si raggruppano in una sola domanda.
- **Rapporto con il kit.** Se la library deriva da un kit, chiedi se il team segue gli aggiornamenti del fornitore. Le opzioni sono: il team segue gli aggiornamenti; il file ormai è solo del team; la library non deriva da un kit.
- **Piattaforma primaria.** iOS, Android, web, oppure più piattaforme con una primaria. La classificazione dell'analisi, ricavata dai mirror e dai componenti di piattaforma, è la prima opzione.
- **Tema di consegna.** In quale tema si consegna una schermata: chiaro, scuro, entrambi.

Le risposte sul materiale e sul kit hanno queste conseguenze.

- **Materiale scritto dal team o adottato dal team.** Le regole che contiene entrano nell'Elenco di revisione con `Fonte: documentazione del file`.
- **Materiale del fornitore che il team non segue.** Non produce regole. Una convenzione che compare solo in quel materiale, per esempio solo nelle schermate dimostrative, non si propone come convenzione del team.
- **Library che segue il kit.** Ogni opzione di conflitto che si allontana dalla forma del fornitore lo dichiara nella descrizione: a ogni aggiornamento del kit la correzione va rifatta. In questo caso la raccomandazione è la forma del fornitore, salvo un difetto di accessibilità o un nome con più significati.

Le risposte del Blocco 1 si registrano nella sezione *Dati per l'aggiornamento* del Regolamento (vedi `references/formato-documenti.md`).

## Blocco 2 — Conflitti

Un conflitto per domanda, con le forme concorrenti come opzioni e i conteggi nella descrizione di ogni opzione. Che cosa è un conflitto lo definisce `references/analisi-figma.md`, *Come si deduce una convenzione*. Se una forma coincide con lo standard della piattaforma primaria, con la documentazione del team o con la forma del fornitore, dillo nella descrizione.

**Conflitti minori.** Un conflitto minore, secondo la soglia di `references/analisi-figma.md`, *Come si deduce una convenzione*, non diventa una domanda. Va nell'Elenco di revisione, nel gruppo *Conflitti minori*.

Sono conflitti anche i nomi con più significati trovati dall'analisi (vedi `references/analisi-figma.md`, *Nomi con più significati*). Per questi la domanda chiede quale significato tiene il nome. **Ogni opzione dice anche quale nome prendono gli altri significati**, così che la scelta non lasci decisioni aperte. Esempio: "`Type` resta al colore semantico; la forma passa a `Shape`, l'enfasi a `Style`." Prima di proporre un nome nuovo, verifica che non sia già il nome di una pagina, di una collection o di un gruppo di variabili del file.

**Scelte ad alto costo.** Una regola che cambierebbe il nome o il code syntax di variabili che hanno già un code syntax diventa una domanda del Blocco 2, anche quando viene da una convenzione dominante: il code syntax è il segno che lo sviluppo può usare quei nomi. La domanda dice quante variabili cambierebbero, e offre come alternativa di tenere i nomi attuali. Le altre rinomine di variabili restano nell'Elenco di revisione, e le loro righe nelle Violazioni hanno comunque Precauzione `avvisa lo sviluppo`.

## Blocco 3 — Lacune

Il file Figma non contiene il modo di lavorare. Il catalogo qui sotto divide le aree di processo in due gruppi.

### Aree che dipendono dal team

Per queste aree solo il team conosce la risposta, quindi si chiede all'owner. Sono domande di fatto: chiedono come lavora oggi il team. Se il team non ha ancora una pratica, segue una domanda di decisione con la raccomandazione.

| Area | Domande da porre |
| --- | --- |
| **Lingue** | In che lingua si scrivono i nomi di layer, componenti e annotazioni? In che lingua sono i copy dell'interfaccia? In che lingua si scrivono le description di componenti, variabili e stili? |
| **Ruoli** | Chi approva le modifiche alla library? A chi si rivolge un designer quando una regola non copre il suo caso? Le persone si indicano con nome e cognome, oppure con il ruolo (vedi `SKILL.md`, Passo 1). |
| **Handoff** | Con quale strumento si annota? Come si segnala che una Section è pronta per lo sviluppo? Le transizioni si indicano con preset di motion o con durate libere? |
| **Componenti di forma nativa** | I componenti disegnati dall'app ma di forma nativa (tab bar, toggle, text field) prendono il brand, oppure l'app usa i controlli del sistema? |
| **File di lavoro esistenti** | Solo se i file di lavoro esistono e l'analisi li ha letti: le convenzioni trovate su pagine dei flussi, nomi delle schermate, stati delle Section ed esplorazione vanno nell'Elenco di revisione; si chiedono solo i conflitti. |

Nei testi che seguono, **la persona che approva** è la persona indicata nella risposta sui ruoli. Se l'owner non indica nessun altro, la persona che approva è l'owner.

### Aree coperte da regole di default

Per queste aree la pratica corrente del settore offre una regola senza alternative realistiche. La skill scrive la regola di default e la mette nell'Elenco di revisione con `Fonte: standard`. Se il file o la documentazione del team ha una forma dominante diversa dal default, prevale la forma del file, con `Fonte: file` o `Fonte: documentazione del file` secondo dove la forma si trova. Fa eccezione l'accessibilità: se la forma del file viola il default, il caso diventa un conflitto del Blocco 2.

| Area | Regola di default |
| --- | --- |
| **Fonti ammesse** | Istanze, stili, icone e immagini si prendono solo dalle pagine della library pubblicata. Non si prendono mai da esplorazioni, mirror di piattaforma, backup, schermate dimostrative o documentazione. |
| **Componenti di sistema** | Gli elementi disegnati dal sistema operativo (status bar, tastiera, alert di sistema) si usano così come sono. |
| **Naming dei layer** | I layer si nominano per funzione, non per aspetto. I nomi di default di Figma (`Frame 12`, `Rectangle 3`) sono vietati nelle schermate consegnate e nei componenti. Un'istanza mantiene il nome del componente. |
| **Detach e override** | Il detach è vietato nelle schermate consegnate e nei componenti della library. Nascondere o sovrapporre layer per correggere un'istanza è vietato. Se un componente non basta, si chiede una variante alla persona che approva. |
| **Valori fissi** | Colori, raggi, spaziature, testi ed effetti si legano a variabili o stili. Fanno eccezione illustrazioni, foto e grafica di brand. |
| **Token** | Nelle schermate si usano solo i token semantici. Una trasparenza si ottiene con un token dedicato, non con l'opacità sulla paint. Un token semantico nuovo ha nome secondo la convenzione del file, alias a un primitivo, scope specifici, description con il solo scopo e code syntax. Un token di colore nuovo ha il contrasto verificato contro i token di sfondo con cui è previsto l'uso. |
| **Effetti** | Gli effetti con vincoli d'uso dichiarati dal file o dalla piattaforma si applicano solo dove il vincolo lo permette, per esempio il blur solo sullo sfondo. |
| **Proprietà dei componenti** | Una proprietà che mostra o nasconde un layer è una proprietà booleana. Una proprietà che cambia aspetto o struttura del componente è un asse di variante. I valori di un asse di conteggio, cioè un asse che indica un numero di elementi (es. `Tabs=2\|3\|4\|5`), stanno in ordine crescente. |
| **Creazione di componenti** | Un componente nuovo ha auto layout, valori legati a token, tutti gli stati di interazione, touch target minimo, focus visibile e description. |
| **Modifica di componenti** | Prima di rinominare o rimuovere una proprietà si verificano le istanze. Ogni pubblicazione ha una descrizione della modifica. La persona che approva approva le modifiche prima della pubblicazione. |
| **Deprecazione** | Un elemento da rimuovere si marca nel nome e nella description per almeno una pubblicazione prima della rimozione. Se il file ha già un marcatore, si usa quello. |
| **Accessibilità** | Vale WCAG 2.2 AA. Il contrasto è almeno 4.5:1 per il testo normale e 3:1 per il testo grande (da 18 pt, o da 14 pt in grassetto). Confini dei componenti e grafica informativa hanno contrasto almeno 3:1; i componenti disabilitati sono esclusi. Il touch target minimo è 44 × 44 pt su iOS, 48 × 48 dp su Android, 24 × 24 px CSS sul web. Il focus è sempre visibile. Il significato non è mai affidato al solo colore. |
| **Contenuti** | Copy e dati sono realistici e coerenti fra le schermate. |

Per i criteri numerici di accessibilità cita la fonte giusta. I 44 pt e i 48 dp vengono dalle linee guida di Apple e di Material. I 24 × 24 px CSS vengono dal criterio WCAG 2.5.8 (livello AA). Il criterio 2.5.5 (livello AAA) chiede 44 × 44 px CSS: se l'owner vuole un minimo più alto sul web, cita quel criterio.

### File di lavoro assenti

Se i file di lavoro non esistono ancora, la loro organizzazione non si chiede a vuoto. La skill la copre con un pacchetto di default, costruito sulle convenzioni della library e sulle risposte sull'handoff, che va nell'Elenco di revisione con `Fonte: standard`. Il pacchetto di partenza:

- pagine di flusso con il prefisso di pagina-schermate della library e un codice di flusso, per esempio `◼︎ AUTH | Authentication`;
- schermate con codice di flusso e numero a passi di dieci, stato e piattaforma opzionali, per esempio `AUTH-020 Sign In | Error`;
- Section con stati di avanzamento espliciti. Lo stato finale è quello indicato nella risposta sull'handoff; se la risposta non ne indica uno, è lo stato nativo di Figma "Ready for dev". Gli stati intermedi si segnano con lo strumento di annotazione indicato nella risposta sull'handoff;
- esplorazioni in Section datate e firmate, mai in pagine personali;
- componenti locali con un prefisso che nessun nome della library usa, per esempio `Local / `, da promuovere nella library quando servono in più di un flusso;
- annotazioni con lo strumento indicato nella risposta sull'handoff, su comportamenti e stati.

Prima di mostrare il pacchetto, verifica che ogni formato di nome rispetti i criteri di *Formati e separatori*. Ogni elemento del pacchetto che cita un componente inesistente, per esempio un componente per gli stati delle Section, va negli elementi da creare.

## Blocco 4 — Elenco di revisione

L'Elenco di revisione mostra all'owner, in un unico testo, tutte le regole che la skill ha deciso da sola. Sostituisce la conferma voce per voce: l'owner legge l'elenco e toglie o corregge ciò che non vuole.

### Copertura

Prima di comporre l'elenco, confronta le regole raccolte con le aree fondamentali qui sotto. Un'area scoperta, o coperta solo in parte, che ha una regola di default nel Blocco 3 riceve quella regola, che entra nell'elenco. Un'area scoperta senza regola di default, per esempio perché l'owner non ha risposto alla domanda sulle lingue, riceve una domanda con tre opzioni:

1. la regola che raccomandi, allineata agli standard attuali, con il motivo (Recommended);
2. una regola alternativa, se esiste un'alternativa realistica;
3. "Nessuna regola, per scelta", che registra l'esclusione nel report di consegna.

| Area fondamentale | Cosa deve dire il Regolamento |
| --- | --- |
| Lingua dei nomi e dei copy | In che lingua si scrivono nomi tecnici, description e testi dell'interfaccia. |
| Fonti ammesse | Da dove si prendono istanze, stili e asset, e da dove mai. |
| Naming di pagine, componenti, parti interne | Il formato di ogni tipo di nome. |
| Naming dei layer | Nomi per funzione, divieto dei nomi di default, nome delle istanze. |
| Assi e proprietà dei componenti | Nomi, significato e ordine dei valori degli assi principali; nomi delle proprietà booleane, di testo, di swap e di slot. |
| Uso delle variabili | Quali collection si applicano, divieto dei primitivi dove serve, trasparenza da token. |
| Creazione di un token | Nome, alias, scope, description, code syntax. |
| Testo ed effetti | Solo stili; vincoli di applicazione degli effetti. |
| Creazione e modifica di componenti | Requisiti minimi, verifica delle istanze, pubblicazione. |
| Deprecazione | Come si segnala un elemento che sta per sparire. |
| Organizzazione dei file di lavoro | Anche quando i file non esistono ancora. |
| Accessibilità | Contrasto, touch target, focus visibile, significato mai affidato al solo colore. |
| Handoff | Cosa si annota, con cosa, e come si segnala che una Section è pronta. |
| Ruoli | Chi approva e a chi si chiede. |

### Contenuto dell'elenco

L'elenco è numerato e diviso in gruppi, in quest'ordine:

1. **Regole dal file.** Le convenzioni dominanti, una riga per regola con il testo breve, il conteggio e l'impatto.
2. **Conflitti minori.** Una riga per conflitto: le forme con i loro conteggi, la forma raccomandata con il motivo, e l'alternativa. La riga porta `Fonte: file` se la forma raccomandata è già usata nel file, `Fonte: standard` se non lo è. Se l'owner sceglie l'alternativa, la regola prende `Fonte: owner`.
3. **Regole dalla documentazione del team.**
4. **Regole di default.** Le regole del Blocco 3 e quelle che coprono le aree fondamentali scoperte, ognuna con lo standard o la pratica da cui viene.
5. **Pacchetto per i file di lavoro**, se i file di lavoro non esistono.
6. **Elementi da creare**, con il nome che avranno e la regola che li cita.
7. **Decisioni rimaste aperte.** Ogni punto che la stesura richiederebbe di decidere, per esempio la forma corretta di un elemento che nessuna risposta ha fissato. Ogni punto porta la sua raccomandazione, che vale se l'owner non la cambia. I punti che emergono solo durante la stesura passano dalla *Verifica di stesura* di `SKILL.md`.
8. **Conteggi aggiornati.** I conteggi che sono cambiati rispetto a quelli mostrati nelle domande. Se un cambio inverte il confronto fra le opzioni di una domanda già risposta, quella domanda si ripresenta in un pannello.
9. **Ambito e azione sugli elementi esistenti.** Per ogni regola che il file oggi non rispetta, l'ambito e l'azione predefinita (vedi sotto).

Ogni riga riporta la fonte con lo stesso valore del campo Fonte di `references/formato-documenti.md`.

### Ambito e azione predefiniti

- **Regola dal file, dalla documentazione del team o da un conflitto risolto.** Vale anche per gli elementi esistenti. Gli elementi che la violano vanno nelle Violazioni con Azione `correggere`.
- **Regola nuova da uno standard, da un default o da una regola libera dell'owner.** Vale per gli elementi nuovi o modificati. Gli elementi esistenti che la violano vanno nelle Violazioni con Azione `alla prossima modifica`.
- **Library che segue il kit.** Le forme del fornitore che una regola mette fuori regola vanno nelle Violazioni con Azione `tollerare`.

L'owner può cambiare ambito o azione di qualunque regola nell'elenco. L'azione scelta si registra nel campo Ambito della regola (vedi `references/formato-documenti.md`), così sopravvive quando le Violazioni si rigenerano.

### Come si presenta

L'elenco ha due livelli, con una numerazione unica. Dentro ogni livello le voci seguono l'ordine dei gruppi di *Contenuto dell'elenco*.

- **Voci da guardare.** Si mostrano per intero, con il testo della regola, il conteggio, l'impatto e la fonte. Sono le voci che mettono fuori regola almeno un elemento del file e le regole che la skill ha riformulato o interpretato. Entrano qui anche, per intero, i gruppi *Conflitti minori*, *Decisioni rimaste aperte*, *Conteggi aggiornati* e *Ambito e azione sugli elementi esistenti*.
- **Voci da approvare in blocco.** Sono le regole che non mettono fuori regola nessun elemento e che riportano senza modifiche una convenzione del file, un testo della documentazione del team o una regola di default. Si mostrano in forma compatta, una riga di al massimo 15 parole per voce.

Una voce compatta si approva insieme alle altre, ma resta correggibile per numero come ogni voce. Se l'owner chiede il testo completo di una voce compatta, mostralo prima di procedere.

Mostra l'elenco come testo numerato, prima le voci da guardare e poi le voci da approvare in blocco. Poi un pannello con una domanda di fatto, senza raccomandazione: "Approvi l'Elenco di revisione?", con le opzioni "Approvo tutto" e "Tolgo o correggo alcune voci". Il campo libero raccoglie i numeri delle voci e le correzioni. Una voce corretta dall'owner prende `Fonte: owner`.

Una voce tolta che lascia scoperta un'area fondamentale riceve la domanda a tre opzioni di *Copertura*.

L'intervista si chiude quando l'owner ha approvato l'elenco. Una regola che l'owner non ha visto nell'elenco, e che non viene da una sua risposta, non entra nel Regolamento.
