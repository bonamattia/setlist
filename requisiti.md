---
titolo: "Requisiti, vincoli e ipotesi"
tags: [requisiti, vincoli, ipotesi]
stato: bozza
ultimo_aggiornamento: 2026-09-27
---

# Requisiti, vincoli e ipotesi

Cosa deve fare il progetto e **dentro quali limiti**. È la **checklist** contro cui si valida il
design in [[soluzione]]: qui **non si scrivono soluzioni**, solo obiettivo, requisiti, vincoli e
ipotesi. Fonti: [[setlist-first-ideas]], [[setlist-riorientamento-macroaree]], [[prova-A01-mtg-jamendo-conteggi]].

## Obiettivo e non-obiettivi

**Obiettivo** — Da una richiesta in linguaggio naturale, generare una **scaletta di brani metal e rock
strumentali con un arco di intensità coerente**, come la costruirebbe una band per un concerto. Farlo un
gradino alla volta per **imparare l'AI musicale** toccandone gli strati principali, e misurare dove gli
strumenti esistenti reggono o cedono su questo genere. Pesa di più l'apprendimento del prodotto.

**Non-obiettivi** — cosa resta **fuori**, per scelta:
- niente catalogo commerciale: solo musica a licenza aperta o propria;
- niente mix audio continuo: il sistema decide l'ordine, non produce il mix;
- niente raccomandazione su dati d'ascolto di utenti reali (niente filtraggio collaborativo);
- niente prodotto pubblico: è un progetto di studio e dimostrativo;
- generazione musicale e identificazione (fingerprinting, cover) fuori percorso.

## Cruscotto copertura (vs design)

Legenda: 🟢 coperto · 🟡 parziale (presente ma da completare) · 🔴 gap (assente/insufficiente) ·
⚪ documentale (non nel disegno tecnico).

**Stato attuale: 🟢 0 · 🟡 1 · 🔴 6 · ⚪ 0** — _(ingest del 2026-09-27; primo re-scoring da fare con [[lint]])_

> La copertura vive **solo qui**. La colonna *Copertura* punta all'**elemento della soluzione**
> che soddisfa il requisito e, di seguito, alla decisione che l'ha modellato:
> `REQ-01 🟢 → [[soluzione#SOL-1]] · [[decisioni#DEC-01]]`.
> **Senza un `SOL-x` non si è 🟢**: una decisione presa ma non ancora riflessa nel design non copre.

## Vincoli (valgono su tutto il progetto)

| ID | Vincolo | Origine | Nota |
|---|---|---|---|
| VIN-1 | Solo musica a licenza aperta o dell'utente; nessun catalogo commerciale. | `raw/input/setlist-first-ideas` §7 · scelta | — |
| VIN-2 | Il codice gira in locale sul PC dell'utente (WSL); GPU non obbligatoria. | scelta · [[decisioni#DEC-06]] | Essentia non ha pacchetti per Windows nativo. |
| VIN-3 | Repo pubblico: audio, dataset e modelli mai in git. | scelta · [[decisioni#DEC-05]] | Diritti su brani propri e di terzi. |
| VIN-4 | Modelli Essentia CC BY-NC-SA 4.0: uso non commerciale, non ridistribuibili. | licenza Essentia | — |

## Requisiti

| ID | Requisito | Origine | Copertura |
|---|---|---|---|
| REQ-01 | Da una richiesta in linguaggio naturale, produrre una scaletta ordinata che rispetti la durata richiesta. | `setlist-first-ideas` §1, §3.1 · riorientamento | 🔴 nessun `SOL` |
| REQ-02 | Selezionare i brani per come suonano (dall'audio), non solo dalle etichette. | `setlist-first-ideas` §3.2–3.3 | 🔴 nessun `SOL` |
| REQ-03 | Ordinare i brani secondo l'arco di intensità richiesto, con transizioni fluide di tempo, accordatura e intensità. | `setlist-first-ideas` §3.4 · riorientamento | 🔴 nessun `SOL` · [[decisioni#DEC-02]] |
| REQ-04 | Riconoscere genere e sottogenere di un brano metal o rock strumentale. | riorientamento (step 2) | 🟡 → [[soluzione#SOL-1]] · [[decisioni#DEC-03]] · [[decisioni#DEC-04]] — design in bozza, non ancora eseguito |
| REQ-05 | Misurare l'intensità di un brano nel tempo, non solo come valore unico. | riorientamento (step 3) | 🔴 nessun `SOL` |
| REQ-06 | Distinguere i brani strumentali da quelli cantati. | `prova-A01` (nessun tag affidabile) | 🔴 nessun `SOL` |
| REQ-07 | Spiegare perché ha scelto quei brani e in quell'ordine. | `setlist-first-ideas` §3.5 | 🔴 nessun `SOL` |

## Ipotesi

Ipotesi **di merito** su cui poggia il design (volumi, comportamento di un modello, qualità dei
dati, prestazioni). Non si confermano chiedendo: si **verificano**, con un esperimento o una misura.

| ID | Ipotesi | Perché la assumo | Come la verifico |
|---|---|---|---|
| ASS-01 | Discogs-EffNet riconosce i sottogeneri dei brani metal strumentali di riferimento. | Addestrato su ~3,3M brani con stili Discogs, Sludge e Post-Metal inclusi. | Prova C01: stile atteso nei primi 3 su almeno N brani di riferimento (soglia: [[decisioni#Punti aperti\|DOM-05]]). |
| ASS-02 | I tag di MTG-Jamendo bastano per i generi grossolani (metal, post-rock, hard rock). | A01: 1.435 brani metal, 377 post-rock, 490 hard rock. | Ascolto a campione dei primi 5 artisti per tag; classificatore C02 separato per artista. |
