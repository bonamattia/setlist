---
titolo: "Creazione case study — runbook"
tags: [procedura, case-study, portfolio, output]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Creazione case study — runbook

Procedura fissa che l'agente esegue quando l'utente dice **«case study»**, **«scrivi il case
study»** o **«portfolio»**. Produce [[case-study]], l'**unico output finale** di un'istanza: la
storia del progetto per un lettore esterno (recruiter tecnico, CTO, cliente potenziale).

> **Regola d'uso**: l'agente **rilegge questo file per intero prima di eseguire**. Il case study
> **non introduce fatti nuovi**: riorganizza ciò che è validato in [[requisiti]], [[soluzione]] e
> [[decisioni]]. Se serve un contenuto che lì non c'è, va prima scritto lì.
>
> Vale il **principio HITL** ([[CLAUDE]] §1): l'agente propone, tu validi. I **punti di
> fermata** di questa procedura sono in fondo.
>
> Vale il **budget di forma** ([[CLAUDE]] §4): 1–2 pagine in tutto.

## Passi (in ordine)

1. **Prerequisiti** — Verifica: [[lint]] rapido **senza 🔴**; *Valutazione* in [[soluzione]] con
   **risultati misurati**; lingua fissata in [[CLAUDE]] §2. Se manca qualcosa, **dillo e fermati**:
   un output derivato non si auto-promuove ([[CLAUDE]] §1).

2. **Decisioni chiave** — Proponi 3–5 `DEC` da raccontare, con una riga di motivo ciascuna: quelle
   dove il bivio era reale e la scelta dice qualcosa di come ragioni.

3. **Scaletta e TL;DR** — Proponi il TL;DR (max 3 righe) e una riga per sezione del template.

4. **Stesura** — Compila [[case-study]] nella lingua dell'istanza. Regole:
   - ogni affermazione ha una casa nel vault; i numeri vengono **solo** dalla *Valutazione*;
   - i **limiti si dichiarano**: un case study senza limiti non è credibile;
   - registro da **panoramica**, dettaglio tecnico solo dove serve a capire una decisione.

5. **Chiusura** — Aggiorna `deriva_da:` nel frontmatter (file sorgente con il loro
   `ultimo_aggiornamento`), aggiungi il case study a [[index]] se manca, appendi a [[log]]:
   `## [YYYY-MM-DD] build | case study: <sezioni scritte/aggiornate>`.

## Punti di fermata (HITL)

Applicazione del principio in [[CLAUDE]] §1 a questa procedura.

- 🛑 **Le decisioni chiave** (passo 2) — cosa raccontare è una scelta tua.
- 🛑 **TL;DR e scaletta** (passo 3) — si scrive dopo l'ok.
- 🛑 **La stesura** — presentata sezione per sezione, o in blocco se lo chiedi.
- 🔧 **Fix sicuri**: `deriva_da:`, wikilink, riga di [[index]] e di [[log]].

## Cosa NON fa

- Non aggiunge fatti, numeri o decisioni che non siano già nel vault.
- Non si scrive su un design con 🔴 o senza risultati misurati.
- Non pubblica: la pubblicazione (sito, README del repo, post) è fuori dal vault.
