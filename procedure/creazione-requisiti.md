---
titolo: "Creazione requisiti — runbook (ingest)"
tags: [procedura, ingest, requisiti]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Creazione requisiti — runbook

Procedura fissa che l'agente esegue quando l'utente dice **«crea requisiti»**, **«estrai
requisiti»** o **«ingest»** su una fonte. È l'operazione *ingest* del pattern LLM-wiki: da una fonte
in `raw/` si ricavano i requisiti in [[requisiti]].

> **Regola d'uso**: l'agente **rilegge questo file per intero prima di eseguire**. Lavora **una
> fonte alla volta**, discute i take-away con l'utente prima di scrivere, e **non inventa** requisiti
> non supportati dalla fonte.
>
> Vale il **principio HITL** ([[CLAUDE]] §1): l'agente propone, tu validi. I **punti di
> fermata** di questa procedura sono in fondo.
>
> Vale il **budget di forma** ([[CLAUDE]] §4): un `REQ`/`VIN`/`ASS`/`DOM` sta in **una riga**.
> Se non ci sta, sono due voci.

## Passi (in ordine)

1. **Individua la fonte** — In `raw/`: quale materiale si lavora (idea, appunti, paper, repo di
   riferimento, esperimento precedente)? Se non è ovvio, chiedi. Al primo ingest si fissano anche
   **obiettivo e non-obiettivi** in testa a [[requisiti]].

2. **Leggi e sintetizza** — Leggi la fonte e proponi all'utente i **take-away** principali prima di
   scrivere. Attendi conferma/indirizzo su cosa enfatizzare.

3. **Estrai i requisiti** — Per ciascun requisito aggiungi una riga alla tabella *Requisiti* in [[requisiti]]:
   - **ID** progressivo `REQ-x`;
   - **Requisito** in una riga, chiaro e non ambiguo;
   - **Origine**: `idea`, `raw/<file>` (con sezione se utile) o `vincolo`;
   - **Copertura** iniziale ⚪ (il design la aggiornerà; il re-scoring vive in [[lint]]).

4. **Vincoli e ipotesi** — Se emergono, aggiungi `VIN-x` (budget, tempo, stack, limiti che ti
   imponi) e `ASS-x` (ipotesi di merito), ognuna con **come la verifichi**.

5. **Deduplica** — Se un requisito è già presente, **aggiorna/collega** invece di duplicarlo. Un
   requisito ha una sola riga, anche se più fonti lo toccano (cita le origini multiple).

6. **Ambiguità → domande** — Dove la fonte lascia dubbi, **non assumere in silenzio**: apri una
   `DOM` nei [[decisioni#Punti aperti|punti aperti]], e
   collega il requisito relativo.

7. **Aggiorna index e log** — Aggiungi la fonte all'elenco in [[index]]; appendi a [[log]] una riga:
   `## [YYYY-MM-DD] ingest | <fonte>: <n requisiti, n vincoli, n ipotesi, n domande>`.

## Report di fine-ingest

Chiudi sempre l'ingest con due righe: **quanti** `REQ`/`VIN`/`ASS` hai aggiunto, e **cosa non
torna** (ambiguità, contraddizioni, punti che richiedono una scelta dell'utente). I punti aperti si
instradano secondo la regola in [[CLAUDE]] §1: transitorio → si chiede in chat, persistente →
diventa una `DOM` nel tracker.

## Punti di fermata (HITL)

Applicazione del principio in [[CLAUDE]] §1 a questa procedura.

- 🛑 **La lista di `REQ`/`VIN`/`ASS` prima di scriverla** — proponila in chat (ID, testo, origine); in
  [[requisiti]] entra solo ciò che confermi. Un requisito che riformuli si scrive **con le tue parole**.
- 🛑 **Ogni `ASS-x`** — un'ipotesi è un'informazione che **manca**: va dichiarata e accettata, con
  il suo modo di verifica, mai scelta dall'agente per far tornare il quadro.
- 🔧 **Fix sicuri**: numerazione progressiva degli ID, copertura iniziale ⚪, fonte in [[index]] e
  riga di [[log]] — **dopo** che l'estrazione è stata validata.

## Cosa NON fa

- Non scrive soluzioni: qui si estraggono **solo** requisiti/vincoli/ipotesi (ownership:
  requisiti ≠ soluzione).
- Non tocca `raw/` (immutabile).
- Non chiude domande né decide ipotesi al posto dell'utente: le propone.
