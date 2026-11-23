---
name: correzione-in-regola
description: >
  Trasforma una correzione in una regola scritta, così lo stesso errore non torna alla
  conversazione successiva. Gestisce tre tipi di correzione: di stile (la lista nera
  delle frasi e delle parole che suonano scritte da una macchina), di fatto (un dato
  sbagliato o superato) e di comportamento (un modo di lavorare da cambiare). Rilegge
  anche un testo contro la lista nera prima della consegna. Si attiva con i comandi
  "lista nera: ...", "fatto: ...", "regola: ..." e con frasi come "te l'ho già detto",
  "è la seconda volta che lo correggo", "non scrivere più così", "questo dato è vecchio",
  "ricordatelo per le prossime volte", "rileggi questo testo contro la lista nera",
  "togli dalla lista nera".
license: CC-BY-4.0
---

# Correzione in regola

> **In una riga:** un errore corretto due volte a mano è un errore del sistema, e si corregge nel sistema: nella lista di stile, nella casa del fatto o nella regola di lavoro.

## Quando usarla

Ogni volta che l'utente corregge qualcosa che può ripetersi. La correzione nella singola risposta si fa comunque. La skill aggiunge il secondo passo: scrivere la correzione dove verrà letta la prossima volta.

| Tipo | Comando breve | Esempio di frase | Dove finisce |
|---|---|---|---|
| Stile | `lista nera: <cosa>` | "non usare più questa espressione" | `sistema/STILE.md`, sezione Aggiunte |
| Fatto | `fatto: <cosa>` | "questo numero è superato", "non è più il loro fornitore" | nella casa di quel fatto, più una riga nel registro |
| Comportamento | `regola: <cosa>` | "prima di scrivere il documento chiedimi il formato" | nel file di istruzioni dell'ambito giusto, più una riga nel registro |

I comandi brevi servono a chi vuole correggere in tre secondi. La skill riconosce anche le correzioni dette a parole, e in quel caso dichiara in una riga come le ha classificate.

## Cosa chiedere prima di partire

Di norma niente: le correzioni si applicano subito e si confermano con una riga. Si chiede solo in tre casi.

1. Non è chiaro l'ambito: la regola vale per tutti i clienti o per uno solo.
2. La correzione di un fatto contraddice un dato scritto con un'etichetta più forte (per esempio un numero letto in un documento contro uno detto a voce).
3. La regola nuova contraddice una regola già scritta.

## I file

Se mancano, creali: `sistema/STILE.md` dal contenuto di `references/lista-nera-di-partenza.md`, `sistema/CORREZIONI.md` dal modello in fondo.

Perché la lista e le regole vengano lette davvero, proponi all'utente di aggiungere al file di istruzioni del progetto (`CLAUDE.md` in Claude Code, le istruzioni del progetto su claude.ai) queste tre righe:

```markdown
- Prima di consegnare un testo rileggilo contro `sistema/STILE.md`.
- Una correzione che può ripetersi si applica con la skill `correzione-in-regola`, senza chiedere conferma, con una riga di eco.
- Le regole di lavoro stanno in questo file. Lo stato datato sta nei file di stato.
```

## I passi

### Correzione di stile

1. Aggiungi la voce alla sezione Aggiunte di `sistema/STILE.md`, con la data. Non chiedere conferma.
2. Riscrivi il passaggio che ha provocato la correzione.
3. Rispondi con una riga di eco: cosa è entrato nella lista.

Per togliere una voce l'utente scrive `lista nera togli: <cosa>`. La voce si sposta nella sezione Tolte con la data, così resta traccia del ripensamento.

### Correzione di fatto

1. Trova la casa del fatto. Per un cliente è il file indicato dalla sua scheda; per il resto è il file dove quel fatto è scritto per esteso.
2. Correggi lì, con data, fonte ed etichetta. Il valore vecchio resta nella riga precedente se è un numero in serie, altrimenti si sostituisce.
3. Cerca le copie dello stesso fatto negli altri file. Dove trovi una copia, sostituiscila con un rimando alla casa oppure allineala.
4. Scrivi una riga in `sistema/CORREZIONI.md`.
5. Rispondi con una riga di eco: cosa è cambiato e in quale file.

### Correzione di comportamento

1. Scegli l'ambito più stretto in cui la regola è vera: una sola skill, un solo cliente (la sua scheda), tutto il lavoro (il file di istruzioni generale).
2. Scrivi la regola come un'istruzione eseguibile: quando si applica e cosa si fa. Un divieto senza alternativa lascia il problema dov'era.
3. Controlla che non contraddica una regola esistente. Se la contraddice, chiedi quale vale.
4. Scrivi una riga in `sistema/CORREZIONI.md`.
5. Rispondi con una riga di eco: la regola e dove è stata scritta.

