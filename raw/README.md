# raw/ — fonti immutabili

Qui vanno le **fonti del progetto**, così come sono, **senza modificarle**: idee e appunti, paper,
documentazione, repo di riferimento, risultati di esperimenti.

Due sottocartelle:
- **`input/`** — fonti **tue**: idee, appunti, paper, documentazione, repo di riferimento.
- **`output/`** — materiale prodotto **dall'agente** durante il lavoro: sintesi di discussioni validate, risultati di prove ed esperimenti. Resta una fonte da ingerire, ma si distingue a colpo d'occhio da ciò che hai scritto tu.

Regole:
- L'LLM **legge** da `input/` e non modifica mai quei file. In `output/` scrive solo file nuovi, e una volta scritti non li modifica.
- Un requisito in [[requisiti]] che nasce da una fonte la cita qui (colonna *Origine*); quelli nati
  da un'idea tua non hanno bisogno di un file.
- Nel **blueprint** questa cartella resta vuota; si riempie solo nelle istanze-progetto.
