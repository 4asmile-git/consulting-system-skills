---
name: spazio-cliente
description: >
  Apre lo spazio di lavoro di un cliente nuovo e lo tiene leggibile: una cartella, una
  scheda a dodici voci che dice dove vive ogni pezzo del sapere su quel cliente, un file
  dei fatti con data e fonte, lo stato dell'ingaggio e un solo elenco dei clienti. Serve
  anche per allineare un cliente che ha già materiale sparso e per rispondere a "abbiamo
  già uno spazio per questo cliente". Si attiva con frasi come "nuovo cliente [nome]",
  "apri lo spazio per [nome]", "[nome] ha firmato", "prepara le cartelle per il nuovo
  cliente", "allinea [cliente] alla scheda", "esiste già uno spazio per [nome]",
  "controlla i clienti". Vale anche per un'area che non è un cliente (amministrazione,
  contenuti, un progetto personale).
license: CC-BY-4.0
---

# Spazio cliente

> **In una riga:** ogni cliente ha una cartella fatta allo stesso modo e una scheda che si legge per prima, così ogni lavoro parte dal contesto giusto senza doverlo rispiegare.

## Quando usarla

Chi segue più clienti insieme perde tempo in due modi: rispiega il contesto a ogni conversazione e non ricorda dove ha messo un dato. La skill risolve tutti e due i problemi con una convenzione sola.

Si usa in tre momenti:

| Momento | Frase tipica | Cosa fa |
|---|---|---|
| Apertura | "nuovo cliente [nome]", "[nome] ha firmato" | Crea cartella, scheda, file dei fatti, stato e riga nell'elenco |
| Allineamento | "allinea [cliente] alla scheda" | Scrive solo la scheda, puntando ai file dove il sapere vive già. Non sposta nulla |
| Controllo | "controlla i clienti", "esiste già uno spazio per [nome]" | Verifica che ogni cliente attivo sia registrato e che la scheda sia completa |

Prima di aprire uno spazio nuovo la skill controlla sempre l'elenco. La domanda "ne avevamo già uno" arriva spesso, e una seconda cartella per lo stesso cliente è l'errore più costoso da rimediare.

## Cosa chiedere prima di partire

Sei domande, in un solo messaggio. Quello che l'utente non sa si scrive `manca`, non si inventa.

1. Nome del cliente e un codice breve per la cartella (minuscolo, senza spazi).
2. Tipo di ingaggio e date: inizio, fine o rinnovo, eventuale finestra di disdetta.
3. Persone: chi decide, chi firma, chi è il riferimento di tutti i giorni.
4. Perimetro: cosa prevede l'accordo e cosa resta fuori.
5. Confini: riservatezza tra le persone del cliente, conflitti con altri clienti o fornitori, lingua dei documenti.
6. Materiale già disponibile (call, documenti, esportazioni) e fonti che Claude può leggere per questo cliente, con quale account.

## La struttura

```
clienti/
  ELENCO.md            l'unico elenco dei clienti
  <codice>/
    SCHEDA.md          l'indice a dodici voci, si legge per primo
    SAPERE.md          i fatti sul cliente, con data, fonte ed etichetta
    STATO.md           dove siamo, cosa è aperto, scadenze, decisioni
    PROMESSE.md        cosa hai promesso tu e cosa aspetti dagli altri
    CALL.md            una voce per call, in ordine di data
    ricevuti/          materiale arrivato dal cliente, non si modifica
    bozze/             documenti in attesa della tua approvazione
    archivio/          versioni superate
```

Due registri e nessun altro: l'elenco dei clienti e la scheda di ciascuno. Un elenco di clienti riscritto dentro una skill o dentro un altro file è un debito, perché al prossimo cliente nuovo qualcuno si dimentica di aggiornarlo.

Le altre cartelle si aggiungono quando servono, con una riga nella scheda che dice cosa contengono.

## I passi

### Apertura

1. Leggi `clienti/ELENCO.md`. Se manca, crealo dal modello qui sotto. Se il cliente c'è già, fermati e proponi l'allineamento.
2. Crea `clienti/<codice>/` con le tre sottocartelle.
3. Scrivi `SCHEDA.md` dal modello. Ogni voce punta al file e alla sezione dove quel sapere vive. Una voce che non ha ancora contenuto si scrive `manca`, con il nome di chi ha il dato.
4. Scrivi `SAPERE.md` con quello che si sa già. Ogni fatto porta data, fonte ed etichetta (vedi le regole sui fatti).
5. Crea `STATO.md`, `PROMESSE.md` e `CALL.md` dai modelli. Se è installata `stato-ingaggio`, da qui in poi li tiene lei.
6. Aggiungi la riga del cliente in `ELENCO.md`.
7. Fai l'inventario del materiale già esistente: cosa c'è, dove, di che data. Quello che arriva dal cliente va in `ricevuti/` senza modifiche. Per ogni call già fatta, una voce in `CALL.md`.
8. Chiudi con un riepilogo breve: file creati, voci rimaste `manca` con chi ha il dato, le prime tre domande da fare al cliente.

