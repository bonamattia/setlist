---
titolo: "Soluzione — design end-to-end"
tags: [soluzione, design, architettura]
stato: bozza
ultimo_aggiornamento: 2026-09-27
---

# Soluzione — design end-to-end

Qui vive il **come**. Due livelli di lettura:
- **panoramica** — schema d'insieme, componenti, flussi: leggibile da chiunque, è la base del
  case study;
- **dettaglio tecnico** — stack, interfacce, logica, limiti: **solo** per i `SOL-x` in cui una
  scelta lo merita.

Per ogni scelta c'è un riferimento a [[decisioni]] con una riga di motivazione.

> Regola anti-duplicazione: qui **non si riscrivono i requisiti** né si duplica il cruscotto —
> si rimanda a [[requisiti]]. Le decisioni con motivazione stanno in [[decisioni]].

## Schema d'insieme

_(diagramma end-to-end da fare quando esistono più `SOL-x`; per ora il design copre solo il riconoscimento del genere.)_

Sintesi in una riga: da una richiesta testuale a una scaletta ordinata, passando per analisi dei brani (genere, intensità), ricerca per suono e ordinamento con vincoli — oggi progettato solo il primo mattone, il genere.

## Componenti e flussi (`SOL-x`)

Gli elementi del design sono ciò che **copre** i requisiti: il cruscotto in [[requisiti]] punta qui.
Numerazione unica `SOL-x` per componenti e flussi — al cruscotto interessa cosa copre, non se sia
una scatola o una sequenza.

| ID | Elemento | Tipo | Ruolo | Requisiti coperti | Decisione |
|---|---|---|---|---|---|
| SOL-1 | Riconoscimento genere | flusso | Assegna a ogni brano i sottogeneri Discogs, per finestra e sul brano intero | [[requisiti#Requisiti\|REQ-04]] | [[decisioni#DEC-03]] · [[decisioni#DEC-04]] |

Un `SOL-x` senza **Requisiti coperti** è un segnale: o manca un requisito, o stiamo costruendo
qualcosa che nessuno ha chiesto.

### SOL-1 · Riconoscimento genere

1. Carica il brano in mono a 16 kHz.
2. Estrattore EffNet → un embedding per finestra (salvati per riuso).
3. Testa genre400 → 400 probabilità per finestra.
4. Media sul brano → primi 5 stili (csv).
5. Mappa di calore dei 6–8 stili principali nel tempo, grezza e lisciata (png).
6. Confronto con l'annotazione dell'utente: primo posto, primi tre, errori.

Fonte del disegno: [[prova-C01-discogs-effnet]].

## Dettaglio tecnico

Un blocco per ogni `SOL-x` con scelte **non banali** — non per tutti. Campi fissi, max 3 righe
l'uno ([[CLAUDE]] §4): ciò che sfora va in una pagina di approfondimento linkata.

### SOL-1 · Riconoscimento genere — dettaglio

- **Stack**: Essentia (`essentia-tensorflow`) in WSL; modelli `discogs-effnet-bs64-1` e `genre_discogs400-discogs-effnet-1` (https://essentia.upf.edu/models.html).
- **Interfacce**: in: file audio in `data/riferimento/` + annotazione (sottogenere atteso, secondo accettabile). Out: `C01-predizioni.csv`, `C01-<brano>-stili-nel-tempo.png`, embedding (1.280 valori per finestra).
- **Logica chiave**: uscite sigmoide indipendenti → si leggono i primi stili, non un vincitore; media sul brano più curva nel tempo; lisciatura con media mobile su poche finestre.
- **Limiti noti**: PR-AUC dichiarata 0,21; etichette Discogs assegnate all'uscita discografica, non al brano; durata e sovrapposizione delle finestre (~1,5 s) da verificare.
- **Codice**: `code/prove/c01_discogs_effnet.py` (da creare).

## Valutazione

Come si misura che la soluzione **funziona**. È qui che si verificano le ipotesi di
[[requisiti#Ipotesi]]: ogni `ASS-x` con un *Come la verifico* trova qui metrica e risultato.

| Cosa si misura | Metrica | Dataset / metodo | Soglia | Risultato | Verifica |
|---|---|---|---|---|---|
| Riconoscimento del sottogenere | stile atteso nei primi 3 (e al primo posto) | 8–10 brani di riferimento annotati dall'utente | da fissare ([[decisioni#Punti aperti\|DOM-05]]) | da misurare | [[requisiti#Ipotesi\|ASS-01]] |

## Scelte tecniche

Ogni scelta rimanda alla decisione che la motiva (con stato e alternative) in [[decisioni]].

- modello per il genere → riferimento: Discogs-EffNet + genre_discogs400 · vedi [[decisioni#DEC-03]]
- lettura dell'output → riferimento: mappa di calore nel tempo + media · vedi [[decisioni#DEC-04]]
- ambiente di esecuzione → riferimento: Essentia in WSL sul PC dell'utente · vedi [[decisioni#DEC-06]]

## Punti aperti

Dubbi che toccano il design e non sono ancora chiusi: vedi [[decisioni#Punti aperti]].
