# Prova A-01 — MTG-Jamendo: quanto metal e rock c'è davvero

**Data:** 2026-09-27 · **Macroarea:** A (Dati e corpus) · **Tipo:** risultato di esperimento (conteggio sui metadati)
**Fonte dati:** `data/raw_30s_cleantags.tsv` del repo ufficiale MTG/mtg-jamendo-dataset (55.701 brani, 595 tag). Nessun audio scaricato.

## Domanda

Il dataset contiene abbastanza metal e rock strumentale per lavorarci?

## Numeri (brani · artisti · ore)

| Sottoinsieme (tag) | Brani | Artisti | Ore |
|---|---|---|---|
| `genre---rock` | 6.865 | 1.019 | 441,9 |
| `genre---metal` | 1.435 | 232 | 98,9 |
| metal + hardrock + postrock + progressive + grunge | 3.413 | 581 | 246,9 |
| `genre---instrumentalrock` | 598 | 151 | 40,2 |
| `genre---postrock` | 377 | 79 | 28,8 |
| `genre---heavymetal` | 222 | — | — |
| `genre---thrashmetal` · `deathmetal` · `blackmetal` | 113 · 81 · 22 | — | — |
| `genre---doom` | 8 | — | — |
| sludge, post-metal, djent, stoner | 0 (tag assenti) | — | — |
| `mood/theme---heavy` · `mood/theme---dark` (tutti i generi) | 156 · 1.202 | — | — |

Nei sottoinsiemi metal, post-rock e instrumental rock i 5 artisti principali coprono circa il 23–24% dei brani.

## Cosa ho visto

- **Il volume per iniziare c'è:** circa 100 ore di metal e 250 della famiglia rock "pesante".
- **Non c'è un tag "strumentale" affidabile.** `instrument---voice` compare su soli 1.604 brani in tutto il dataset: i tag degli strumenti sono sparsi, quindi l'assenza della voce non vuol dire che il brano sia strumentale. Unico appiglio: `instrumentalrock` (598 brani). Capire se un brano è strumentale va **ricavato dall'audio** (rilevamento della voce): è un task in più, in C.
- **I sottogeneri che interessano di più non esistono come etichetta:** doom 8 brani, sludge e post-metal zero. Il sottogenere fine non si può imparare da questi tag; al massimo metal / post-rock / hard rock / prog.
- **Molti brani per artista (~6):** la divisione train/test va fatta per artista, altrimenti il modello riconosce l'artista e non il genere. Il dataset fornisce già split per artista.

## Domande aperte

- FMA ha più sottogeneri metal? Da contare allo stesso modo.
- Quanto è affidabile un rilevatore voce/strumentale su chitarre distorte?
