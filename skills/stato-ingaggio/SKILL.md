---
name: stato-ingaggio
description: >
  Tiene lo stato vivo dell'ingaggio con un cliente: dove siamo, cosa è aperto, scadenze,
  decisioni prese, promesse fatte da te e cose che aspetti dagli altri. Si aggiorna dopo
  ogni call, mail importante o consegna, e prepara la call successiva. Si attiva con
  frasi come "aggiorna lo stato di [cliente] dopo la call", "a che punto siamo con
  [cliente]", "cosa ho promesso a [cliente]", "cosa manca di questa lista", "cosa aspetto
  da loro", "fammi il recap delle attività aperte", "riprendi l'ultima call e ricordami i
  prossimi passi", "preparami per la call con [cliente]".
license: CC-BY-4.0
---

# Stato dell'ingaggio

> **In una riga:** dopo ogni call lo stato del cliente si aggiorna in tre file, e la domanda "a che punto siamo" ha una risposta che non dipende dalla memoria di nessuno.

## Quando usarla

Con più clienti aperti, le promesse fatte in call si perdono nel giro di due settimane. La skill le scrive nel momento in cui nascono, con una data e una fonte, e le chiude solo quando c'è una prova.

Si usa in tre momenti:

| Momento | Frase tipica | Cosa produce |
|---|---|---|
| Dopo un evento | "aggiorna lo stato dopo la call" | Voce in `CALL.md`, righe in `PROMESSE.md`, `STATO.md` aggiornato |
| A richiesta | "a che punto siamo", "cosa ho promesso" | Risposta breve letta dai tre file, con la data dell'ultimo aggiornamento |
| Prima di una call | "preparami per la call" | Una pagina: relazione, promesse nei due sensi, decisioni da ottenere, domande |

## Cosa chiedere prima di partire

Per un aggiornamento servono quattro cose. Se l'utente incolla appunti o una trascrizione, quasi tutte si ricavano da lì.

1. Quale cliente.
2. Cosa è successo: appunti, trascrizione, mail, oppure un racconto a voce di tre righe.
3. Data dell'evento e chi era presente.
4. Se qualcosa di quello che è stato detto è riservato rispetto ad altre persone dello stesso cliente.

Per "a che punto siamo" e per la preparazione di una call basta il nome del cliente.

## I file

Stanno in `clienti/<codice>/`. Se mancano, creali dai modelli in fondo. Se manca anche la cartella del cliente, creala con i tre file e segnala che la scheda del cliente non c'è (la apre `spazio-cliente`).

| File | Cosa contiene | Cosa non contiene |
|---|---|---|
| `STATO.md` | fase, aperti, scadenze, decisioni, file prodotti | fatti sul cliente e numeri di mercato |
| `PROMESSE.md` | impegni con un responsabile e una data, nei due sensi | idee, desideri, cose "da valutare" |
| `CALL.md` | una voce per call, tre righe | la trascrizione intera |

I fatti nuovi sul cliente (un numero, un nome, un prezzo) vanno nel file del sapere del cliente con l'etichetta DETTO, e lo stato li cita.

## I passi

### Dopo una call, una mail o una consegna

1. Leggi la scheda del cliente, se esiste, e poi `STATO.md` e `PROMESSE.md`.
2. Dal materiale estrai cinque cose: decisioni prese, promesse fatte dall'utente, impegni presi dagli altri, date, domande rimaste aperte. Per ogni promessa annota la frase da cui nasce.
3. Aggiungi la voce in `CALL.md`: data, presenti, cosa si è deciso, cosa resta aperto, una frase testuale che conviene ricordare.
4. Aggiorna `PROMESSE.md`. Le promesse nuove entrano con responsabile, destinatario e data. Quelle chiuse cambiano stato in `fatto` con la data e la prova. Nessuna riga si cancella.
5. Aggiorna `STATO.md`: la riga dell'ultimo aggiornamento, dove siamo, gli aperti, le scadenze, le decisioni, i file prodotti.
6. Porta i fatti nuovi nel file del sapere. Se un numero contraddice uno già scritto, tienili entrambi in fila per data e segnalalo.
7. Mostra un riepilogo di poche righe: cosa è cambiato, promesse in scadenza entro sette giorni, divergenze trovate.

### "A che punto siamo"

Rispondi in quest'ordine: promesse scadute, promesse in scadenza entro sette giorni, cose che l'utente aspetta da altri, decisioni da prendere, prossima scadenza fissa. Chiudi con la data dell'ultimo aggiornamento dello stato. Se è più vecchia di quattordici giorni dillo nella prima riga, perché la risposta potrebbe essere superata.

