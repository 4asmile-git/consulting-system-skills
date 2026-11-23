---
name: controllo-settimanale
description: >
  Controllo settimanale delle incoerenze nella cartella di lavoro di un consulente:
  clienti non registrati, lo stesso fatto scritto in due posti con valori diversi, numeri
  senza data o fonte, stati non aggiornati, promesse scadute, versioni doppie dei
  documenti, file di istruzioni appesantito da stato datato, correzioni in coda. Sceglie
  al massimo tre interventi e la volta dopo verifica che siano stati fatti. Una volta al
  mese aggiunge un controllo di salute con poche misure. Si attiva con frasi come
  "controllo settimanale", "controlla le incoerenze", "è tutto allineato", "fai ordine
  nella cartella", "pota il file di istruzioni", "controllo di salute", "come sto usando
  il sistema", "cosa miglioreresti nella struttura".
license: CC-BY-4.0
---

# Controllo settimanale

> **In una riga:** una volta a settimana si cercano le incoerenze con un elenco fisso di controlli, si scelgono tre interventi e si lascia stare il resto.

## Quando usarla

Un sistema di file tenuto da una persona sola si sporca in modi prevedibili: un numero aggiornato in un file e non nell'altro, uno stato fermo da un mese, due versioni dello stesso documento con date diverse. Nessuno di questi problemi fa rumore finché non finisce in un documento consegnato. Il controllo li cerca a cadenza fissa, quando costano poco.

Si lancia a fine settimana, a mano. Chi ha la possibilità di programmare un'attività ricorrente può agganciarla a questa skill, ma non è richiesto.

La richiesta "cosa miglioreresti" trova qui una risposta ordinata: prima i controlli, poi tre interventi, senza un elenco di idee.

## Cosa chiedere prima di partire

Niente. La skill legge la cartella. Chiede soltanto, se non lo trova scritto, quale file fa da file di istruzioni del progetto.

## I passi

### 1. Verifica degli interventi precedenti

Apri `sistema/CONTROLLI.md` (se manca, crealo dal modello) e leggi i tre interventi scelti la volta scorsa. Per ciascuno guarda nei file se è stato fatto. Un intervento non fatto per due controlli di fila si ripropone una volta con la domanda se va tolto: forse non era così importante.

### 2. I nove controlli

Per ogni problema trovato scrivi una riga con il file, il punto e il rimedio già pronto.

| # | Controllo | Cosa si cerca |
|---|---|---|
| 1 | Clienti registrati | Clienti attivi nell'elenco senza cartella o senza scheda; schede con voci vuote; cartelle che non compaiono nell'elenco |
| 2 | Un fatto, una casa | Lo stesso numero o lo stesso fatto scritto per esteso in due file, soprattutto se con valori diversi |
| 3 | Numeri | Cifre senza data, senza fonte o senza etichetta; serie che non ricevono un punto nuovo da più tempo della loro cadenza |
| 4 | Stato e promesse | Stati di clienti attivi non aggiornati da quattordici giorni; più di sette aperti; promesse scadute; bozze in coda con l'evento già passato |
| 5 | Versioni | Due versioni dello stesso documento una accanto all'altra. Vale quella con la data più recente nel nome, le altre vanno in `archivio/` |
| 6 | File di istruzioni | Stato datato dentro le regole: date, "questa settimana", eventi in corso, elenchi che cambiano spesso. Lunghezza cresciuta rispetto al controllo precedente |
| 7 | Correzioni | Voci nella coda Da verificare; correzioni con contatore a due o più e nessuna regola scritta; regole doppie o in contraddizione |
| 8 | Richieste ripetute | Temi nel registro delle richieste arrivati a due o più occorrenze senza una skill |
| 9 | Stile | Tre testi recenti presi a caso, riletti contro la lista nera |

I controlli che dipendono da un file che non esiste si saltano, con una riga che dice quale skill lo crea.

### 3. Cosa si sistema subito e cosa no

Si sistema senza chiedere solo ciò che è meccanico e reversibile: spostare in `archivio/` una versione superata, sostituire con un rimando una copia identica alla casa del fatto, correggere la data `aggiornato` di una scheda appena riletta.

Tutto quello che cambia un fatto, una regola o il file di istruzioni si propone e aspetta un sì. Se è installata `chi-approva-cosa`, vale la sua mappa.

### 4. La potatura del file di istruzioni

Il file di istruzioni viene caricato a ogni conversazione, quindi ogni riga inutile costa ogni volta. Quando il controllo 6 trova stato datato:

