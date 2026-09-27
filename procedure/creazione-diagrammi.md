---
titolo: "Creazione diagrammi — catalogo e standard"
tags: [procedura, diagrammi, excalidraw, assets]
stato: bozza
ultimo_aggiornamento: 2026-09-25
---

# Creazione diagrammi — catalogo e standard

Procedura che l'agente esegue su **«diagramma»**, **«schema»**, **«crea diagramma»** — e, quando
sai già cosa vuoi, su **«disegna l'architettura»**, **«flusso dati»**, **«vista di rete»**,
**«sequenza»**, **«ciclo di vita»**.

Questo file è un **dispatcher**: sceglie il tipo, fissa lo standard comune e delega ai runbook dei
tipi **generati**. I tipi che si disegnano a mano si esauriscono qui.

> **Regola d'uso**: l'agente **rilegge questo file per intero prima di eseguire**. Il tipo di
> diagramma è una scelta di comunicazione, non di stile: si concorda prima di aprire un file.
>
> Vale il **principio HITL** ([[CLAUDE]] §1): l'agente propone, tu validi. I **punti di
> fermata** di questa procedura sono in fondo.

## 1. Catalogo dei tipi

| Tipo | Risponde a | Quando si usa | Come si produce |
|---|---|---|---|
| **Architettura (HLD)** | com'è fatto l'insieme? | blocchi e confini, zero implementazione | a mano dal template |
| **Flusso dati** | come si muovono i dati? | ingestione, arricchimento, indicizzazione | a mano dal template |
| **Sequenza** | chi chiama chi, e in che ordine? | quando il punto è il **tempo**: fallback, autenticazione, retry | a mano dal template |
| **Deployment / rete** | dove gira, dentro quali confini? | residenza dei dati, tenant, rete chiusa, identità | a mano dal template |
| **Ciclo di vita** | quali stati attraversa una cosa? | stati di un documento, di una pratica, di un job | a mano dal template |

**Un tipo esce da questo file e diventa un runbook a sé quando ha un generatore.** Finché si disegna
a mano, le sue regole stanno qui. Oggi nessun tipo ha un generatore.

Se il tipo non è ovvio dalla richiesta, l'agente **propone** quello che gli sembra giusto con una
riga di motivazione e attende. Puoi sempre derogare al catalogo — chiedendo una vista che non c'è —
purché la deroga sia **dichiarata**, non implicita.

## 2. Due livelli di zoom

| Livello | Per chi | Contenuto |
|---|---|---|
| **Vista d'insieme** | chi legge il case study (recruiter, CTO) — è la vista che va nel [[case-study]] | pochi blocchi, nomi comuni, nessun dettaglio implementativo |
| **Vista di dettaglio** | chi implementa | un flusso o un componente alla volta, con le scelte tecniche |

Sono due livelli, non tre: un progetto si ferma prima di arrivare al dettaglio interno di un
componente. Se un giorno servisse un terzo livello, si aggiunge — non si assume in anticipo.

## 3. Quando una vista è obbligatoria

Certe viste non sono una scelta stilistica: **in presenza di certi vincoli, se mancano manca un
pezzo del progetto.** L'agente lo verifica leggendo [[requisiti]].

| Se in `requisiti` c'è… | …serve |
|---|---|
| un `VIN` su residenza dei dati, tenant, rete chiusa o identità | **deployment / rete** |
| un `REQ` su trattamento di dati personali o riservati | **flusso dati**, coi flussi sensibili marcati |
| un `REQ` su tempi di risposta, fallback o comportamento in errore | **sequenza** |

## 4. Standard comune (vale per tutti i tipi)

1. **Formato & posizione** — file `.excalidraw` in `assets/`, **uno per diagramma**. L'editabile è il
   `.excalidraw`; i **PNG di consegna** non stanno qui.
2. **Naming** — kebab-case descrittivo. Se il diagramma illustra una scelta, suffissa con l'ID:
   `pipeline-ingest-DEC03.excalidraw`. La vista d'insieme si chiama `architettura-hld.excalidraw`.
3. **Titolo sul canvas** — primo elemento, un testo con `"id": "title"`, `fontFamily: 2`.
4. **Stile** — `fontFamily: 2`, `roughness: 1`, stroke neutro `#1e1e1e` per la struttura.
   La **palette è semantica e fissa** (§6): un colore ha lo stesso significato in tutti i diagrammi
   del vault, non si sceglie volta per volta. Se in un diagramma compaiono colori, la legenda va sul
   canvas — ma solo per i significati effettivamente usati.
