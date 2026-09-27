---
titolo: "Creazione soluzione & decisioni — runbook (design)"
tags: [procedura, design, soluzione, decisioni]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Creazione soluzione & decisioni — runbook

Procedura fissa che l'agente esegue quando l'utente dice **«design»**, **«progetta»** o
**«struttura soluzione»**. Copre il passaggio centrale del metodo: dai [[requisiti]] si struttura
il **COME** in [[soluzione]], aprendo una **decisione** ([[decisioni]]) ogni volta che serve una
scelta. La soluzione è il ponte *cosa ↔ come*; le decisioni le stanno accanto e la spiegano.

> **Regola d'uso**: l'agente **rilegge questo file per intero prima di eseguire**. Vale il
> **design-first**: si parte dal design proposto dall'utente; l'agente lo **struttura**, non inventa
> architetture. Ogni bivio con più di un'opzione diventa una `DEC`, non una scelta implicita.
>
> Vale il **principio HITL** ([[CLAUDE]] §1): l'agente propone, tu validi. I **punti di
> fermata** di questa procedura sono in fondo.
>
> Vale il **budget di forma** ([[CLAUDE]] §4): una `DEC` sono i sei campi, max 2 righe l'uno e
> **nessun sotto-titolo**. Se sfora è quasi sempre design: la casa è [[soluzione]].

## Passi (in ordine)

1. **Punto di partenza** — Leggi [[requisiti]] (`REQ`/`VIN`/`ASS`) e il design proposto
   dall'utente. Chiarisci cosa è in scope.

2. **Struttura la soluzione** — In [[soluzione]] compila: schema d'insieme, componenti e flussi
   numerati **`SOL-x`** (ognuno coi `REQ` che copre), scelte tecniche. Usa etichette **coerenti** con quelle dei
   diagrammi. **Non riscrivere i requisiti**: rimanda con `[[requisiti#REQ-…]]`.
   Poi, sull'ossatura validata: compila il **Dettaglio tecnico** solo per i `SOL-x` con scelte non
   banali (stack, interfacce, logica chiave, limiti noti, codice) e imposta la **Valutazione**,
   collegando ogni metrica all'`ASS-x` che verifica. Claim tecnici con fonte ([[CLAUDE]] §6).

3. **Apri le decisioni** — Ad ogni bivio crea una `DEC` in [[decisioni]] con: **innesco**
   (requirement-driven / design-driven / da domanda), opzioni, scelta, motivazione (fonti con URL
   se da ricerca), **Adottata in** (il `SOL-x` che modella), stato iniziale `proposta`.

4. **Collega** — Nella [[soluzione]] richiama le decisioni (`[[decisioni#DEC-…]]`).

5. **Valida** — Esegui [[lint]] in modalità **rapida**: verifica che ogni requisito abbia un `SOL-x` che lo copre e
   aggiorna il cruscotto (`REQ 🟢 → [[soluzione#SOL-…]] · [[decisioni#DEC-…]]`). La validazione è **parte del
   processo di design**, non un passo opzionale: se restano `🔴 gap`, il design non è completo.

6. **Diagrammi** — Crea/aggiorna lo schema end-to-end seguendo [[creazione-diagrammi]] (parti dal
   template `assets/_schema-logico.excalidraw`) ed embeddalo nella [[soluzione]].

7. **Ambiguità → domande** — Dove manca un'informazione o serve una scelta non tua, apri una `DOM`
   nei [[decisioni#Punti aperti|punti aperti]], con cosa **Blocca**.

8. **Log** — Appendi a [[log]]: `## [YYYY-MM-DD] design | soluzione: <cosa strutturato, n DEC aperte>`.

## Punti di fermata (HITL)

Applicazione del principio in [[CLAUDE]] §1 a questa procedura.

- 🛑 **L'ossatura prima di scriverla** — componenti e flussi si presentano in elenco; in [[soluzione]]
  si scrive dopo l'ok. Si struttura **il tuo** design: l'agente non propone architetture al posto tuo.
- 🛑 **Quali `SOL-x` meritano il dettaglio** — l'agente propone l'elenco con una riga di motivo; la
  scelta è tua, perché è una scelta di **comunicazione** (cosa mostrare), non di design.
- 🛑 **Metriche e soglie della Valutazione** — le proponi o le confermi tu: una soglia scelta
  dall'agente per far tornare il risultato non vale.
- 🛑 **Ogni bivio** — l'agente apre la `DEC` con opzioni e una raccomandazione motivata, ma **la
  scelta è tua**, e lo stato `decisa`/`chiusa` lo metti tu.
- 🔧 **Fix sicuri**: wikilink e rimandi, numerazione `SOL-x` e `DEC-x`, riga di [[log]].

## Cosa NON fa

- Non riscrive i requisiti (li rimanda) né duplica il cruscotto.
- Non congela le decisioni al posto tuo: le apre come `proposta` e ti segnala quelle da chiudere.
- Non fa i controlli di coerenza del vault: quelli sono [[lint]] in modalità completa.