1. Scrivi la versione potata in un file a parte, accanto all'originale.
2. Sposta lo stato datato dove deve stare: negli stati dei clienti, oppure in `sistema/IN_CORSO.md` se riguarda il modo di lavorare e non un cliente (un elenco datato, una riga per voce).
3. Mostra la differenza tra le due versioni.
4. Sostituisci l'originale solo dopo il sì.

### 5. Il rapporto

Una schermata, in quest'ordine: esito degli interventi precedenti, numero di problemi per controllo, i tre interventi proposti per la settimana (ognuno con il primo passo pronto), l'elenco dei problemi rimandati. Scrivi la voce in `sistema/CONTROLLI.md`.

I tre interventi si scelgono con questo criterio: prima ciò che può finire in un documento consegnato, poi ciò che si ripete, poi il resto.

Un problema che l'utente decide di non sistemare si segna come `accettato` e non viene più riproposto.

## Il controllo di salute mensile

Una volta al mese, al posto del rapporto normale. Prima si verifica l'esito degli interventi del mese prima, poi si misurano otto cose e si confrontano con il mese precedente.

| Misura | Come si conta |
|---|---|
| Stati aggiornati | clienti attivi con `STATO.md` aggiornato negli ultimi quattordici giorni, sul totale |
| Promesse puntuali | promesse chiuse entro la data, sul totale delle chiuse nel mese |
| Correzioni ripetute | righe del registro con contatore a due o più |
| Richieste instradate | richieste del mese risolte da una skill esistente, contro prompt scritti da zero |
| Attesa delle bozze | bozze rimaste in coda più di sette giorni |
| Peso delle istruzioni | righe del file di istruzioni, rispetto al mese prima |
| Skill ferme | skill installate mai usate nel mese |
| Voci mancanti | voci `manca` nelle schede dei clienti attivi |

Dalle misure escono al massimo tre interventi per il mese. Una misura che migliora per due mesi di fila è un buon argomento per alzare l'autonomia sul tipo di output collegato.

Le misure che la cartella non permette di contare si dichiarano non misurabili, con il file che servirebbe.

## Modelli

### `sistema/CONTROLLI.md`

```markdown
# Controlli

## AAAA-MM-GG (settimanale | mensile)

Interventi precedenti: 1) fatto 2) non fatto 3) fatto

| # | Controllo | Problemi | Sistemati subito |
|---|---|---|---|
| 1 | Clienti registrati | | |
| 2 | Un fatto, una casa | | |
| 3 | Numeri | | |
| 4 | Stato e promesse | | |
| 5 | Versioni | | |
| 6 | File di istruzioni | | |
| 7 | Correzioni | | |
| 8 | Richieste ripetute | | |
| 9 | Stile | | |

Interventi scelti:
1. <cosa> (<file>, primo passo: <azione>)
2. ...
3. ...

Rimandati: <elenco breve>
Accettati: <problemi che l'utente ha deciso di non sistemare>
```

## Esempio

Esempio inventato: clienti, file e numeri non esistono.

```
Controllo del 21/03.
Interventi della volta scorsa: 2 fatti, 1 no (la scheda del cliente C ha ancora tre voci vuote).

Problemi: 11 in tutto. Sistemati subito 3 (due versioni superate in archivio, una copia sostituita da un rimando).

Interventi proposti:
1. Il prezzo d'ingresso del cliente A è 39 euro in SAPERE.md e 49 nella bozza del piano. La bozza esce giovedì. Primo passo: dimmi quale vale.
2. Il cliente B non ha aggiornamenti di stato da 23 giorni e ha due promesse scadute. Primo passo: dieci minuti di aggiornamento con te.
3. Il file di istruzioni contiene il calendario di un evento di febbraio. Primo passo: ti mostro la versione potata.

Rimandati: 5 (elenco nel file dei controlli).
```

## Errori da evitare

- Sistemare tutto in una volta. Tre interventi a settimana si portano a termine, dieci restano sulla carta.
- Rispondere a ogni problema con una regola nuova. Molte incoerenze si chiudono correggendo un file, e le regole in più pesano sul file di istruzioni.
- Cambiare un fatto durante il controllo perché "era chiaramente sbagliato". Si propone e si aspetta.
- Scrivere un rapporto lungo. Oltre una schermata nessuno lo legge e la settimana dopo non si rifà.
- Saltare la verifica degli interventi precedenti. Senza quella il controllo produce elenchi e basta.
- Riproporre ogni settimana un problema che l'utente ha già deciso di accettare.
- Potare il file di istruzioni sovrascrivendo l'originale prima di aver mostrato la differenza.

## Se non puoi scrivere file

Il controllo richiede di leggere la cartella. Senza accesso ai file, chiedi all'utente di incollare l'elenco dei clienti, gli stati e il file di istruzioni, esegui i controlli 4, 6 e 7 e dichiara quali hai saltato.
