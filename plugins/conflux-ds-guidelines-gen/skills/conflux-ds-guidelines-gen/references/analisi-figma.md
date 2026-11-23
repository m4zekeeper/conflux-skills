# Analisi del file Figma

Questa procedura legge il design system e produce l'inventario delle convenzioni. L'analisi è in sola lettura: gli script non creano, non rinominano e non spostano nulla.

## Strumenti

- `create_session` con la file key, prima di qualunque altra chiamata al file.
- `get_metadata` senza `nodeId`: elenco delle pagine con il loro id e il loro ordine.
- `use_figma` per leggere variabili, stili, testi e proprietà dei componenti tramite la Plugin API. Prima di usarlo carica la skill `figma:figma-use`, che ne descrive le regole. Ogni script deve solo leggere e restituire dati.
- `get_screenshot` solo quando serve capire una pagina di documentazione fatta di immagini.

La file key si estrae dall'URL: `figma.com/design/<fileKey>/...`. Se l'URL contiene `/branch/<branchKey>/`, la chiave da usare è `branchKey`.

### Come leggere molte pagine

`figma.loadAllPagesAsync()` non è supportato da `use_figma`. Per leggere il contenuto di una pagina senza cambiare la pagina corrente, usa `await page.loadAsync()` sulla pagina ottenuta con `figma.getNodeByIdAsync(id)`. Così uno script legge circa dieci pagine per chiamata, e i lotti si lanciano in parallelo nello stesso messaggio.

Indicizza sempre i risultati per **id di pagina**, non per nome. Lo stesso nome di pagina può comparire in più sezioni: per esempio "❖ Button" fra i componenti del design system, fra i mirror iOS e fra i mirror Material.

Queste due regole valgono per ogni lettura del file: l'analisi iniziale, le verifiche durante l'intervista e i conteggi della stesura.

## Cosa leggere, in quest'ordine

### 1. Struttura delle pagine

Da `get_metadata` ricava i prefissi delle pagine (es. `✦`, `❖`, `◼︎`, `–––`), il loro significato deducibile dalla posizione, l'ordine delle pagine dentro ogni sezione (alfabetico o no), e le pagine con un ruolo speciale: esplorazione, changelog, cover, crediti, kit di annotazione.

Identifica i gruppi di componenti che non vanno usati nelle schermate, per esempio i mirror di piattaforma (iOS, Material). Il nome della pagina-sezione nel file è il nome canonico: se il file dice "✦ Apple Platform", il Regolamento usa "✦ Apple Platform" e non "iOS".

Dai mirror e dai componenti di piattaforma ricava la piattaforma probabile, e dagli stili o dalle mode delle collection il tema probabile. Il Blocco 1 dell'intervista li fa confermare all'owner.

### 2. Documentazione già presente nel file, e la sua origine

La documentazione di un file sta in quattro posti: le pagine introduttive (es. "Introduction", "Getting Started", "Changelog"), i frame di documentazione dentro le pagine dei componenti, le description dei componenti, e le schermate dimostrative. Leggi i nodi di testo dei primi due con `use_figma`. Le description si leggono con il loro testo al passo 5. Delle schermate dimostrative leggi i nodi di testo di un campione di almeno cinque schermate, scelte in flussi diversi.

Per ogni blocco stabilisci **chi l'ha scritto**, in tre classi:

- **team**: il testo parla del prodotto e del brand del team;
- **fornitore**: il testo viene da un kit commerciale, open source o community. Gli indizi sono nomi di prodotto diversi dal brand, link a negozi o al sito del kit, crediti di un altro team, licenze, istruzioni d'uso generiche. Un esempio tipico è un kit che consiglia di duplicare il file e cancellare le pagine non usate, mentre il team lavora con una library pubblicata;
- **misto**: testo del fornitore adattato dal team, per esempio con il nome del brand sostituito ma valori e istruzioni del kit.

Le schermate dimostrative si classificano allo stesso modo.

La classificazione dell'analisi non decide da sola. Diventa la prima opzione della domanda del Blocco 1 (`references/intervista.md`), che chiede per ogni tipo di materiale se descrive come lavora il team. La classe "misto" non ha una conseguenza propria: decide la risposta dell'owner.

Il materiale che l'owner dichiara scritto o adottato dal team produce regole con `Fonte: documentazione del file`, che entrano nell'Elenco di revisione, perché la documentazione dentro un file può essere vecchia. Il materiale del fornitore che il team non segue non produce regole, e la Mappa del file lo indica come pagina di servizio. Una convenzione che compare solo in quel materiale non si propone come convenzione del team.

### 3. Variabili

Per ogni collection leggi: nome, mode, numero di variabili, gruppi (il prefisso prima di `/`). Per ogni variabile leggi: nome, tipo, se il valore è un alias o un valore diretto in ogni mode, scope, description, code syntax, `hiddenFromPublishing`.

Script di partenza da adattare:

```js
const cols = await figma.variables.getLocalVariableCollectionsAsync();
const out = [];
for (const c of cols) {
  const vars = [];
  for (const id of c.variableIds) {
    const v = await figma.variables.getVariableByIdAsync(id);
    vars.push({
      n: v.name, t: v.resolvedType,
      alias: Object.values(v.valuesByMode).map(x => x?.type === 'VARIABLE_ALIAS'),
      sc: v.scopes, d: v.description, cs: v.codeSyntax, h: v.hiddenFromPublishing
    });
  }
  out.push({ col: c.name, modes: c.modes.map(m => m.name), vars });
}
return out;
```

Da questi dati ricava: quali collection sono primitive e quali semantiche, la convenzione di nome (maiuscole, separatori, struttura gruppo/ruolo-step), la quota di semantici che sono alias e i gruppi dove si concentrano i valori diretti, l'uso di `ALL_SCOPES`, la presenza e il formato delle description e del code syntax, i marcatori nei nomi (es. `⚠️`).

Se una collection supera 300 variabili, restituisci statistiche per gruppo e un campione, per non saturare la risposta.

### 4. Stili

Leggi gli stili di testo, di effetto, di colore e di griglia locali: nomi, raggruppamento, font e pesi per gli stili di testo, e se le proprietà sono legate a variabili. Ricava la convenzione di nome (es. `{size}/{weight}`) e la scala.

Se gli stili sono più di 300, restituisci statistiche per gruppo e un campione, e dichiara il campione nell'inventario.

### 5. Componenti

Per ogni pagina sotto la sezione componenti, e per la pagina del kit di annotazione, leggi i component set e i componenti singoli che non stanno dentro un set. Per ognuno: nome, presenza e testo della description, definizioni delle proprietà (tipo, nome, valori di variante nel loro ordine), nomi dei sotto-componenti interni. Leggi anche i nomi dei frame di primo livello di ogni pagina, e i testi dei frame che fanno da documentazione. Quando il primo livello è fatto di Section senza nome, scendi di un livello.

Conta anche, per ogni componente, le istanze annidate che non vengono dalla library. Un'istanza il cui componente principale ha `remote` uguale a `true` viene da un'altra library, per esempio un'icona presa da un set esterno: è una deviazione della regola sulle fonti ammesse. Un'istanza il cui componente principale non esiste più nel file è un componente da ricreare, e va fra gli elementi da creare.

Se una pagina contiene più di 300 componenti, restituisci statistiche per gruppo e un campione, e dichiara il campione nell'inventario.

Script di partenza da adattare, un lotto di circa dieci pagine per chiamata:

```js
const ids = [/* id delle pagine del lotto */];
const res = [];
for (const id of ids) {
  const page = await figma.getNodeByIdAsync(id);
  await page.loadAsync();
  const nodes = page.findAllWithCriteria({ types: ['COMPONENT_SET', 'COMPONENT'] })
    .filter(n => n.type === 'COMPONENT_SET' || n.parent?.type !== 'COMPONENT_SET');
  res.push({ id, page: page.name, top: page.children.map(c => c.name), comps: nodes.map(n => ({
    name: n.name, desc: (n.description || '').slice(0, 200),
    props: Object.entries(n.componentPropertyDefinitions || {}).map(([k, d]) => ({
      k: k.split('#')[0], t: d.type, v: d.variantOptions
    }))
  })) });
}
return res;
```

Da questi dati ricava: il formato dei nomi di componente, famiglia e parte interna; i nomi degli assi di variante e la frequenza di ognuno; l'ordine dei valori dentro un asse; il formato dei nomi delle proprietà booleane, di testo, di instance swap e di slot; la quota di componenti con description; i marcatori di stato nel nome (es. `[OLD]`, `⚠️`, `[M]`).

### 6. Nomi con più significati

Contare quante volte compare un nome non basta. Per ogni asse di variante frequente (tipicamente `Type`, `Style`, `State`, `Size`, `Variant`), raggruppa i valori per significato:

- colore semantico (Brand, Neutral, Info, Success, Warning, Error);
- enfasi (Filled, Outline, Weak, Link);
- forma o struttura (Pill, Circle, Horizontal, Vertical);
- tipo di contenuto (Avatar, Emoji, Password, Prefix);
- interazione (Default, Pressed, Focused, Disabled);
- selezione (Active, Selected);
- stato di un controllo (Checked, Unchecked, Indeterminate), distinto dalla selezione;
- stato di un campo (Empty, Filled, Error, Read-only);
- limite di un valore (Min, Max);
- apertura (Open, Close);
- fase di processo (Uploading, Typing, Generating);
- progressione (Step 1, Step 2, Completed);
- tema (Light, Dark);
- breakpoint o adattamento (Mobile, Tablet, Desktop, Fill, Hug);
- scala (xs…xl, Small, Default, Compact), con l'altezza come caso particolare.

Un valore che non rientra in nessuna categoria si registra come categoria nuova nell'inventario, con il nome che descrive il suo significato.

