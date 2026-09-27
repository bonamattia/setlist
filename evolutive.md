---
titolo: "Evolutive del metodo — appunti"
tags: [evolutive, appunti, backlog]
stato: bozza
ultimo_aggiornamento: 2026-09-27
---

# Evolutive del metodo — appunti

Quaderno degli **spunti di miglioramento** del metodo. Ha **due ruoli**:
- **nell'istanza** — taccuino di note sul metodo, raccolte giorno per giorno usando il blueprint su
  quel progetto. Righe con ID locale `N-xx`: l'ID `EV` si assegna solo alla convergenza;
- **nel blueprint** — backlog in cui, periodicamente, si fanno **convergere** le note di tutte le
  istanze. Dalle istanze torna il **metodo**, mai i dati del progetto.

> Regola: **buttalo giù grezzo, subito.** Una riga vale più di un'idea perfetta dimenticata.
> Stati: `spunto → da valutare → accettata → applicata` (+ `scartata`).

## Note dell'istanza (N-xx)

| ID | Data | Spunto | Origine | Perché / cosa risolve | Dove tocca | Stato |
|---|---|---|---|---|---|---|
| N-01 | 2026-09-27 | **Istanziazione incompleta e non verificata**: §2 con segnaposto, `log`/`evolutive`/`index` ancora con i dati del blueprint. Serve una checklist (o script) di istanziazione con verifica finale. | prima lettura istanza Setlist | Il passo 1 del README è manuale e si salta: l'istanza parte sporca e il primo lint segnalerebbe rumore non del progetto. | `README.md` · `CLAUDE.md` §2 · `log` · `evolutive` · `index` | spunto |
| N-02 | 2026-09-27 | **Il testo dello stampo resta nell'istanza**: `CLAUDE.md` dice «qui non devono mai finire dati di un progetto» anche dopo la copia. | prima lettura istanza Setlist | Istruzione in conflitto con §2 da compilare: l'agente riceve due regole opposte. Serve un'intestazione che cambi fra blueprint e istanza. | `CLAUDE.md` intro · `README.md` | spunto |
| N-03 | 2026-09-27 | **Nessuna casa per l'apprendimento**: aree di studio, cosa ho imparato, risorse. Non è REQ, né SOL, né DEC. | `raw/setlist-first-ideas.md` §5 | Se l'obiettivo è imparare facendo, metà del valore resta fuori dal vault o finisce nella casa sbagliata. Valutare un file `studio.md` + riga in ownership. | `CLAUDE.md` §3–§4 · `index` · nuovo file | spunto |
| N-04 | 2026-09-27 | **Manca il ponte repo ↔ vault**: come i risultati di codice ed esperimenti entrano in `raw/` e nella *Valutazione*. | prima lettura istanza Setlist | In un progetto personale il prodotto vero è codice + misure: senza un canale definito il vault racconta un progetto diverso da quello che esiste. | `soluzione` §Valutazione · `raw/README` · `lint` | applicata nell'istanza (code/ + prove in raw/output/) |
| N-05 | 2026-09-27 | **Formato leggero per esperimenti esplorativi** (spike: domanda → prova → cosa ho visto), senza catena REQ→SOL→DEC→case study. | cambio di obiettivo: esplorare il dominio | Il metodo è tarato su un progetto con case study finale; per prove brevi di apprendimento è troppo pesante e scoraggia a registrarle. | `CLAUDE.md` §5 · nuovo template/runbook · `index` | spunto |
| N-06 | 2026-09-27 | **`raw/` diviso in `input/` (fonti dell'utente) e `output/` (materiale prodotto dall'agente: sintesi validate, risultati di prove).** | l'agente ha scritto proprie sintesi in `raw/` | Senza distinzione, le fonti dell'utente e le produzioni dell'agente si confondono e l'immutabilità di `raw/` perde senso. Applicato nell'istanza, da far convergere. | `raw/README` · `CLAUDE.md` §0 §3 §4 · runbook `creazione-requisiti` e `lint` (passo 6) | applicata nell'istanza |
| N-07 | 2026-09-27 | **`README.md` ha due ruoli in conflitto**: nel blueprint spiega come istanziare; nell'istanza pubblicata è la vetrina del progetto su GitHub. | repo pubblico dell'istanza Setlist | Istanziando, il README dello stampo resta e presenta il metodo invece del progetto. Serve un template di README-progetto e la guida allo stampo altrove (es. `procedure/istanziazione.md`). | `README.md` · `CLAUDE.md` §3 · N-01 | applicata nell'istanza (README riscritto) |

## Backlog

> Derivato da `main` @ `4a8c23a` (blueprint di prevendita): lo storico `EV` completo è lì. Qui
> restano solo gli spunti che valgono anche per il design. **I nuovi `EV` partono da EV-29.**

