---
tipo: log
tags: [log]
---

# Log — cronologia append-only

Convenzione: `## [YYYY-MM-DD] <ingest|design|query|lint|build> | <descrizione>`.
Ultimi 5 eventi: `grep "^## \[" log.md | tail -5`.

## [2026-07-23] build | Inizializzato il vault-blueprint: CLAUDE.md (schema) + stub di requisiti, soluzione, decisioni, index, log.

## [2026-08-06] build | EV-01 applicata: principio HITL come `CLAUDE.md` §1 (rinumerate le sezioni successive) + sezione «Punti di fermata (HITL)» nei 7 runbook di `procedure/`.

## [2026-08-06] build | EV-05 applicata: assunzioni di inquadramento `ASS-G` in `requisiti.md` (natura intervento, budget, rate, orizzonte) + passo di inquadramento e avviso in piano/costi + controllo nel riallineamento.

## [2026-08-06] query | backport a mano da un'istanza reale: analisi di CLAUDE.md, log, runbook e convenzioni → 13 nuovi candidati in [[evolutive]] (EV-08…EV-20: 7 backport di metodo collaudato, 6 attriti emersi dal log). EV-06 ed EV-07 spostate in Scartate perché superate da EV-08. Nessuna modifica al metodo in questo giro.

## [2026-08-06] query | evolutive: EV-21 (budget di forma), EV-22 (catalogo diagrammi, ricerca su archify + C4), EV-23 (revisione critica) da UX d'uso; EV-20 estesa alla lettura del log come diario degli attriti.

## [2026-08-06] build | EV-21 applicata: budget di forma in `CLAUDE.md` §4 (forma + tetto per REQ/DOM/DEC/flussi/log/EV), richiamato in creazione-requisiti e creazione-soluzione, controllo nel passo ownership del riallineamento. Collaudo: `evolutive.md` ricompattato, mediana riga EV 842→386 car.

## [2026-08-06] build | EV-23 (1/n) `CLAUDE.md`: precisata l'operazione `query` in §0 (interrogare la wiki; si logga solo se produce un artefatto) ed eliminata §8 *Strumenti opzionali* (Dataview/qmd/Marp, mai adottati in due settimane di caso reale). Sezione *Comandi* rinumerata §9→§8.

## [2026-08-06] build | EV-26: copertura invertita in `REQ → SOL-x → DEC`. Nuovo prefisso `SOL-x`, `decisioni` diventa memoria del perché con campo *Adottata in*, senza `SOL-x` non si è 🟢. Toccati 9 file + rigenerato `_schema-logico` (DECISIONI non è più in mezzo). Assorbe EV-16.

## [2026-08-06] build | EV-23 su `CLAUDE.md`: compressa la tabella fix sicuri/merito, tolte due frasi retoriche in §1 e la metà di regola che ripeteva §7, ridotti a due parole i commenti dell'albero in §3 (ripetevano la tabella ownership). 14.096 → 13.156 car., nessuna regola rimossa.

## [2026-08-06] build | EV-23 sui runbook: potati i sette blocchi *Punti di fermata (HITL)*, 35 → 21 bullet, 5.543 → 3.445 car. Criterio: via i bullet che parafrasano un passo già scritto sopra o la Regola d'uso. Nessuna fermata nuova, nessun 🔧 Fix sicuri rimosso.

## [2026-08-06] build | EV-23 su `index.md`: 2.507 → 1.559 car. Tolti trigger e descrizioni dei runbook (casa unica in CLAUDE §8), accorciate le righe dei file di lavoro, corretta la riga di flusso che citava ancora il vecchio workflow in sei passi invece delle tre fasi.

## [2026-08-06] build | EV-27: terzo asse **solidità**. Colonna *Poggia su* in `soluzione`, marcatore `🟢*` nel cruscotto, assegnazione in `validazione`, due controlli nel `riallineamento` + il **controllo inverso** (`SOL-x` che non copre nulla). Toccati 5 file.

## [2026-08-06] build | EV-23 su `creazione-requisiti`: *Report di fine-ingest* da 12 righe a 4 — la regola transitori/persistenti era finita in `CLAUDE.md` §1 stamattina e qui restava duplicata. Nuova EV-28 (categorie nella matrice requisiti) registrata come spunto.

## [2026-08-06] build | EV-09 backportata: nuovo `creazione-gantt` (specifica JSON + generatore + referto di verifica), collegato da `creazione-piano` passo 6, CLAUDE §8, index e `creazione-diagrammi`. Generatore collaudato: 6 barre, 20 gg, nessun overload.

## [2026-08-06] query | analisi di `tt-a1i/archify` (README, SKILL.md, DESIGN.md): EV-22 spezzata in 22a catalogo trigger → tipo, 22b referto di layout + palette semantica, 22c generatori per tipo. Scartati HTML interattivo, CLI npm/ajv e la loro palette cloud.

## [2026-08-06] build | EV-22a: `creazione-diagrammi` riscritto come dispatcher — catalogo di sei tipi, trigger dedicati, due livelli per lettore, viste obbligatorie in presenza di certi `VIN`. Un tipo diventa runbook a sé solo quando ha un generatore.

## [2026-08-06] design | EV-22c ridotta al solo generatore *flusso dati*, in attesa di un caso reale su cui collaudarlo. Scartati i generatori per HLD, sequenza, ciclo di vita e deployment: lì il layout è una scelta di comunicazione e il referto non avrebbe nulla da verificare.