Un asse che porta significati diversi in componenti diversi è un conflitto, anche quando il nome è lo stesso ovunque. Riportalo all'intervista con l'elenco dei componenti per ogni significato.

Fai lo stesso controllo al contrario: un significato espresso con nomi diversi (selezione come `Active`, `Selected`, `State=Active`) è un conflitto quando nessun nome raggiunge i due terzi dei componenti con quel significato. Se un nome li raggiunge, è la convenzione dominante e gli altri nomi sono deviazioni. Un significato può comparire sia in un asse con più significati sia in questo controllo. In quel caso l'inventario lo registra una volta sola, con tutti i nomi che lo esprimono, e l'intervista lo decide in una sola domanda (`references/intervista.md`, *Significati condivisi fra più domande*).

Registra anche i nomi già occupati da pagine, collection e gruppi di variabili. L'intervista li usa per non proporre un nome nuovo che esiste già con un altro significato.

### 7. Valori non legati (solo se una regola lo richiede)

Questo passo si esegue dopo l'intervista, e solo se il Regolamento ha una regola sui valori fissi che vale anche per gli elementi esistenti. In quel caso conta nei componenti i fill, gli stroke, i raggi e le spaziature che non hanno `boundVariables`. Su un file con più di 300 componenti lavora su un campione di component set e dichiara il campione nelle Violazioni, alla voce Copertura dell'analisi. Se la regola vale solo per gli elementi nuovi o modificati, il passo si salta, e la Copertura dell'analisi lo dichiara.

### 8. File di lavoro (solo se esistono e l'owner li ha indicati)

Leggi nomi delle pagine, nomi delle Section e nomi dei frame di primo livello. Da qui si ricavano le convenzioni di naming dei flussi e delle schermate e gli stati delle Section. Se i file di lavoro non esistono, questo passo si salta e le regole relative arrivano nell'Elenco di revisione come pacchetto di default.

## Come si deduce una convenzione

Una convenzione è **dominante** quando la seguono almeno due terzi degli elementi dello stesso tipo e con lo stesso significato. Riporta sempre il conteggio, per esempio "asse `Size` con scala `xs…xl` in 8 componenti; scala a parole in 7". Il conteggio permette all'owner di decidere con i dati davanti, e serve di nuovo alla consegna per dire quanti elementi una scelta mette fuori regola.

Una convenzione dominante va nell'Elenco di revisione, e non diventa una domanda. C'è invece un **conflitto**, che diventa una domanda del Blocco 2 salvo i conflitti minori descritti più sotto, nei casi seguenti:

- nessuna forma raggiunge i due terzi;
- la forma dominante porta significati diversi in componenti diversi (vedi *Nomi con più significati*);
- la forma dominante contraddice uno standard della piattaforma o di accessibilità;
- il file usa con costanza un formato di description a più campi, oppure un separatore che non rispetta i criteri di `references/intervista.md`, *Formati e separatori*;
- la correzione delle deviazioni cambierebbe il nome o il code syntax di variabili che hanno già un code syntax.

Un conflitto è **minore** quando le forme in conflitto, tutte insieme, riguardano al massimo 5 elementi e al massimo il 10% degli elementi dello stesso tipo nella library. I mirror di piattaforma non entrano nel totale. Esempio: in una library di 127 componenti, `Info` in 2 componenti e `Information` in 1 sono un conflitto minore. In una library di 20 componenti il 10% vale 2 elementi, quindi lo stesso caso non è minore.

Un conflitto minore non diventa una domanda: la skill applica la raccomandazione e lo porta nell'Elenco di revisione. Restano sempre domande del Blocco 2, anche sotto la soglia, tre casi:

- un nome con più significati;
- una forma che contraddice uno standard di accessibilità;
- una correzione che cambierebbe il nome o il code syntax di variabili che hanno già un code syntax.

Una convenzione che viene solo da materiale attribuito al fornitore segue la risposta del Blocco 1: se il team non segue quel materiale, la convenzione non si propone.

Una forma presente solo nei mirror di piattaforma non è una deviazione della library: i mirror seguono la terminologia del sistema operativo. Tienili in un conteggio separato.

## Formato dell'inventario

L'inventario è un appunto di lavoro: non va nei documenti finali. Per ogni ambito, una riga per convenzione:

```
[ambito] convenzione dominante — N su M — deviazioni: nome1, nome2, … — fonte: file | documentazione del file | documentazione del fornitore
```

Per ogni deviazione salva nella cartella di lavoro l'elenco completo degli elementi, con id, nome, pagina e forma attuale. Il conteggio dell'inventario, i conteggi mostrati nelle domande e le righe delle Violazioni si ricavano da questo elenco, così restano uguali dall'analisi alla stesura.

In coda all'inventario, elenca ciò che non è stato possibile leggere (pagine non caricate, timeout, collection troncate, controlli non eseguiti) e il motivo.