### La regola della seconda volta

Quando una correzione arriva per la seconda volta, cerca la prima nel registro. Se c'è già una regola e non ha funzionato, la regola va riscritta o spostata in un file che viene letto prima. Se la prima volta era stata sistemata solo la risposta, adesso si scrive la regola. In entrambi i casi il contatore `Volte` della riga sale.

Vale anche in senso inverso: quando Claude nota un'incoerenza che non può sistemare al volo (due file che dicono cose diverse, una regola che non si riesce più ad applicare), la mette nella coda Da verificare senza aspettare che l'utente se ne accorga.

### La coda Da verificare

Una correzione che richiede un controllo prima di essere applicata non si applica e non si perde: va nella sezione Da verificare del registro, con quello che serve per scioglierla. La coda si svuota una volta a settimana (lo fa `controllo-settimanale`, oppure l'utente quando chiede "cosa c'è da verificare").

### Rilettura di un testo contro la lista nera

1. Leggi `sistema/STILE.md` per intero, comprese le Aggiunte.
2. Segna ogni passaggio che viola una voce e riscrivilo. Per gli incisi scegli caso per caso tra virgola, parentesi, due punti o due frasi separate: una sostituzione meccanica crea un tic nuovo al posto del vecchio.
3. Rileggi una seconda volta cercando le frasi che suonano scritte da una macchina senza violare nessuna voce. Si riscrivono lo stesso: la lista è il pavimento.
4. Restituisci il testo corretto e, sotto, l'elenco breve di cosa hai cambiato.

Quando si scrive in un'altra lingua valgono le costruzioni equivalenti.

## Regole

1. Le correzioni di stile e quelle chiare di fatto e di comportamento si applicano senza chiedere conferma. Sono reversibili e il registro dice cosa è stato fatto.
2. Una regola, una casa. La stessa regola scritta in due file diverge al primo aggiornamento.
3. L'ambito più stretto vince. Una regola nata per un cliente non sale nel file generale finché non si è vista su un secondo cliente.
4. Le regole si ritirano. Una regola che da tre mesi non serve più, o che un'altra regola ha assorbito, passa nella sezione Ritirate.
5. Il registro non contiene fatti riservati dei clienti: dice quale file è stato corretto, non ripete il dato.

## Modelli

### `sistema/CORREZIONI.md`

```markdown
# Registro delle correzioni

## Applicate
| Data | Tipo | Correzione | Dove è stata scritta | Volte |
|---|---|---|---|---|

## Da verificare
| Data | Cosa | Cosa serve per decidere | Chi lo sa |
|---|---|---|---|

## Ritirate
| Data | Regola | Motivo |
|---|---|---|
```

### `sistema/STILE.md`

Il contenuto di partenza è in `references/lista-nera-di-partenza.md`. In fondo ha due sezioni che crescono con l'uso:

```markdown
## Aggiunte
- AAAA-MM-GG: <espressione o abitudine>

## Tolte
- AAAA-MM-GG: <voce> (<motivo>)
```

## Esempio

Esempio inventato, serve solo a mostrare l'eco di una riga.

```
Utente: lista nera: "a 360 gradi"
Claude: Aggiunta alla lista nera: "a 360 gradi". Ho riscritto il secondo paragrafo.

Utente: fatto: il listino uffici parte da 39 euro al mese, non da 49
Claude: Corretto in clienti/torrefazione-alfa/SAPERE.md §5 (DETTO, oggi). C'era una copia nella bozza del piano: allineata.

Utente: regola: i documenti per questo cliente partono sempre dall'indice, me lo fai approvare e poi scrivi
Claude: Scritta nei Confini della scheda del cliente: prima l'indice, poi il testo dopo il tuo sì.
```

## Errori da evitare

- Sistemare la risposta e fermarsi lì. Alla conversazione successiva l'errore torna.
- Chiedere conferma per ogni aggiunta alla lista nera. L'utente smette di correggere.
- Sostituire un tic con un altro, per esempio mettere una virgola al posto di ogni trattino lungo.
- Scrivere la regola nel file generale quando vale per un cliente solo.
- Scrivere regole vaghe ("fai più attenzione ai numeri"). Una regola dice quando si applica e cosa si fa.
- Correggere un fatto in un file e lasciare le copie negli altri.
- Lasciare crescere la lista senza mai ritirare nulla. Una lista di duecento voci non viene più letta.
- Applicare di forza una correzione che contraddice un dato più solido. Va nella coda Da verificare.

## Se non puoi scrivere file

Mostra la riga da aggiungere e il file in cui va, in un blocco che l'utente può copiare. A inizio conversazione chiedi all'utente di incollare `sistema/STILE.md` se deve scrivere testi.
