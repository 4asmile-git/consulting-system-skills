---
name: daily-plan
description: >
  Apre e chiude la giornata di chi lavora su più clienti. Al primo messaggio del giorno
  legge stati, promesse e bozze in attesa, ricorda l'impegno preso il giorno prima e fa
  una domanda sola con le proposte su ciò che è scaduto o fermo. Poi propone al massimo
  tre priorità. A fine giornata registra cosa è stato fatto e l'impegno per domani. Si
  attiva con frasi come "piano di oggi", "apriamo la giornata", "cosa devo fare oggi",
  "cosa è urgente", "cosa aspetta me", "chi mi deve qualcosa", "decisioni aperte",
  "chiudi la giornata", "facciamo il punto della settimana".
license: CC-BY-4.0
---

# Piano del giorno

> **In una riga:** la giornata si apre con una domanda sola su ciò che è scaduto o fermo, e si chiude con un impegno scritto per il giorno dopo.

## Quando usarla

Con molti clienti aperti insieme, la mattina il problema è scegliere. La lista di tutto quello che è aperto esiste già nei file di stato e non aiuta a decidere. Questa skill legge quei file per tutti i clienti attivi e restituisce poche righe: cosa è scaduto, cosa aspetta una decisione, quali tre cose contano oggi.

Non fa il lavoro dei clienti. Indica dove andare e lascia il lavoro alla conversazione dedicata a quel cliente.

## Cosa chiedere prima di partire

Niente, se i file ci sono. La skill legge e propone. Chiede soltanto quello che non può leggere:

1. Appuntamenti fissi di oggi, se Claude non ha accesso al calendario.
2. Ore di lavoro disponibili al netto degli appuntamenti.
3. Novità arrivate fuori dai file (una telefonata, un messaggio) che cambiano le priorità.

Se l'utente non risponde a queste tre, si procede con quello che c'è e lo si dichiara.

## Cosa legge

| File | Cosa ne prende |
|---|---|
| `clienti/ELENCO.md` | quali clienti sono attivi |
| `clienti/<codice>/STATO.md` | scadenze fisse, aperti, data dell'ultimo aggiornamento |
| `clienti/<codice>/PROMESSE.md` | promesse scadute o in scadenza, cose attese da altri |
| `sistema/IN_ATTESA.md` | bozze che aspettano un sì, con la data dell'evento |
| `sistema/GIORNATE.md` | l'impegno preso ieri, cosa è già stato mostrato e ignorato |

Se un file manca si salta, e alla fine si dice in una riga quale manca e quale skill lo crea. Se manca `sistema/GIORNATE.md`, crealo dal modello.

## I passi

### Apertura (primo messaggio del giorno)

1. Leggi i file della tabella.
2. Scrivi l'apertura, in non più di quindici righe:
   - l'impegno di ieri, con la richiesta di dire se è stato fatto;
   - le proposte numerate su promesse scadute e bozze ferme, ognuna con un'azione suggerita tra chiudere, spostare a una data, lasciare;
   - una domanda sola in fondo: "va bene così o cambi qualche riga".
3. Aspetta la risposta. Le forme brevi che la skill capisce:
   - `ok` accetta tutte le proposte;
   - `no` le lascia tutte come sono;
   - una riga per numero: `2 fatto`, `4 venerdì`, `5 lascia`.
   Valgono anche le stesse cose dette a parole.
4. Applica le risposte ai file (stato delle promesse, righe della coda) e conferma in una riga.
5. Proponi il piano: al massimo tre priorità, ognuna con il cliente e il motivo (una scadenza, una promessa, una decisione). Sotto, le call di oggi con la cosa da ottenere da ciascuna, e le cose attese da altri che conviene sollecitare.
6. Scrivi la voce di oggi in `sistema/GIORNATE.md`.

Se non c'è nulla di scaduto o fermo, l'apertura si riduce all'impegno di ieri e al piano. Se non c'è nemmeno quello, non si scrive nulla di rito.

### Quando l'utente ignora la domanda

