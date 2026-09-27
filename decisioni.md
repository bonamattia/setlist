---
titolo: "Decisioni di design (ADR-lite)"
tags: [decisioni, adr]
stato: bozza
ultimo_aggiornamento: 2026-09-27
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
| DOM-01 | Quali 8–10 brani di riferimento per C01 (strumentali, sottogenere noto; idealmente sludge e post-metal)? | [[soluzione#SOL-1]] · [[requisiti#Ipotesi\|ASS-01]] | aperta | — |
| DOM-02 | Brani interi o solo un estratto (es. i primi 2 minuti)? | [[soluzione#SOL-1]] | aperta | — |
| DOM-03 | Soglia minima di probabilità sotto cui dire «il modello non sa»? | [[soluzione#SOL-1]] | aperta | — |
| DOM-04 | Dove tenere gli embedding: `data/` fuori da git o piccoli nella cartella della prova? | [[soluzione#SOL-1]] | aperta | — |
| DOM-05 | Soglia di successo di ASS-01: su quanti brani su 10 lo stile atteso deve stare nei primi 3? | [[requisiti#Ipotesi\|ASS-01]] | aperta | — |
| DOM-06 | FMA ha più metal strumentale e più sottogeneri di MTG-Jamendo? | [[requisiti#Ipotesi\|ASS-02]] | aperta | — |
| DOM-07 | Il rilevatore voce/strumentale di Essentia regge su chitarre distorte? | [[requisiti#Requisiti\|REQ-06]] | aperta | — |

> **Blocca**: quale `REQ`/`DEC` resta in sospeso finché il punto non si chiude.

## Indice decisioni

| ID | Titolo | Stato | Adottata in |
|---|---|---|---|
| DEC-01 | Dominio: metal e rock strumentale | decisa | [[requisiti#Obiettivo e non-obiettivi]] (nessun `SOL` diretto) |
| DEC-02 | Scaletta live, non DJ set | decisa | — (da adottare nel design di REQ-03) |
| DEC-03 | Genere: prima modello pre-addestrato, poi classificatore proprio | decisa | [[soluzione#SOL-1]] |
| DEC-04 | Output del genere come mappa di calore nel tempo | decisa | [[soluzione#SOL-1]] |
| DEC-05 | Il vault è il repo pubblico | decisa | `CLAUDE.md` §2–§4 · struttura del repo |
| DEC-06 | Il codice gira sul PC dell'utente (WSL) | decisa | `CLAUDE.md` §2 · [[requisiti#Vincoli (valgono su tutto il progetto)\|VIN-2]] |

---

## DEC-01 — Dominio: metal e rock strumentale

- **Stato**: decisa
- **Contesto**: le prime idee puntavano a un catalogo generico; serve un dominio in cui l'utente ha competenza e che metta alla prova gli strumenti.
- **Opzioni considerate**: A) catalogo generico (più dati, meno distintivo); B) metal e rock strumentale (competenza propria, strumenti meno collaudati).
- **Scelta**: B.
- **Motivazione**: l'utente sa la risposta giusta sui propri brani; i limiti dei modelli su questo genere sono essi stessi un risultato.
- **Adottata in**: obiettivo in [[requisiti]]; nessun `SOL` diretto.
- **Conseguenze / rischi**: dati etichettati scarsi (A01: sludge e post-metal assenti in MTG-Jamendo); servono brani di riferimento propri.

## DEC-02 — Scaletta live, non DJ set

- **Stato**: decisa
- **Contesto**: le prime idee usavano le regole del DJ (compatibilità di tonalità, Camelot), pensate per l'elettronica tonale.
- **Opzioni considerate**: A) DJ set con mixaggio armonico; B) scaletta live con transizioni per accordatura, tempo e intensità.
- **Scelta**: B.
- **Motivazione**: nel metal la continuità passa da accordatura e intensità; la tonalità automatica è poco affidabile con la distorsione.
- **Adottata in**: — (da adottare quando si progetta REQ-03).
- **Conseguenze / rischi**: servono stima dell'accordatura e misura d'intensità (REQ-05), meno standard di BPM e tonalità.

## DEC-03 — Genere: prima modello pre-addestrato, poi classificatore proprio

- **Stato**: decisa
- **Contesto**: REQ-04 ammette più strade: modello pronto, zero-shot audio-testo (CLAP), classificatore su embedding, CNN da zero.
- **Opzioni considerate**: A) Discogs-EffNet così com'è (400 stili, sludge incluso); B) CLAP zero-shot (debole sulle nicchie); C) classificatore su embedding (serve dati); D) CNN da zero (didattica, peggiore).
- **Scelta**: A per primo (C01), poi C e D come prove di apprendimento; B spostato alla ricerca per suono (REQ-02).
- **Motivazione**: capire e usare bene un modello solido prima di costruirne uno; A ha i sottogeneri che MTG-Jamendo non ha. https://essentia.upf.edu/models.html
- **Adottata in**: [[soluzione#SOL-1]]
- **Conseguenze / rischi**: dipendenza da un modello CC BY-NC-SA (VIN-4); PR-AUC dichiarata 0,21, stili rari poco precisi.

## DEC-04 — Output del genere come mappa di calore nel tempo

- **Stato**: decisa
- **Contesto**: il modello dà 400 probabilità indipendenti (sigmoide) per finestra di circa 1,5 s.
- **Opzioni considerate**: A) stile vincente per finestra; B) mappa di calore dei 6–8 stili principali nel tempo, più la media sul brano.
- **Scelta**: B, in versione grezza e lisciata.
- **Motivazione**: A salta tra stili vicini (sludge ↔ doom) e nasconde la confidenza; B mostra convivenza e cambi (intro pulite, picchi).
- **Adottata in**: [[soluzione#SOL-1]]
- **Conseguenze / rischi**: durata e sovrapposizione reali delle finestre da verificare al primo giro.

## DEC-05 — Il vault è il repo pubblico

- **Stato**: decisa
- **Contesto**: codice e design rischiano di divergere se vivono in posti diversi (nota N-04).
- **Opzioni considerate**: A) repo separato dal vault; B) vault come radice del repo, con `code/`; pubblico o privato.
- **Scelta**: B, pubblico (https://github.com/bonamattia/setlist).
- **Motivazione**: un solo posto, tracciabilità prova ↔ codice ↔ risultato; il metodo diventa visibile.
- **Adottata in**: `CLAUDE.md` §2–§4 · struttura del repo.
- **Conseguenze / rischi**: `raw/input` e il log diventano pubblici; audio e modelli esclusi da git (VIN-3).

## DEC-06 — Il codice gira sul PC dell'utente (WSL)

- **Stato**: decisa
- **Contesto**: Essentia funziona solo su Linux e macOS; nel cloud dell'agente i modelli non si scaricano.
- **Opzioni considerate**: A) ambiente cloud dell'agente (copia di audio e modelli a ogni giro); B) PC dell'utente in WSL, con Claude Code in VS Code.
- **Scelta**: B.
- **Motivazione**: tutto resta locale, nessuna copia di audio; l'utente lancia e vede i risultati direttamente.
- **Adottata in**: `CLAUDE.md` §2 · VIN-2.
- **Conseguenze / rischi**: prestazioni legate al PC; WSL e Python da preparare.