### Allineamento di un cliente che esiste già

Scrivi soltanto `SCHEDA.md`, con i puntatori ai file dove il sapere sta oggi, anche se hanno altri nomi e altre cartelle. Lo spostamento dei file è un lavoro a parte, da fare solo se l'utente lo chiede. Una scheda che descrive il disordine vale più di un riordino lasciato a metà.

### Controllo

Per ogni cliente con stato `attivo` nell'elenco verifica quattro cose: la cartella esiste, la scheda ha tutte le dodici voci, nessuna voce è vuota (o punta a un file, o dice `manca`), la data `aggiornato` della scheda non è più vecchia di due mesi. Poi cerca le cartelle in `clienti/` che non compaiono nell'elenco. Riporta una riga per problema, con il rimedio.

## Le dodici voci

Sempre in quest'ordine e con questi nomi, così chi legge (tu, Claude, un'altra skill) sa dove guardare.

| # | Voce | Cosa contiene |
|---|---|---|
| 1 | profilo | azienda, prodotto, modello di ricavo, stadio |
| 2 | persone | chi è chi, chi decide, chi firma |
| 3 | mandato | perimetro dell'accordo, cosa è fuori, date |
| 4 | confini | riservatezza, conflitti, cosa non deve uscire |
| 5 | numeri | ogni cifra con data, fonte ed etichetta |
| 6 | segmenti | chi compra oggi, chi dovrebbe comprare, chi no, segnali d'acquisto |
| 7 | personas | chi decide, chi usa, obiezioni per ruolo |
| 8 | offerta | cosa si vende, prezzi, cosa si può dichiarare |
| 9 | messaggio | posizionamento, voce, parole da evitare |
| 10 | concorrenti | diretti, alternative, comparabili |
| 11 | canali | stato di ogni canale, cosa ha funzionato, regole |
| 12 | gap | domande aperte, dati mancanti, chi li ha |

La scheda non contiene fatti, solo puntatori. Per questo non invecchia quando cambia un numero.

## Regole sui fatti

1. Un fatto, una casa. Un numero vive in un posto solo e gli altri file lo citano.
2. Ogni affermazione ha un'etichetta: VISTO (letto in un documento o in un dato), DETTO (sentito in call o scritto in una mail), CALCOLATO (ricavato da altri numeri, con il conto), IPOTESI, NON VERIFICABILE.
3. Ogni numero porta data e fonte. Due fonti che divergono si scrivono entrambe, in fila per data. Niente medie.
4. I gap si nominano. Chi non trova un dato scrive quale fonte servirebbe e chi la possiede.
5. Quello che dipende da una persona sta nella voce persone, così quando la persona cambia si corregge un punto solo.
6. Nei file di un cliente non compaiono mai i nomi di altri clienti. Prima o poi un pezzo di quei file finisce in un documento consegnato.

## Le due fasi del sapere

All'inizio basta un file solo, `SAPERE.md`, con le sezioni nell'ordine delle voci 1 e 5-12. Si scrive in fretta e si corregge spesso: un file è più onesto di dodici file mezzi vuoti.

Quando l'ingaggio continua e una sezione supera la pagina, o viene aggiornata da lavori diversi, il file si divide in una cartella `sapere/` con un file per voce. Si fa una volta sola, poi si aggiornano i puntatori della scheda.

## Modelli

### `clienti/ELENCO.md`

```markdown
# Elenco clienti

Unico elenco. Stato: attivo, in chiusura, chiuso, fermo, prospect.

| Codice | Nome | Stato | Dal | Fino al | Cartella | Nota |
|---|---|---|---|---|---|---|
| | | | | | `clienti/<codice>/` | |
```

### `clienti/<codice>/SCHEDA.md`

```markdown
---
cliente: <codice>
nome: <nome esteso>
fase: avvio | regime | chiusura | fermo
dal: AAAA-MM-GG
fino_al: AAAA-MM-GG oppure vuoto
lingua_documenti: it
riservatezza: <una riga, oppure "standard">
aggiornato: AAAA-MM-GG
---

# <Nome>: scheda

Indice del sapere su questo cliente. Si legge per primo. I fatti stanno nei file indicati.

| Voce | Dove | Stato |
|---|---|---|
| profilo | `SAPERE.md` §1 | |
| persone | qui sotto | |
| mandato | qui sotto | |
| confini | qui sotto | |
| numeri | `SAPERE.md` §2 | |
| segmenti | `SAPERE.md` §3 | |
| personas | `SAPERE.md` §4 | |
| offerta | `SAPERE.md` §5 | |
| messaggio | `SAPERE.md` §6 | |
| concorrenti | `SAPERE.md` §7 | |
| canali | `SAPERE.md` §8 | |
| gap | `SAPERE.md` §9 | |

**Stato dell'ingaggio**: `STATO.md`, `PROMESSE.md`
**Call**: `CALL.md`
**Fonti e accessi**: <quali strumenti del cliente si possono leggere, con quale account, chi concede l'accesso>

## Persone
- <ruolo>: <cosa decide, come preferisce lavorare>

## Mandato
1. <cosa prevede l'accordo, per punti>

Fuori perimetro: <cosa non si fa>. La domanda che governa il lavoro: <una frase>.

## Confini
- <riservatezza tra persone, conflitti, cosa non entra nei documenti>
```

