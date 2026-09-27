---
titolo: "Requisiti, vincoli e ipotesi"
tags: [requisiti, vincoli, ipotesi]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Requisiti, vincoli e ipotesi

Cosa deve fare il progetto e **dentro quali limiti**. È la **checklist** contro cui si valida il
design in [[soluzione]]: qui **non si scrivono soluzioni**, solo obiettivo, requisiti, vincoli e
ipotesi. Le fonti sono idee, appunti, paper e repo di riferimento in `raw/`.

## Obiettivo e non-obiettivi

**Obiettivo** — _(2–3 righe: che problema risolve il progetto e cosa vuole dimostrare)_

**Non-obiettivi** — cosa resta **fuori**, per scelta:
- _(es. niente multi-tenant: un solo utente)_
- _(es. niente UI curata: basta una CLI o un notebook)_

## Cruscotto copertura (vs design)

Legenda: 🟢 coperto · 🟡 parziale (presente ma da completare) · 🔴 gap (assente/insufficiente) ·
⚪ documentale (non nel disegno tecnico).

**Stato attuale: 🟢 0 · 🟡 0 · 🔴 0 · ⚪ 0** — _(aggiornare a ogni re-scoring)_

> La copertura vive **solo qui**. La colonna *Copertura* punta all'**elemento della soluzione**
> che soddisfa il requisito e, di seguito, alla decisione che l'ha modellato:
> `REQ-01 🟢 → [[soluzione#SOL-1]] · [[decisioni#DEC-01]]`.
> **Senza un `SOL-x` non si è 🟢**: una decisione presa ma non ancora riflessa nel design non copre.

## Vincoli (valgono su tutto il progetto)

| ID | Vincolo | Origine | Nota |
|---|---|---|---|
| VIN-1 | _(es. budget cloud: solo free tier / < 20 €/mese)_ | _(scelta personale)_ | — |
| VIN-2 | _(es. tempo: ~4 h a settimana, MVP in 6 settimane)_ | — | — |
| VIN-3 | _(es. stack da dimostrare: LangGraph + Azure AI Foundry)_ | — | — |

## Requisiti

| ID | Requisito | Origine | Copertura |
|---|---|---|---|
| REQ-01 | _(descrizione del requisito)_ | _(idea / `raw/<file>` / vincolo)_ | ⚪ _(→ [[soluzione#SOL-…]] · [[decisioni#DEC-…]])_ |
| REQ-02 | | | |
| REQ-03 | | | |

## Ipotesi

Ipotesi **di merito** su cui poggia il design (volumi, comportamento di un modello, qualità dei
dati, prestazioni). Non si confermano chiedendo: si **verificano**, con un esperimento o una misura.

| ID | Ipotesi | Perché la assumo | Come la verifico |
|---|---|---|---|
| ASS-01 | _(es. un modello small basta per la classificazione)_ | _(es. benchmark pubblico, intuizione)_ | _(es. eval su 50 casi, soglia F1 ≥ 0.8)_ |
| ASS-02 | | | |
