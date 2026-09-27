---
titolo: "Decisioni di design (ADR-lite)"
tags: [decisioni, adr]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Decisioni di design (ADR-lite)

Il **perché** delle scelte. Ogni decisione è una voce breve con uno **stato**
(`proposta → decisa → chiusa`, oppure `scartata`). Le decisioni misurano la **maturità** del
design; la **completezza** (cosa copre) vive nel cruscotto di [[requisiti]].

> Una decisione **non copre** un requisito: modella un elemento del design (`SOL-x`) che lo copre.
> Il cruscotto in [[requisiti]] passa da lì: `REQ-01 🟢 → [[soluzione#SOL-1]] · [[decisioni#DEC-01]]`.

## Da dove nasce una decisione

Una decisione è la **memoria del perché**: quale strada si è presa, quali si sono scartate, se la
scelta è congelata o ancora aperta. Il ponte fra il *cosa* e il *come* è la [[soluzione]] — le
decisioni le stanno **accanto** e la spiegano. Si innescano in tre modi:

1. **Requirement-driven** — un `REQ`/`VIN` ammette più modi di essere soddisfatto e **impone una
   scelta** (nasce dai requisiti).
2. **Design-driven** — mentre si struttura la [[soluzione]] emerge un **bivio** non dettato da un
   singolo requisito (nasce dal design; può far emergere a ritroso un nuovo `REQ`/`ASS`).
3. **Da una domanda chiusa** — una `DOM` risolta (sezione *Punti aperti* qui sotto) diventa una
   decisione (o un requisito/ipotesi).

In tutti i casi la casa è **solo questo file**. Ogni `DEC` dichiara **dove è adottata**: il `SOL-x`
che ha modellato. Una decisione senza *Adottata in* è una scelta presa e mai riflessa nel design —
si vede a occhio, senza aspettare il [[lint]].

## Punti aperti

Dubbi, cose che non tornano, informazioni da cercare, scelte non ancora mature per una `DEC`.
Li apre chiunque dei due — tu o l'agente, durante ingest o design. Quando si chiudono, l'**Esito**
punta a dove sono confluiti: una `DEC`, un `REQ` o un'`ASS`.

| ID | Domanda | Blocca | Stato | Esito |
|---|---|---|---|---|
| DOM-01 | _(punto che non torna / scelta da fare / info da cercare)_ | _(REQ-… / DEC-…)_ | aperta | _(→ [[decisioni#DEC-…]] / [[requisiti#REQ-…]] / [[requisiti#ASS-…]])_ |
| DOM-02 | | | | |

> **Blocca**: quale `REQ`/`DEC` resta in sospeso finché il punto non si chiude.

## Indice decisioni

| ID | Titolo | Stato | Adottata in |
|---|---|---|---|
| DEC-01 | _(titolo scelta)_ | proposta | [[soluzione#SOL-1]] |

---

## DEC-01 — _(titolo della decisione)_

- **Stato**: proposta _(proposta / decisa / chiusa / scartata)_
- **Contesto**: _(qual è il problema / vincolo che impone una scelta)_
- **Opzioni considerate**: _(A, B, C — pro/contro in una riga)_
- **Scelta**: _(opzione scelta)_
- **Motivazione**: _(perché, in 1-2 righe; fonti con URL se ricerca esterna)_
- **Adottata in**: [[soluzione#SOL-1]] _(l'elemento del design che questa scelta ha modellato)_
- **Conseguenze / rischi**: _(cosa comporta, dipendenze, cosa resta aperto)_