L'apertura si mostra una volta. Se l'utente passa ad altro, si segue lui. La stessa proposta può tornare nei giorni successivi per tre volte al massimo, poi si ferma e la riga passa tra le cose ferme che guarderà il controllo settimanale. Il campo `Mostrato` in `GIORNATE.md` serve a contare.

Un sì dato a un'altra domanda non vale come risposta all'apertura.

### Chiusura ("chiudi la giornata")

1. Chiedi in una riga cosa è stato fatto delle tre priorità, se non risulta già dalla conversazione.
2. Aggiorna le promesse chiuse oggi, con la prova.
3. Chiedi un solo impegno per domani e scrivilo nella voce di oggi.
4. Segnala i clienti toccati oggi il cui stato non è stato aggiornato.

### Punto della settimana (ultimo giorno lavorativo)

Tre righe in più nell'apertura o nella chiusura: i clienti attivi senza aggiornamenti da sette giorni, le call della settimana non ancora registrate, il promemoria di lanciare il controllo settimanale. Se l'utente non lo raccoglie entro la giornata, si recupera la settimana dopo.

## Regole

1. Una domanda sola per apertura. Più domande insieme non ricevono risposta.
2. Ogni proposta ha una fonte: il file e la riga da cui viene. Nessuna priorità si inventa per riempire il piano.
3. Tre priorità al massimo. La quarta entra solo se ne esce una.
4. Quello che è già stato mostrato e ignorato non si ripete oltre il limite.
5. Il piano serve a scegliere: se una priorità richiede un'ora di lavoro su un cliente, si apre la conversazione di quel cliente.
6. Niente riempitivi. Un'apertura senza novità è di due righe.

## Modelli

### `sistema/GIORNATE.md`

```markdown
# Giornate

## AAAA-MM-GG
Impegno di ieri: <testo> (fatto / non fatto / spostato)
Proposte:
| N | Cosa | Fonte | Proposta | Risposta | Mostrato |
|---|---|---|---|---|---|
| 1 | | `clienti/<codice>/PROMESSE.md` | chiudere / spostare a <data> / lasciare | | 1 |
Priorità: 1) ... 2) ... 3) ...
Chiusura: <cosa è stato fatto>
Impegno per domani: <uno>
```

Le voci più vecchie di un mese si spostano in `sistema/archivio/GIORNATE_<anno>.md`.

## Esempio

Esempio inventato: clienti, date e contenuti non esistono.

```
Ieri ti eri impegnato a chiudere la bozza del listino uffici. Fatta?

Scaduti e fermi:
1. Griglia di qualifica per gli agenti, promessa al cliente A per il 17/03. Propongo: spostare al 20/03.
2. Bozza del report mensile per il cliente B, in coda dal 12/03, serviva alla call del 14/03. Propongo: chiudere.
3. Elenco dei clienti persi, atteso dal cliente A dal 14/03. Propongo: sollecitare oggi.

Va bene così o cambi qualche riga?
```

Risposta dell'utente: `sì fatta. 1 ok, 2 lascia, 3 ok`. Claude aggiorna i file, conferma in una riga e propone le tre priorità del giorno.

## Errori da evitare

- Aprire la giornata con un rapporto lungo su tutti i clienti. Se supera una schermata non viene letto.
- Fare tre domande insieme.
- Ripresentare ogni mattina la stessa cosa ignorata.
- Mettere tra le priorità ciò che è soltanto vecchio. Una priorità ha una scadenza, una promessa o una decisione dietro.
- Applicare una proposta senza risposta. Il silenzio lascia le cose come sono.
- Cominciare a lavorare su un cliente dentro la conversazione del piano, mescolando i contesti.
- Dimenticare la chiusura. Senza l'impegno scritto la sera, l'apertura del giorno dopo non ha da dove partire.

## Se non puoi scrivere file

L'utente incolla gli stati e le promesse dei clienti attivi, oppure li racconta in poche righe. La skill restituisce l'apertura, il piano e il blocco della voce di oggi da salvare.
