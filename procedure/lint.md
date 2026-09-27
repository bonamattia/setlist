---
titolo: "Lint — runbook di controllo (copertura + coerenza)"
tags: [procedura, lint, validazione, copertura, cruscotto]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Lint — runbook

È l'operazione *lint* del pattern LLM-wiki, resa concreta. Un solo runbook, **due modalità**:

| Trigger | Modalità | Esegue |
|---|---|---|
| **«valida»** · **«valida copertura»** | **rapida** — "è tutto coperto?" | solo la **Parte A** |
| **«lint»** · **«riallineamento»** · **«aggiorna»** | **completa** — "il vault è coerente?" | **Parte A + Parte B** |

La modalità rapida è **parte del design** ([[creazione-soluzione]]): gira a ogni giro di
costruzione. La completa è periodica.

> **Regola d'uso**: l'agente **rilegge questo file per intero prima di eseguire** e segue i passi
> nell'ordine dato. Qui **non si progetta** e **non si tocca `raw/`**: si misura e si segnala.
>
> Vale il **principio HITL** ([[CLAUDE]] §1): l'agente propone, tu validi. I **punti di
> fermata** di questa procedura sono in fondo.

## Parte A — Copertura

È la **casa unica** della logica di copertura.

1. **Leggi** [[requisiti]] (`REQ`/`VIN`/`ASS`) e la [[soluzione]] + [[decisioni]] correnti.

2. **Valuta ogni requisito** — Per ciascun `REQ`/`VIN`: **quale `SOL-x` lo soddisfa?** Assegna lo
   stato e linka l'elemento del design, poi la decisione che l'ha modellato:
   - 🟢 **coperto** → `REQ-x 🟢 → [[soluzione#SOL-y]] · [[decisioni#DEC-z]]`
   - se esiste una `DEC` ma **nessun `SOL-x`**, non è 🟢: è 🔴 o 🟡 (scelta non ancora nel design)
   - 🟡 **parziale** (presente ma incompleto)
   - 🔴 **gap** (assente o insufficiente)
   - ⚪ **documentale** (non nel disegno tecnico)

3. **Concordanza** — Cruscotto e tabella `SOL-x` devono **concordare** sulla stessa terna
   `REQ → SOL → DEC`. *(le terne discordanti si segnalano)*

4. **Conteggi** — Aggiorna i conteggi del cruscotto in [[requisiti]] (🟢/🟡/🔴/⚪).
   *(fix automatico, a stati validati)*

5. **Esito copertura** — Elenca i 🔴 **gap** e i 🟡 **parziali**, dicendo per ognuno **cosa manca**
   nel design, e i ⚪ documentali. In modalità **rapida** qui si passa direttamente a *Report + log*.

## Parte B — Coerenza (solo modalità completa)

6. **Ingest pendenti** — Controlla `raw/`: ci sono fonti non ancora compilate nei documenti di
   lavoro? Elencale come da lavorare (non ingerirle in automatico senza conferma).

7. **Coerenza dei link** — Wikilink rotti, ancore `#REQ-…` / `#DEC-…` inesistenti, pagine orfane
   (senza link in entrata). *(segnala; correggi i refusi evidenti)*

8. **Anti-duplicazione / ownership** — Nessun requisito riscritto in [[soluzione]]; cruscotto
   **solo** in [[requisiti]]; decisioni **solo** in [[decisioni]]. Se trovi contenuto fuori casa,
   segnalalo con la casa corretta. Controlla anche i **budget di forma** ([[CLAUDE]] §4): un
   elemento che sfora è quasi sempre contenuto di un altro tipo finito nella casa sbagliata —
   segnala elemento, tetto e casa probabile. *(segnala)*

9. **Stati decisione** — `DEC` ferme in `proposta` da troppo tempo; **`DEC` senza *Adottata in***
   (scelta presa e mai riflessa nel design); `DEC` che punta a un `SOL-x` inesistente. *(segnala)*

10. **Utilità del design** — **`SOL-x` senza requisiti coperti** nella tabella di [[soluzione]]: o
    manca un requisito, o stiamo costruendo qualcosa che nessuno ha chiesto. *(segnala)*

11. **Domande & ipotesi** — `DOM` aperte che bloccano un `REQ`/`DEC`; `DOM` chiuse non ancora
    trasformate in `REQ`/`ASS`/`DEC`; **`DOM` senza `Blocca` compilato**; `ASS` senza
    *Come la verifico* o con la verifica ancora da fare. *(segnala)*

12. **Igiene frontmatter** — `ultimo_aggiornamento` non aggiornato dopo modifiche; `stato`
    incoerente (`bozza`/`in-revisione`/`validato`). *(fix automatico delle date)*

13. **Case study allineato** — Se esiste [[case-study]]: una fonte in `deriva_da:` ha
    `ultimo_aggiornamento` **più recente** di quello registrato → il case study è rimasto indietro.
    *(segnala, con le sezioni probabilmente toccate)*

## Report + log

Chiudi sempre con un **report sintetico**:
- ✅ **A posto**: cosa è coerente.
- ⚠️ **Da sistemare**: elenco puntato, ognuno con il file e l'azione suggerita (gap e parziali
  compresi).
- 🔧 **Fix applicati**: cosa hai corretto in automatico.

Poi appendi a [[log]] **una** riga:
- rapida: `## [YYYY-MM-DD] lint | rapida: 🟢n · 🟡n · 🔴n · ⚪n`
- completa: `## [YYYY-MM-DD] lint | completa: 🟢n · 🟡n · 🔴n · ⚪n · <n fix, n segnalazioni>`

## Punti di fermata (HITL)

Applicazione del principio in [[CLAUDE]] §1 a questa procedura. Il lint è un **controllo**: vede
molto e corregge poco. Uno stato di copertura è un **giudizio**, non una misura: si mostra prima di
scriverlo.

- 🛑 **Ogni assegnazione di stato** — che sia un passaggio (🔴→🟢) o un ⚪ documentale: presenta la
  riga col `SOL-x` che copre e la `DEC` che l'ha modellato, poi si scrive nel cruscotto. Dichiarare
  un requisito fuori dal disegno tecnico è una scelta di perimetro, non un'osservazione.
- ⚖️ **In dubbio vince il più severo** — 🟡 invece di 🟢, 🔴 invece di 🟡 — e lo si segnala nel report.
  Non si arrotonda verso il verde.
- 🛑 **Ogni voce del report ⚠️** — le segnalazioni sono materiale per te: non si risolvono nello
  stesso giro, **nemmeno quelle che l'agente saprebbe sistemare**.
- 🔧 **Fix sicuri**: conteggi del cruscotto a stati validati, `ultimo_aggiornamento`, refusi evidenti
  nei wikilink, riga di [[log]].

## Cosa NON fa

- Non **inventa** coperture: se una cosa non è nel design è 🔴, anche se una `DEC` la prevede.
- Non **chiude** gap né decisioni e non progetta: li **segnala** (il design è [[creazione-soluzione]]).
- Non ingerisce fonti nuove senza conferma (è un controllo, non un ingest).
- Non tocca `raw/` (immutabile).
