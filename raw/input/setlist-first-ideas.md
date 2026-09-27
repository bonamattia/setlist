# Setlist

*From natural language to DJ-sequenced playlists with audio embeddings and LLM agents*

**Versione:** 0.1 — documento funzionale
**Stato:** idea definita, design tecnico da fare

---

## 1. L'idea in breve

Setlist è un sistema che riceve una richiesta musicale scritta in linguaggio naturale e restituisce una playlist già ordinata, come la costruirebbe un DJ.

Esempio di richiesta:

> "30 minuti di brani strumentali cupi, che partono lenti e crescono di intensità."

Il sistema non si limita a trovare brani "simili" alla descrizione. Interpreta la richiesta, ne ricava vincoli concreti (durata, mood, tempo, andamento dell'energia), seleziona i brani più adatti ascoltandone il contenuto audio e li mette in una sequenza con un arco coerente, curando le transizioni tra un brano e l'altro.

Il risultato è una **setlist**: una scaletta con un inizio, uno sviluppo e una fine, non un elenco di brani affini.

---

## 2. Perché questo progetto

### 2.1 Obiettivo di carriera

L'obiettivo è spostarsi verso aziende che applicano l'AI alla musica: piattaforme di streaming come Spotify e realtà del music tech europeo, con particolare attenzione all'ecosistema di Barcellona e Valencia.

Il profilo attuale copre bene la parte GenAI (agenti LLM, RAG, orchestrazione), che queste aziende usano già per funzionalità come DJ virtuali, playlist generate da prompt e ricerca conversazionale. Mancano però le competenze storiche su cui il settore è costruito: **sistemi di raccomandazione** e **audio machine learning**. Setlist serve a colmare questo gap in modo dimostrabile.

### 2.2 Cosa deve dimostrare

A chi valuta il portfolio, il progetto deve comunicare quattro cose:

1. **Interesse reale per il dominio.** Un progetto musicale segnala direzione, non solo competenza generica.
2. **Capacità di lavorare con l'audio**, non solo con testo e metadati.
3. **Rigore nella valutazione.** Nel mondo consumer un modello vale quanto le metriche con cui lo si misura.
4. **Sensibilità musicale.** Il sequencing armonico e la gestione dell'energia richiedono di conoscere la musica, non solo i dati. È il fattore che distingue il progetto da un generico "AI playlist generator".

### 2.3 Perché proprio così

- **Riusa ciò che già si sa fare**, cioè agenti e retrieval, come punto d'appoggio. Non si parte da zero.
- **Aggiunge ciò che manca** (audio, raccomandazione, valutazione) dentro un unico caso d'uso concreto, invece di tre esercizi scollegati.
- **Ha una demo facile da capire.** Chiunque può scrivere una richiesta e ascoltare il risultato.
- **Gira in locale**, senza costi di API, su una GPU consumer.
- **Usa un dataset nato nel music tech di Barcellona** (MTG-Jamendo, del Music Technology Group della Universitat Pompeu Fabra), un dettaglio riconoscibile per i possibili interlocutori in Spagna.

---

## 3. Cosa fa il sistema (livello funzionale)

### 3.1 Comprende la richiesta

L'utente descrive ciò che vuole con parole proprie. Il sistema scompone la richiesta in due parti:

- **una parte descrittiva**, cioè l'atmosfera, il genere, gli strumenti, il carattere ("cupi", "strumentali", "malinconico ma con groove");
- **una parte strutturale**, cioè i vincoli misurabili: durata totale, intervallo di tempo (BPM), andamento dell'energia nel corso della playlist (costante, crescente, a onda, in calo).

### 3.2 Conosce il catalogo

Ogni brano del catalogo viene analizzato una volta sola, a partire dall'audio, per ricavarne:

- una **rappresentazione del suono** confrontabile con una descrizione testuale;
- alcune **caratteristiche musicali** misurabili: tempo, tonalità, livello di energia.

In questo modo il sistema può selezionare i brani per come *suonano*, non solo per come sono stati etichettati.

### 3.3 Seleziona i candidati

Il sistema cerca nel catalogo i brani che meglio corrispondono alla descrizione e scarta quelli che violano i vincoli strutturali. Il risultato è un insieme di candidati più ampio della playlist finale.

### 3.4 Costruisce la sequenza

Dai candidati, il sistema sceglie e ordina i brani in modo che:

- la durata totale rispetti la richiesta;
- l'energia segua l'andamento richiesto;
- i passaggi tra brani consecutivi siano fluidi dal punto di vista del **tempo** (niente salti bruschi di BPM);
- i passaggi siano compatibili dal punto di vista **armonico**, secondo le regole usate dai DJ per il mixaggio tra tonalità.

### 3.5 Spiega le proprie scelte

Per ogni playlist il sistema può indicare perché ha scelto quei brani e perché in quell'ordine. Questo rende il risultato verificabile e aiuta a capire dove sbaglia.

### 3.6 Estensione opzionale: impara dal feedback

L'utente può reagire ai brani proposti ("più così", "meno così"). Il sistema ricalibra la selezione di conseguenza, introducendo una forma semplice di raccomandazione interattiva.

---

## 4. Come si valuta

La valutazione è una parte centrale del progetto, non un'appendice.

- **Pertinenza della selezione.** I brani del dataset hanno tag di genere, mood e strumenti. Si possono usare come riferimento per misurare quanto i brani scelti corrispondano davvero alla richiesta.
- **Qualità della sequenza.** Si può misurare quanto l'ordine rispetti la curva di energia richiesta e quanto siano fluide le transizioni di tempo e tonalità, confrontandolo con un ordine casuale.
- **Limiti noti.** I modelli audio-testo funzionano meglio su generi diffusi e mood generici, peggio sulle nicchie. Documentare dove e perché il sistema fallisce fa parte del risultato.

---

## 5. Aree di studio

Questa è la parte che rende il progetto utile oltre il portfolio. Ogni area è collegata a una funzione concreta del sistema.

### 5.1 Music Information Retrieval e audio ML — *priorità alta*

**Dove entra:** analisi del catalogo (3.2) e selezione per contenuto audio (3.3).

**Cosa studiare:**
- come si rappresenta l'audio per il machine learning (spettrogrammi, rappresentazioni percettive);
- embedding audio e modelli che collegano audio e linguaggio;
- estrazione di caratteristiche musicali: tempo, tonalità, energia;
- i task classici del MIR: tagging, riconoscimento di accordi, beat tracking, separazione delle sorgenti.

**Perché è importante:** è la competenza che distingue un ML engineer "generico" da uno di dominio musicale, ed è quella che oggi manca di più al profilo.

### 5.2 Sistemi di raccomandazione — *priorità alta*

**Dove entra:** selezione dei candidati (3.3), costruzione della sequenza (3.4), feedback (3.6).

**Cosa studiare:**
- l'architettura a due stadi, prima il recupero dei candidati e poi il loro ordinamento;
- filtraggio collaborativo e basato sul contenuto, e quando usare l'uno o l'altro;
- raccomandazione sequenziale: prevedere "il prossimo brano" in funzione di quelli precedenti;
- raccomandazione interattiva basata sul feedback.

**Perché è importante:** è il cuore del business delle piattaforme di streaming. È anche l'area più vicina all'esperienza attuale, perché il retrieval a due stadi è parente stretto del RAG.

### 5.3 Valutazione e sperimentazione — *priorità media*

**Dove entra:** tutta la sezione 4.

**Cosa studiare:**
- metriche di ranking e di pertinenza;
- differenza tra valutazione offline (su dati storici) e online (su utenti reali);
- basi di A/B testing e metriche di engagement.

**Perché è importante:** nelle aziende consumer le decisioni si prendono sui numeri. Saper dire *quanto* un sistema funziona conta quanto saperlo costruire.

### 5.4 Agenti LLM applicati al dominio musicale — *priorità bassa (già coperta)*

**Dove entra:** comprensione della richiesta (3.1) e spiegazione delle scelte (3.5).

**Cosa approfondire:**
- trasformare richieste vaghe in vincoli strutturati affidabili;
- combinare ricerca semantica e filtri su attributi misurabili;
- usare modelli locali in modo robusto.

**Perché è importante:** è il ponte tra le competenze attuali e quelle nuove, ed è il tipo di funzionalità che le piattaforme stanno lanciando adesso.

### 5.5 Teoria musicale applicata — *priorità bassa (vantaggio competitivo)*

**Dove entra:** costruzione della sequenza (3.4).

**Cosa approfondire:**
- relazioni tra tonalità e regole del mixaggio armonico;
- gestione dell'energia e della dinamica in un DJ set o in una scaletta live.

**Perché è importante:** è ciò che rende il progetto credibile agli occhi di chi lavora nel settore e difficile da replicare per chi non conosce la musica.

---

## 6. Risultato atteso

- Una **demo funzionante** in cui si scrive una richiesta e si ascolta la setlist generata.
- Un **repository** documentato, con i risultati della valutazione.
- Un **breve video** dimostrativo.
- Un **post tecnico** che racconti le scelte fatte, i risultati e i limiti.

---

## 7. Fuori scopo (per ora)

- Brani di catalogo commerciale: si lavora solo con musica a licenza aperta.
- Mixaggio audio reale tra i brani: il sistema decide *l'ordine*, non produce un mix continuo.
- Personalizzazione basata sulla storia d'ascolto di utenti reali.
- Un prodotto pubblico: è un progetto dimostrativo.

---

## 8. Decisioni aperte

- Tempo disponibile e, di conseguenza, se includere l'estensione con feedback.
- Dimensione del sottoinsieme di catalogo da usare.
- Design tecnico dettagliato, da definire in un documento successivo.