### `clienti/<codice>/SAPERE.md`

```markdown
# <Nome>: sapere

Fatti con data, fonte ed etichetta (VISTO, DETTO, CALCOLATO, IPOTESI, NON VERIFICABILE).
Due fonti che divergono si scrivono entrambe. Ultimo aggiornamento: <data>.

## 1. Profilo
## 2. Numeri, in fila per data
| Data | Numero | Valore | Fonte | Etichetta |
|---|---|---|---|---|

## 3. Segmenti
## 4. Personas
## 5. Offerta e prezzi
## 6. Messaggio
## 7. Concorrenti e alternative
## 8. Canali
## 9. Gap e domande aperte
| ID | Cosa manca | Chi lo ha | Cosa blocca |
|---|---|---|---|
```

### `STATO.md`, `PROMESSE.md`, `CALL.md`

```markdown
# <Nome>: stato
**Ultimo aggiornamento:** AAAA-MM-GG (<cosa è cambiato, una riga>)
## Dove siamo
## Aperti (massimo 7, con data)
## Scadenze fisse
## Decisioni prese
## File prodotti
```

```markdown
# <Nome>: promesse
## Promesse mie
| Data | Promessa | A chi | Entro | Stato |
|---|---|---|---|---|
## Aspetto da altri
| Data | Cosa | Da chi | Entro | Stato |
|---|---|---|---|---|
```

```markdown
# <Nome>: call
## AAAA-MM-GG, <con chi>
Deciso: ...
Aperto: ...
Frase da ricordare: "..."
```

## Esempio

Esempio inventato: azienda, persone e numeri non esistono e servono solo a mostrare il formato.

Una torrefazione che vende caffè e macchine a bar e uffici firma un incarico di tre mesi per rimettere ordine nelle vendite. Dopo le sei domande, la scheda si apre così:

```markdown
---
cliente: torrefazione-alfa
nome: Torrefazione Alfa (inventata)
fase: avvio
dal: 2025-03-03
fino_al: 2025-05-30
lingua_documenti: it
riservatezza: titolare e direttore vendite sentiti separatamente
aggiornato: 2025-03-04
---

| Voce | Dove | Stato |
|---|---|---|
| profilo | `SAPERE.md` §1 | completo |
| numeri | `SAPERE.md` §2 | fatturato VISTO, clienti attivi DETTO |
| segmenti | `SAPERE.md` §3 | ipotesi, da verificare sull'elenco clienti |
| concorrenti | `SAPERE.md` §7 | manca, li conosce il direttore vendite |
| gap | `SAPERE.md` §9 | 3 aperti |
```

E in `SAPERE.md` la divergenza tra due fonti resta scritta:

```markdown
| Data | Numero | Valore | Fonte | Etichetta |
|---|---|---|---|---|
| 2025-03-03 | Clienti attivi | "circa 200" | call con il titolare | DETTO |
| 2025-03-10 | Clienti attivi | 164 | elenco fatture ultimi 12 mesi | VISTO |
```

## Errori da evitare

- Aprire una seconda cartella per un cliente che ne ha già una con un altro nome. Si controlla l'elenco prima di creare qualsiasi cosa.
- Scrivere fatti nella scheda. La scheda punta, i fatti stanno in `SAPERE.md`.
- Lasciare una voce vuota. Una voce senza contenuto dice `manca` e chi ha il dato.
- Riempire un gap con una stima presentata come dato. Le stime si etichettano IPOTESI.
- Riordinare i file di un cliente esistente senza che sia stato chiesto. L'allineamento scrive la scheda e basta.
- Copiare lo stesso numero in tre file. Al primo aggiornamento due copie restano vecchie.
- Mettere nella scheda lo stato della settimana. Le cose che cambiano ogni settimana stanno in `STATO.md`.
- Creare una skill dedicata a un cliente al primo lavoro. Finché un lavoro non si è ripetuto tre volte bastano la scheda e le skill generiche (vedi `da-richiesta-a-skill`).

## Se non puoi scrivere file

In una conversazione senza accesso a una cartella, produci il contenuto di ogni file in un blocco separato con il suo percorso in testa, e chiedi all'utente di salvarlo. Alla conversazione successiva l'utente incolla la scheda e si riparte da lì.
