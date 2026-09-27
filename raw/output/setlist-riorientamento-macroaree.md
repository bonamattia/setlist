# Setlist — riorientamento e macroaree

**Data:** 2026-09-27 · **Origine:** discussione con l'agente, macroaree validate da Mattia
**Aggiorna:** [[setlist-first-ideas]] (che resta invariato)

## Cosa cambia rispetto alle prime idee

- **Scopo:** capire come funziona l'AI nella musica toccandola con mano. Il portfolio è una conseguenza, non il motore.
- **Dominio:** musica **metal e rock strumentale** (post-metal, sludge, post-rock, prog…), non un catalogo generico.
- **Metafora:** da "DJ set" a **scaletta live**, come la costruisce una band per un concerto.
- **Transizioni:** conta la continuità di **accordatura**, tempo e intensità, non il mixaggio armonico stile Camelot.
- **Modo di lavorare:** si progetta e si avanza insieme. Ogni step è una prova breve (domanda → prova → cosa ho visto) che riempie una macroarea.

## Obiettivo (proposta, da validare nell'ingest)

Costruire un sistema che, da una richiesta in linguaggio naturale, genera una scaletta di brani metal e rock strumentali con un arco di intensità coerente. Farlo un gradino alla volta, per imparare l'AI musicale toccandone gli strati principali e misurare dove gli strumenti esistenti reggono o cedono su questo genere. Due facce: **prodotto** (la scaletta funziona) e **apprendimento** (capisco il dominio, fallimenti compresi). Pesa di più la seconda.

## Macroaree

| # | Macroarea | Cosa contiene | Ruolo in Setlist | Decisione |
|---|---|---|---|---|
| A | Dati e corpus | dataset, licenze, annotazioni proprie | tutto poggia qui | trasversale |
| B | Rappresentazione audio | spettrogrammi, feature, embedding pre-addestrati | fondamenta | trasversale |
| C | Analisi musicale (MIR) | genere/sottogenere, tempo, accordatura, struttura, intensità | capire ogni brano | cuore |
| D | Separazione e trascrizione | stem, audio → MIDI | strumento al servizio di C | stem sì · trascrizione facoltativa |
| E | Ricerca e sequenza | ricerca per suono, audio-testo, ordinamento con vincoli | selezione e arco | cuore |
| F | Linguaggio (LLM) | dalla richiesta ai vincoli | interfaccia | minima |
| G | Valutazione | verità di riferimento, metriche, ascolto | dire quanto funziona | trasversale, in ogni step |
| — | Generazione | MusicGen, Stable Audio | nessuno | curiosità fuori percorso |
| — | Identificazione | fingerprinting, cover, rilevamento AI | nessuno | fuori |
| — | Raccomandazione collaborativa | dati d'ascolto utenti | nessun dato | fuori, limite dichiarato |

## Sequenza degli step

0. **Corpus** — quanto metal/rock strumentale c'è nei dataset + brani di riferimento propri (A)
1. **Guarda e ascolta** — spettrogrammi, tempo, accordatura sui brani propri (B, C)
2. **Genere e sottogenere** — pipeline base, matrice di confusione (B, C, G)
3. **Struttura e intensità, con gli stem** — prima su DEAM, poi sui brani annotati a mano (C, D, G)
4. **Ricerca per suono** — audio-testo su corpus metal/rock (E, G)
5. **Ordinamento** — per intensità, tempo, accordatura (E, G)
6. **Richiesta in linguaggio naturale** (F)