5. **Contenuto** — pochi box, sottotitoli brevi. Il dettaglio vive nei documenti. Etichetta gli
   elementi **come in** [[soluzione]]: stessi nomi, stessi `SOL-x`.
6. **Collegamento** — embedda con `![[assets/<nome>.excalidraw]]` nel documento pertinente e collega
   il diagramma al `REQ`/`SOL`/`DEC` che illustra.
7. **Ciclo di vita** — i diagrammi si **rigenerano a decisione chiusa**: finché la `DEC` è aperta il
   diagramma è bozza; quando è `chiusa`, si allinea alla scelta finale.

## 5. Passi (in ordine)

1. **Scegli il tipo e il livello** — dal catalogo (§1, §2); verifica se un vincolo ne rende una
   obbligatoria (§3). Se non è ovvio, proponi e attendi.
2. Se il tipo è **generato**, esegui il suo runbook e fermati qui.
3. **Duplica il template** `assets/_template.excalidraw` col nome giusto.
4. Sostituisci titolo ed elementi; applica lo stile e la **palette semantica** (§6), con la legenda
   dei soli significati usati.
5. **Verifica** prima di consegnare (§7), poi **embedda** nel documento e collega `REQ`/`SOL`/`DEC`.
6. Appendi a [[log]]: `## [YYYY-MM-DD] design | diagramma <nome> (<tipo>) creato/aggiornato`.

## 6. Palette semantica (fissa)

Un colore **significa** qualcosa, e significa la stessa cosa ovunque. Non si sceglie una palette per
diagramma: si prende da qui. È la differenza fra un vault che ha uno stile e sei disegni scollegati.

| Significato | Stroke | Fill |
|---|---|---|
| Componente **nostro**, dentro il perimetro | `#1971c2` blu | `#e7f5ff` |
| **Dato / archivio** (storage, indice, DB) | `#ae3ec9` viola | `#f8f0fc` |
| **Esterno**: servizio di terzi (API, SaaS, modello hosted) | `#868e96` grigio | `#f1f3f5` |
| **Confine**: tenant, rete chiusa, zona pubblica | `#0c8599` petrolio | trasparente, tratteggiato |
| **Dato sensibile** (personale, riservato) | `#e8590c` arancio | `#fff4e6` |
| **Gap / rischio dichiarato** | `#e03131` rosso | `#ffc9c9` |
| **Coperto / validato** | `#2f9e44` verde | `#ebfbee` |

Due regole: il **grigio non è decorativo**, dice «questo non lo facciamo noi»; e l'**arancio non si
usa per enfasi**, marca solo i dati sensibili — perché è ciò che qualcuno cercherà con l'occhio in
una revisione GDPR.

## 7. Verifiche prima di consegnare

Poche, perché lo standard previene più di quanto serva controllare — le sovrapposizioni non si
verificano se gli elementi stanno su una griglia. Restano quelle che la griglia non copre:

| Controllo | Se fallisce |
|---|---|
| Ogni etichetta **sta dentro** il suo elemento | il testo esce dal box: accorcia l'etichetta, non allargare il box |
| La **legenda** elenca tutti e soli i significati usati | colori senza legenda, o legenda con voci assenti dal disegno |
| Ogni elemento ha il **nome che ha in** [[soluzione]] | il diagramma e il testo raccontano due cose diverse |
| Nessun colore **fuori palette** (§6) | un colore che non significa niente |

⚠️ Se un elemento non ci sta, **il problema è il contenuto, non il canvas**: un diagramma con troppi
box non si allarga, si spezza in due viste (§2).

## Punti di fermata (HITL)

Applicazione del principio in [[CLAUDE]] §1 a questa procedura.

- 🛑 **Tipo e livello** — sono una scelta di comunicazione: si concordano prima di aprire un file,
  e una deroga al catalogo va dichiarata.
- 🛑 **Revisione visiva** — un diagramma è un artefatto che va **guardato**: dopo averlo generato
  l'agente ti chiede di aprirlo in Obsidian e attende l'ok prima di considerarlo la versione corrente.
- 🔧 **Fix sicuri**: naming secondo lo standard, stile e palette dal template, embed, riga di [[log]].

## Cosa NON fa

- Non mette nel diagramma il dettaglio implementativo che vive nei documenti.
- Non genera PNG come sorgente (l'editabile è il `.excalidraw`; l'export è per il [[case-study]]).
- Non crea diagrammi scollegati: ognuno è linkato da un documento e da un `REQ`/`SOL`/`DEC`.
- Non sceglie il tipo al posto tuo quando la richiesta è ambigua: propone.