| ID | Data | Spunto | Origine | Perché / cosa risolve | Dove tocca | Stato |
|---|---|---|---|---|---|---|
| EV-16 | 2026-08-06 | **Checklist di propagazione** alla chiusura di una `DEC`: cruscotto, componente, scelte tecniche, flussi, diagrammi, punti aperti. | attrito dal log | Due volte una decisione presa e non adottata a valle, scoperta dal lint giorni dopo, sopra lavoro già fatto su un design incoerente. | `creazione-soluzione` · `decisioni.md` · `lint` | spunto |
| EV-17 | 2026-08-06 | **Il lint verifica i propri fix**: rilegge i file dopo aver scritto e conferma ogni 🔧 dichiarato. | attrito dal log | Ha riportato come applicati due fix che non lo erano. Un lint di cui non ci si può fidare è peggio di nessun lint. | `lint` · `CLAUDE.md` §1 | spunto |
| EV-18 | 2026-08-06 | **Debito dichiarato**: una segnalazione che si decide di non chiudere si registra con motivazione, e il lint smette di ripeterla come nuova. | attrito dal log | «Restano aperte per scelta dell'utente le segnalazioni 5 e 6»: al giro dopo riappaiono identiche e il rumore copre quelle vere. | `lint` · dove registrarlo (punti aperti in `decisioni` o coda di `log`) **da decidere** | spunto |
| EV-20 | 2026-08-06 | **Runbook di `backport`**: diff istanza ↔ blueprint **e** lettura del `log` come diario degli attriti; separa metodo da dati cliente e produce righe `EV`. | attrito dal log | È l'operazione mancante del pattern. Nel caso reale il consolidamento è passato lateralmente fra due istanze senza mai toccare lo stampo. | nuovo `procedure/backport.md` · `CLAUDE.md` §0 e §comandi · `README.md` | spunto |
| EV-22c | 2026-08-06 | **Generatore per il flusso dati** (solo questo tipo), con contratto fisso: posizioni **logiche a griglia** (`stage`/`riga`, mai pixel), confini dichiarati per contenuto (`wraps: [id]`), **`classification` sui flussi** per i dati sensibili, legenda come dato; **vietati** i campi di aggiustamento (`labelDx`/`labelDy`/`labelAt`). Da scrivere **su un caso vero**, non in anticipo. | rif. archify | Un generatore si ripaga se **verifica** o tiene **coerente** qualcosa. Qui: coerenza fra le pipeline della stessa proposta e la marcatura dei flussi sensibili, che su un `VIN` di residenza dati trasforma il disegno in un documento che risponde a un vincolo. **Valutati e scartati** i generatori per HLD, sequenza, ciclo di vita e deployment: lì il layout è una **scelta di comunicazione**, non un calcolo — il Gantt si ripaga perché la larghezza di una barra *è* le giornate, un blocco di HLD sta al centro perché è il perno del racconto. E il loro referto non avrebbe nulla da verificare che la griglia non impedisca già. | nuovo generatore in `procedure/` · `assets/` · dipende da EV-22a | spunto (in attesa di un caso reale) |
| EV-28 | 2026-08-06 | **Categorie nella matrice requisiti**: la tabella è piatta, il caso reale l'ha divisa in funzionali (per area), non funzionali (accesso, sicurezza, deployment) e **documentali** (deliverable e attività). Da valutare se i documentali meritino anche una regola propria. | analisi istanza reale | I documentali si comportano diversamente: sono quelli che nel cruscotto finiscono ⚪ perché non stanno nel disegno tecnico. Senza categorie la distinzione si reinventa a ogni proposta. | `requisiti.md` (matrice) · `creazione-requisiti` · eventualmente `validazione` (regola sui ⚪) | spunto |

## Applicate

| ID | Data | Cosa è cambiato | Nota |
|---|---|---|---|
| DD-01…12 | 2026-09-25 | **Declinazione per progetti personali**: via output commerciali e `ASS-G` (01); requisiti con obiettivo/non-obiettivi e ipotesi verificabili (02); `domande/` → punti aperti in `decisioni` (03); cruscotto senza tre assi, `*`, *Poggia su* (04); `validazione` + `riallineamento` → `lint` a due modalità (05); `soluzione` su due livelli con dettaglio tecnico e valutazione (06); README ed evolutive per progetti (07); `case-study` + runbook, lingua per istanza (08); `raw/` tenuto (09, scartato); `CLAUDE.md` riscritto (10); residui di prevendita tolti, evolutive a due ruoli (11); collaudo lint, schema logico ridisegnato (12). | chiusa |

## Scartate (con motivo)

| ID | Spunto | Perché no |
|---|---|---|

## Collegamenti

[[CLAUDE]] (schema) · [[index]] · [[log]]