Quando l'utente incolla una lista di attività e chiede cosa manca, confrontala con `PROMESSE.md` e con gli aperti dello stato. Riporta le voci presenti nei file e assenti dalla lista, e quelle della lista che nei file non hanno responsabile o data.

### Prima di una call

Una pagina, quattro blocchi:

1. Stato della relazione in tre righe, con l'ultima decisione presa.
2. Promesse aperte nei due sensi, con le scadute in testa.
3. Decisioni da ottenere in questa call, una riga ciascuna.
4. Tre domande da fare, ognuna legata a un gap del file del sapere o a un aperto dello stato.

## Regole

1. Una promessa ha sempre un responsabile, una data e una fonte. Una frase senza data è un'intenzione, e va in fondo allo stato tra le cose da chiarire.
2. Una promessa si chiude per evidenza (un file consegnato, una mail inviata, una frase detta in call) e mai perché è passato del tempo.
3. Gli aperti dello stato sono al massimo sette. L'ottavo obbliga a chiuderne uno, a spostarlo in `PROMESSE.md` o a dichiararlo fermo.
4. Lo stato si riscrive a ogni aggiornamento. `CALL.md` e le righe chiuse di `PROMESSE.md` restano come sono state scritte.
5. Se due persone dello stesso cliente vengono sentite separatamente, le note dell'una non entrano nel materiale preparato per l'altra. Nella voce della call si segnano con la parola `riservato` e il ruolo di chi le ha dette.
6. Lo stato datato vive qui e non nel file di istruzioni generale, che deve contenere solo regole che valgono per mesi.

## Modelli

### `STATO.md`

```markdown
# <Nome>: stato

**Ultimo aggiornamento:** AAAA-MM-GG (<cosa è cambiato, una riga>)

## Dove siamo
- <fase, date, ultimo fatto rilevante>

## Aperti (massimo 7, con data)
- <cosa> | <chi> | <entro quando>

## Scadenze fisse
- <data>: <evento>

## Decisioni prese
- <data>: <decisione> (<fonte>)

## File prodotti
- <data>: `<percorso>`: <cosa è>

## Da chiarire
- <intenzioni senza data o senza responsabile>
```

### `PROMESSE.md`

```markdown
# <Nome>: promesse

## Promesse mie
| Data | Promessa | A chi | Entro | Fonte | Stato |
|---|---|---|---|---|---|

## Aspetto da altri
| Data | Cosa | Da chi | Entro | Fonte | Stato |
|---|---|---|---|---|---|
```

Stati ammessi: `aperta`, `fatto AAAA-MM-GG (<prova>)`, `spostata a AAAA-MM-GG`, `caduta (<motivo>)`.

### `CALL.md`

```markdown
# <Nome>: call

## AAAA-MM-GG, <con chi>
Deciso: <una o due righe>
Aperto: <una o due righe>
Frase da ricordare: "<testuale>"
```

## Esempio

Esempio inventato: cliente, persone, date e contenuti non esistono.

Dopo una call di mezz'ora con il direttore vendite di una torrefazione, l'utente incolla gli appunti e scrive "aggiorna lo stato". Il riepilogo che torna:

```
Stato aggiornato al 10/03.
Nuove promesse mie: griglia di qualifica per gli agenti (entro 17/03), bozza del listino uffici (entro 24/03).
Aspetto da loro: elenco dei clienti persi nel 2024, dal direttore vendite, entro 14/03.
Chiusa: analisi dell'elenco fatture, consegnata il 07/03 (file in bozze/).
Divergenza: i clienti attivi sono 164 nell'elenco fatture e "circa 200" nella call del 03/03. Tenuti entrambi.
In scadenza entro 7 giorni: 2.
```

## Errori da evitare

- Scrivere una promessa senza data perché in call non è stata detta. Si scrive tra le cose da chiarire e si chiede la data alla prima occasione.
- Chiudere una promessa perché "sarà stata fatta". Senza prova resta aperta.
- Usare lo stato come archivio dei fatti sul cliente. I fatti hanno la loro casa, lo stato li cita.
- Riscrivere le voci vecchie di `CALL.md` alla luce di quello che si è saputo dopo.
- Rispondere "a che punto siamo" con un racconto. La risposta è un elenco con le date, e le scadute stanno in testa.
- Far crescere gli aperti oltre sette. Una lista di venti voci non si legge e smette di guidare la settimana.
- Portare nel materiale per una persona le cose dette in confidenza da un'altra.

## Se non puoi scrivere file

Produci i tre file aggiornati in blocchi separati, con il percorso in testa a ciascuno, e chiedi all'utente di salvarli. Alla conversazione successiva l'utente li incolla e si riparte da lì.
