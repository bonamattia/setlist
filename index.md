---
tipo: index
tags: [index]
ultimo_aggiornamento: 2026-09-27
---

# Index — Design Dev Wiki

Catalogo del vault: **cosa esiste e dove sta**. Il metodo è nello [[CLAUDE|schema]].
Tre fasi: **capire** (fonti → requisiti) → **progettare** (soluzione + decisioni) → **produrre**
(diagrammi, case study).

## File di lavoro
- [[requisiti]] — il **COSA**: obiettivo, requisiti, vincoli, ipotesi e cruscotto di copertura.
- [[soluzione]] — il **COME**: elementi `SOL-x`. È qui che un requisito viene coperto.
- [[decisioni]] — il **PERCHÉ**: memoria delle scelte, con stati.
- [[decisioni#Punti aperti]] — dubbi aperti (`DOM-x`), accanto alle decisioni in cui confluiscono.
- [[case-study]] — output: la storia del progetto per il portfolio.

## Governo del vault
- [[CLAUDE]] — schema: struttura, convenzioni, comandi.
- [[README.md|README]] — cos'è il blueprint e come istanziarlo.
- [[evolutive]] — note sul metodo (nell'istanza) · backlog di convergenza (nel blueprint).
- [[log]] — cronologia append-only.

## Procedure (`procedure/`)

Runbook richiamabili a parola-chiave. **Trigger e descrizioni in [[CLAUDE]] §8**, casa unica.

[[creazione-requisiti]] · [[creazione-soluzione]] · [[creazione-diagrammi]] · [[creazione-case-study]] · [[lint]]

## Fonti (in `raw/`: `input/` tue · `output/` prodotte dall'agente)
- [[setlist-first-ideas]] — prime idee (v0.1): Setlist come DJ set, obiettivo di carriera, aree di studio.
- [[setlist-riorientamento-macroaree]] — riorientamento: metal/rock strumentale, scaletta live, macroaree A–G e sequenza degli step.
- [[prova-A01-mtg-jamendo-conteggi]] — prova A-01: conteggi di metal/rock in MTG-Jamendo (cartella in `raw/output/`).

## Codice e dati
- `code/` — officina: pacchetto, script delle prove, test (fuori dall'indice di Obsidian).
- `data/` · `models/` — fuori da git; cosa scaricare nei rispettivi `README.md`.

## Diagrammi (`assets/`)
- _(link agli Excalidraw dell'architettura)_