## [2026-08-06] build | EV-22b: palette semantica fissa (7 significati) e §7 verifiche ridotte a 4 in `creazione-diagrammi`; `_template.excalidraw` allineato. Con EV-22a e la 22c ridotta, il tema diagrammi è chiuso salvo il generatore flusso dati.

## [2026-09-25] build | DD-01: rimossi gli output commerciali (costi-servizio, piano-progetto, runbook costi/piano/gantt) e il blocco ASS-G; rimandi puliti in CLAUDE, index, requisiti, soluzione, riallineamento (passo 8 tolto) e creazione-diagrammi.

## [2026-09-25] build | DD-02: requisiti declinati per progetti personali — blocco obiettivo/non-obiettivi, colonna Fonte → Origine, vincoli personali, assunzioni → ipotesi con «Come la verifico»; allineati creazione-requisiti, riallineamento, CLAUDE (ID, ownership, §8), decisioni, README.

## [2026-09-25] build | DD-03: cartella domande/ (2 file) sostituita dalla sezione Punti aperti in decisioni.md — DOM-x senza distinzione C/I, via Sollevata da e A chi; rimandi aggiornati in CLAUDE, creazione-requisiti, creazione-soluzione, riallineamento, soluzione, index, README.

## [2026-09-25] build | DD-04: cruscotto semplificato — via i tre assi da CLAUDE §4, il marcatore * e la colonna Poggia su; resta la regola «niente 🟢 senza SOL-x» e il controllo SOL-x senza requisiti; validazione e riallineamento allineati.

## [2026-09-25] build | DD-05: validazione + riallineamento fusi in procedure/lint.md con due modalità (rapida = copertura, completa = copertura + 7 controlli di coerenza); trigger invariati; rimandi aggiornati in CLAUDE, creazione-soluzione, creazione-requisiti, decisioni, index.

## [2026-09-25] build | DD-06: soluzione.md su due livelli (panoramica + dettaglio tecnico) — nuove sezioni Dettaglio tecnico (5 campi fissi per i SOL-x non banali) e Valutazione (metriche legate alle ASS-x); creazione-soluzione con 2 nuovi punti di fermata; budget di forma +1 riga.

## [2026-09-25] build | DD-07: README declinato per progetti personali (titolo, intro, raw, istanziazione, +2 righe tabella); evolutive: backlog ridotto da 18 a 6 EV (16, 17, 18, 20, 22c, 28), Applicate/Scartate azzerate con riga di origine da main @4a8c23a, registro DD, nuovi EV da 29.

## [2026-09-25] build | DD-08: nuovo output case-study.md (8 sezioni, deriva_da:, lingua per istanza) + runbook creazione-case-study (5 passi, 3 fermate); CLAUDE §2 lingua, §3, §4 (ownership + budget), §8; index; lint +controllo 13 case study allineato.

## [2026-09-25] build | DD-10: CLAUDE.md riscritto per progetti personali — titolo e intro, §0 fonti raw e regola query, §1 output, §2 Contesto del progetto (5 campi, via perimetro e obiettivo), §3 albero, §4 ID/ownership, §5 chiusura e alternative come opzioni DEC, §6 GA/preview.

## [2026-09-25] build | DD-11: residui da prevendita tolti (index, raw/README, creazione-diagrammi: lettore vista d'insieme e palette «esterno»); evolutive a due ruoli (note N-xx nell'istanza, backlog EV-xx di convergenza nel blueprint) in evolutive, CLAUDE, README, index; README: istanziazione svuota log ed evolutive.

## [2026-09-25] lint | completa (collaudo blueprint): 🟢0 · 🟡0 · 🔴0 · ⚪0 · 0 fix, 4 segnalazioni (terminologia matrice/deliverable, [[README]] ambiguo, disegno orfano vuoto, registro DD).

## [2026-09-25] build | DD-12: chiuse le 4 segnalazioni del lint — terminologia in CLAUDE, creazione-requisiti, creazione-diagrammi; link README espliciti; canvas vuoto Excalidraw/ eliminato; _schema-logico ridisegnato (case study al posto di piano/costi, punti aperti, lint, 6 frecce orfane rimosse); registro DD chiuso.

## [2026-09-27] query | evolutive: aggiunte 5 note N-01…N-05 sui difetti del blueprint emersi alla prima lettura dell'istanza Setlist (istanziazione, stampo vs istanza, apprendimento, ponte repo, esperimenti leggeri).

## [2026-09-27] build | raw: nuova fonte setlist-riorientamento-macroaree (7 macroaree A–G + 3 fuori percorso, sequenza in 7 step) e prova A-01 (MTG-Jamendo: 1.435 brani metal, 377 post-rock, 598 instrumental rock, 0 sludge); index aggiornato.

## [2026-09-27] build | raw/ diviso in input/ (1 file: setlist-first-ideas) e output/ (2 file: riorientamento-macroaree, prova-A01); aggiornati raw/README, index; nota N-06 in evolutive.

## [2026-09-27] build | vault → repo pubblico: CLAUDE §2 compilato, §3 albero (code/, data/, models/, cartelle-prova), §4 +3 righe ownership; README riscritto in inglese; .gitignore/.gitattributes; scheletro code/; prova A-01 in cartella; N-04 e N-07 applicate.
