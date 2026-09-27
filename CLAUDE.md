# LLM Wiki — Design Dev Wiki · blueprint per progetti personali di AI design

> File di configurazione del vault (pattern *LLM Wiki* di Karpathy). Dice all'agente **come è
> strutturato il lavoro e come collaboriamo** nel progettare e documentare un progetto personale di
> AI, fino al case study per il portfolio. L'utente cura design, decisioni e punti aperti; l'LLM
> struttura, scrive e mantiene i file, e valida il design contro i requisiti.
>
> **Questo è uno stampo riutilizzabile.** Per ogni nuovo progetto se ne duplica una copia (vedi
> [[README.md|README]]) e la si riempie con la sua realtà. Il blueprint resta generico: qui dentro **non
> devono mai finire dati di uno specifico progetto**.

## 0. Il pattern (LLM Wiki di Karpathy)

Il vault ha **tre livelli**:
- **raw/** — fonti immutabili: idee e appunti, paper, documentazione, repo di riferimento, risultati
  di esperimenti. L'LLM legge, non modifica.
- **wiki** — i documenti di lavoro (`requisiti`, `soluzione`, `decisioni`, `case-study`, `index`,
  `log`). L'LLM li possiede: crea, aggiorna, mantiene i cross-reference.
- **schema** — questo `CLAUDE.md`.

E **tre operazioni**:
- **ingest** — nuova fonte → entra in `raw/` (immutabile). L'LLM la legge, **discute con te i
  take-away**, poi la compila nei documenti pertinenti (una singola fonte può toccarne diversi) →
  aggiorna `index.md` → append a `log.md`.
- **query** — interrogare la wiki invece di scriverla: l'LLM risponde **dai documenti**, citando il
  paragrafo. Non si logga ogni domanda: si logga **solo quando la risposta diventa un artefatto**
  (una pagina nuova, un'analisi che resta). E una pagina nasce da una query **solo se ancorata a
  una fonte in `raw/` o a un contenuto già validato** della wiki: niente contenuti non tracciabili.
- **lint** — verifica periodica: contraddizioni, link rotti, pagine orfane, cruscotto di copertura
  disallineato dal design, decisioni ferme da troppo tempo. La procedura concreta è un runbook a
  parte, [[lint]] (vedi §8).

## 1. Principio fondante — human-in-the-loop (HITL)

> ⚠️ **Il processo principale non va mai automatizzato.** Ogni passaggio di catena — fonte →
> requisito, requisito → decisione, decisione → soluzione, soluzione → output (diagrammi,
> case study) — passa **sempre** per una **validazione umana** prima di diventare
> contenuto della wiki.

**Divisione dei ruoli.** L'utente **decide e valida**; l'agente **legge, struttura, propone,
scrive e controlla**. Una scelta che l'agente farebbe "in automatico perché ovvia" è comunque una
scelta dell'utente.

**Punto di fermata.** Prima di scrivere un contenuto di merito, l'agente si ferma e presenta
**cosa sta per scrivere e dove** — in forma compatta (la lista di `REQ` estratti, l'ossatura dei
componenti, il bivio con le opzioni), non come dump del file. Poi attende. Ogni runbook in
`procedure/` dichiara i **propri** punti di fermata nella sezione *Punti di fermata (HITL)*.

**Cosa si può fare da soli (fix sicuri) e cosa no (merito).** Il HITL totale su ogni carattere
paralizza; la linea di taglio è questa:

| | Esempi | Comportamento |
|---|---|---|
| 🔧 **Fix sicuri** — meccanici e reversibili | conteggi, ID, date, refusi nei link, riga di [[log]] | li applica **da solo**, li elenca nel report |
| 🛑 **Merito** — cambiano un'interpretazione | testo di `REQ`/`DEC`, stati del cruscotto, numeri, contenuto dei diagrammi | **propone e si ferma** |

**Regole di ingaggio.**

- **Il silenzio non è consenso**: senza una risposta esplicita, il contenuto di merito non si scrive.
- **Niente assunzioni silenziose**: se manca un'informazione, o si chiede in chat (dubbio
  transitorio) o diventa un'`ASS-x` dichiarata o una `DOM` nei punti aperti (dubbio persistente) —
  mai un valore inventato che sembra un dato.
- **Un output derivato non si auto-promuove**: diagrammi e case study
  nascono da una soluzione **già validata**; se la fonte a monte non lo è, l'agente lo dice invece
  di procedere.
- **Ciò che non è validato resta visibile come tale**: stato `proposta`, `🚧 TODO`, `DOM` aperta.

## 2. Contesto del progetto (da compilare per ogni istanza)

> Sezione da riempire all'avvio di ogni istanza. Nel blueprint resta con i segnaposto.
> Obiettivo, perimetro e non-obiettivi **non** stanno qui: la loro casa è [[requisiti]].

- **Progetto**: Setlist
- **Perché lo faccio**: capire l'AI musicale mettendoci le mani, su metal e rock strumentale — da una richiesta in linguaggio naturale a una scaletta con un arco di intensità.
- **Pubblico del case study**: ingegneri e recruiter tecnici del music tech
- **Lingua del case study**: en (anche il `README.md` del repo; il resto del vault resta in italiano)
- **Repo**: pubblico su GitHub — https://github.com/bonamattia/setlist
- **Dove gira il codice**: sul PC dell'utente (WSL), sviluppo con Claude Code in VS Code

## 3. Struttura del vault

```
design-dev-wiki/
├── CLAUDE.md              ← schema (questo file)
├── README.md             ← vetrina del repo (nell'istanza racconta il progetto)
├── index.md              ← catalogo
├── log.md                ← cronologia
├── requisiti.md          ← il COSA
├── soluzione.md          ← il COME
├── decisioni.md          ← il PERCHÉ
├── case-study.md         ← output (per il portfolio)
├── evolutive.md          ← note sul metodo (istanza) · backlog (blueprint)
├── procedure/            ← runbook (§8)
├── raw/
│   ├── input/            ← fonti dell'utente (immutabili)
│   └── output/           ← prodotte dall'agente: sintesi validate, prove
│       └── prova-XX-…/   ← una cartella per prova: nota + risultati
├── assets/               ← diagrammi
├── code/                 ← officina: pacchetto, script delle prove, test
├── data/                 ← audio e dataset (fuori da git)
└── models/               ← modelli pre-addestrati (fuori da git)
```

Chi possiede cosa è nella tabella *Cosa va dove* (§4). L'unica regola che vale già qui: `raw/` è
**immutabile**, l'LLM legge e non modifica.

## 4. Convenzioni

- Lingua: **italiano** (termini tecnici, nomi di servizio e citazioni da paper e documentazione in inglese dove serve).
- Link interni Obsidian `[[...]]`. Stato del file nel frontmatter (`bozza → in-revisione → validato`).
- **Vocabolario ID** (tracciabilità): ogni voce è citabile con `[[link]]`.

  | Prefisso | Significato | Casa |
  |---|---|---|
  | `REQ-x` | Requisito (da una fonte in `raw/` o da un'idea) | `requisiti.md` |
  | `VIN-x` | Vincolo trasversale (budget, tempo, stack…) | `requisiti.md` |
  | `ASS-x` | Ipotesi di merito, da verificare con un esperimento (volumi, comportamenti, prestazioni) | `requisiti.md` |
  | `SOL-x` | **Elemento del design** (componente o flusso) che copre un requisito | `soluzione.md` |
  | `DEC-x` | Decisione di design | `decisioni.md` |
  | `DOM-x` | Punto aperto (domanda, dubbio, info da cercare) | `decisioni.md` |

- **Stati decisione** (in `decisioni.md`): `proposta → decisa → chiusa` (+ `scartata`).
- **Cruscotto copertura** (`🟢` coperto · `🟡` parziale · `🔴` gap · `⚪` documentale): vive
  **solo** in `requisiti.md`.

### Budget di forma

Ogni tipo di contenuto ha una **forma obbligata** e un **tetto**. Il budget non toglie profondità,
la **sposta**: ciò che sfora non si cancella, cambia casa.

| Elemento | Forma | Tetto | Se sfora |
|---|---|---|---|
| `REQ` · `VIN` · `ASS` | una riga di tabella | ~250 car. | sono **due** voci, non una lunga |
| `DOM` | una riga di tabella | ~250 car. | il contesto sta nel `REQ`/`DEC` che blocca |
| `DEC` | i sei campi, max 2 righe l'uno, **nessun sotto-titolo** | ~900 car. | pagina di approfondimento linkata — o `soluzione.md`, se è design |
| Flusso in `soluzione` | max 6 passi numerati, una riga a passo | — | è più di un flusso |
| Dettaglio `SOL-x` in `soluzione` | i cinque campi fissi, max 3 righe l'uno | — | pagina di approfondimento linkata |
| `case-study` | 8 sezioni fisse; TL;DR max 3 righe, decisione chiave max 3 righe | 1–2 pagine | il dettaglio resta in `soluzione`/`decisioni`: si linka |
| Riga di `log` | una frase: cosa è cambiato + i numeri | ~300 car. | il dettaglio è già nei file che hai toccato |
| Riga in `evolutive` (`N-xx` / `EV-xx`) | spunto · perché · file toccati | ~250 car. a campo | — |

Uno sforamento è quasi sempre un **errore di ownership**: il blocco contiene roba di un altro tipo.
Prima di tagliare, chiedersi di chi è.

### Cruscotto di copertura

**A un requisito risponde il design, non una decisione.** La colonna *Copertura* punta quindi
all'elemento della soluzione che lo soddisfa, e di seguito alla decisione che l'ha modellato:
`REQ-04 🟢 → [[soluzione#SOL-3]] · [[decisioni#DEC-09]]`. Un requisito **non può essere 🟢 senza un
`SOL-x`**: una decisione da sola non basta, perché una scelta presa e non ancora riflessa nel
disegno non copre niente.

### Cosa va dove (ownership — regola anti-duplicazione)

Ogni informazione ha **una sola casa**. I rimandi si fanno con `[[link]]`, mai copiando.

| Contenuto | Casa unica | Nota |
|---|---|---|
| Obiettivo e non-obiettivi, requisiti, vincoli, ipotesi, **cruscotto di copertura** | `requisiti.md` | Solo requisiti: **niente soluzioni**. |
| **Design**: componenti e flussi (`SOL-x`), scelte tecniche, schema d'insieme, **dettaglio tecnico**, **valutazione** | `soluzione.md` | Non riscrivere i requisiti: rimanda a [[requisiti]]. È qui che un requisito viene **coperto**. |
| **Decisioni** (DEC-x): memoria del **perché**, con opzioni scartate e stato | `decisioni.md` | Non stanno sul percorso della copertura: il cruscotto passa dal `SOL-x`. Ogni `DEC` dichiara **dove è adottata**. |
| **Punti aperti** (`DOM-x`): domande, incongruenze, info da cercare | `decisioni.md` § *Punti aperti* | Chiusi, confluiscono in una `DEC`, un `REQ` o un'`ASS`. |
| **Case study** (storia del progetto per il portfolio) | `case-study.md` | Output a valle di una soluzione validata; nessun fatto nuovo, `deriva_da:` nel frontmatter. |
| **Spunti di evoluzione del metodo** | `evolutive.md` | Nell'istanza: note `N-xx` raccolte usando il metodo. Nel blueprint: backlog `EV-xx` in cui convergono le note delle istanze. Mai dati di un progetto. |
| **Budget di forma** (lunghezze e forme ammesse) | `CLAUDE.md` §4 | I runbook lo linkano; il controllo vive in [[lint]]. |
| **Principio HITL** (regole generali di fermata) | `CLAUDE.md` §1 | I runbook non lo riscrivono: lo linkano e dichiarano solo i **propri** punti di fermata. |
| Cronologia eventi | `log.md` | Append-only. |
| Catalogo / navigazione | `index.md` | — |
| Fonti immutabili | `raw/` | Leggo, non modifico. |
| Diagrammi | `assets/` | Linkati dai documenti, rigenerati a decisione chiusa. |
| **Codice** (pacchetto, script delle prove, test) | `code/` | Niente decisioni né risultati. Ogni script dichiara in testa l'ID della prova (`C01`…). Il codice non scrive mai nella wiki: produce evidenze. |
| **Prova** (nota + risultati di un esperimento) | `raw/output/prova-XX-<slug>/` | Nota `prova-XX-<slug>.md` (domanda → prova → cosa ho visto) + risultati piccoli (csv, json, png) con l'ID nel nome. Solo file nuovi; entra nella wiki con l'ingest. |
| Audio, dataset, modelli | `data/` · `models/` | **Mai in git** (diritti e licenze). Un `README.md` dice cosa scaricare e dove. |

## 5. Come lavoriamo (workflow)

> Ogni passo qui sotto è soggetto al **principio HITL** (§1): l'agente propone, l'utente valida,
> poi il contenuto entra nella wiki.

**Tre fasi.** *Capire* (fonti in `raw/` → [[requisiti]]) → *progettare* ([[soluzione]], con una
[[decisioni|decisione]] su ogni bivio) → *produrre* (diagrammi, [[case-study]]). Non si
chiudono in ordine: si torna indietro ogni volta che arriva una fonte nuova o si riapre una scelta.

**Ciclo di costruzione** — design → una `DEC` su ogni bivio → [[lint]] rapido → cruscotto. Gira
molte volte: è il grosso del lavoro.

**Ciclo di controllo** — [[lint]] completo, periodico: coerenza, decisioni non adottate a valle,
re-scoring.

**Chiusura** — [[lint]] completo senza 🔴 e valutazione con risultati misurati → [[creazione-case-study|case study]].

**Due regole di precedenza**: si parte dal **design proposto dall'utente** — l'agente lo struttura,
non inventa architetture; può proporre **alternative**, ma solo come opzioni di una `DEC`, e la
scelta resta dell'utente. E non si produce un output da un design **non validato**.

## 6. Grounding & verifica

- Claim tecnici verificati su fonti ufficiali/autorevoli, con URL. Non inventare nomi di
  servizio/feature.
- Distinguere **GA vs preview** quando conta per il progetto (es. un `VIN`).
- Tecnologia **agnostica** dove richiesto: ogni componente deve avere un equivalente sostituibile.

## 7. Convenzione log

Ogni riga: `## [YYYY-MM-DD] <ingest|design|query|lint|build> | <descrizione>`.
**Una frase**: cosa è cambiato più i numeri (~300 car., vedi *Budget di forma* in §4). Il
dettaglio vive nei file che hai toccato, non qui.
Ultimi 5 eventi: `grep "^## \[" log.md | tail -5`.

## 8. Comandi (procedure richiamabili)

Procedure fisse che l'agente esegue su parola-chiave. Ognuna vive in un **file-runbook a sé**, che
l'agente **rilegge per intero prima di eseguire** (così la versione in vigore è sempre l'ultima).

| Trigger | Runbook | Cosa fa |
|---|---|---|
| «crea requisiti» · «estrai requisiti» · «ingest» | [[creazione-requisiti]] | Da una fonte in `raw/` estrae requisiti/vincoli/ipotesi in `requisiti.md`. |
| «design» · «progetta» · «struttura soluzione» | [[creazione-soluzione]] | Struttura la soluzione in elementi `SOL-x` e apre una `DEC` su ogni bivio. |
| «diagramma» · «schema» · «disegna l'architettura» · «flusso dati» · «vista di rete» | [[creazione-diagrammi]] | **Dispatcher**: catalogo dei tipi, due livelli di zoom, viste rese obbligatorie dai vincoli, standard comune. Delega ai tipi generati. |
| «case study» · «scrivi il case study» · «portfolio» | [[creazione-case-study]] | Costruisce `case-study.md` da requisiti, soluzione e decisioni validati; aggiorna `deriva_da:`. |
| «valida» · «valida copertura» → rapida · «lint» · «riallineamento» · «aggiorna» → completa | [[lint]] | **Rapida**: copertura e cruscotto. **Completa**: copertura + controlli di coerenza, report e riga di log. |

I runbook vivono in `procedure/`. **Nuova procedura → nuovo file in `procedure/` + una riga qui.**
Ogni runbook dichiara i propri **Punti di fermata (HITL)**: dove si interrompe per farsi validare,
secondo il principio in §1.
