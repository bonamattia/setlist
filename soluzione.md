---
titolo: "Soluzione — design end-to-end"
tags: [soluzione, design, architettura]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Soluzione — design end-to-end

Qui vive il **come**. Due livelli di lettura:
- **panoramica** — schema d'insieme, componenti, flussi: leggibile da chiunque, è la base del
  case study;
- **dettaglio tecnico** — stack, interfacce, logica, limiti: **solo** per i `SOL-x` in cui una
  scelta lo merita.

Per ogni scelta c'è un riferimento a [[decisioni]] con una riga di motivazione.

> Regola anti-duplicazione: qui **non si riscrivono i requisiti** né si duplica il cruscotto —
> si rimanda a [[requisiti]]. Le decisioni con motivazione stanno in [[decisioni]].

## Schema d'insieme

_(diagramma end-to-end — embed dell'Excalidraw in `assets/`, es. `![[assets/architettura-e2e.excalidraw]]`._
_Parti dallo scheletro `assets/_schema-logico.excalidraw`; per lo standard vedi [[creazione-diagrammi]].)_

Sintesi in una riga: _(cosa fa la soluzione, dall'input all'output)_

## Componenti e flussi (`SOL-x`)

Gli elementi del design sono ciò che **copre** i requisiti: il cruscotto in [[requisiti]] punta qui.
Numerazione unica `SOL-x` per componenti e flussi — al cruscotto interessa cosa copre, non se sia
una scatola o una sequenza.

| ID | Elemento | Tipo | Ruolo | Requisiti coperti | Decisione |
|---|---|---|---|---|---|
| SOL-1 | _(nome)_ | componente | _(a cosa serve)_ | [[requisiti#REQ-01]] | [[decisioni#DEC-01]] |
| SOL-2 | | | | | |

Un `SOL-x` senza **Requisiti coperti** è un segnale: o manca un requisito, o stiamo costruendo
qualcosa che nessuno ha chiesto.

### SOL-… · _(nome flusso, es. ingestione dati)_

_(passi principali, una riga a passo — max 6; se sono di più, è più di un flusso)_

### SOL-… · _(nome flusso, es. query / retrieval)_

_(passi principali)_

## Dettaglio tecnico

Un blocco per ogni `SOL-x` con scelte **non banali** — non per tutti. Campi fissi, max 3 righe
l'uno ([[CLAUDE]] §4): ciò che sfora va in una pagina di approfondimento linkata.

### SOL-… · _(nome)_ — dettaglio

- **Stack**: _(tecnologie e versioni, con link alla doc ufficiale)_
- **Interfacce**: _(input/output, schema dati, contratti con gli altri `SOL-x`)_
- **Logica chiave**: _(prompt, algoritmo, pattern — es. routing condizionale in LangGraph)_
- **Limiti noti**: _(cosa non fa, dove si rompe, cosa costa)_
- **Codice**: _(link al repo / path, se esiste)_

## Valutazione

Come si misura che la soluzione **funziona**. È qui che si verificano le ipotesi di
[[requisiti#Ipotesi]]: ogni `ASS-x` con un *Come la verifico* trova qui metrica e risultato.

| Cosa si misura | Metrica | Dataset / metodo | Soglia | Risultato | Verifica |
|---|---|---|---|---|---|
| _(es. qualità risposte)_ | _(es. faithfulness)_ | _(es. 50 domande annotate a mano)_ | _(≥ 0.8)_ | _(da misurare)_ | [[requisiti#ASS-01]] |

## Scelte tecniche

Ogni scelta rimanda alla decisione che la motiva (con stato e alternative) in [[decisioni]].

- _(area, es. storage)_ → riferimento: _(tecnologia)_ · vedi [[decisioni#DEC-…]]
- _(area, es. orchestrazione)_ → riferimento: _(tecnologia)_ · vedi [[decisioni#DEC-…]]

## Punti aperti

Dubbi che toccano il design e non sono ancora chiusi: vedi [[decisioni#Punti aperti]].
