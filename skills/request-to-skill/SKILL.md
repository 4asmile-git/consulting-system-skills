---
name: request-to-skill
description: >
  Decide quando una richiesta che torna merita una skill, e la scrive. Prima di produrre
  un prompt usa e getta controlla se il lavoro è già coperto da una skill esistente; alla
  seconda richiesta sullo stesso tema registra il candidato; alla terza propone la skill
  e la costruisce separando il metodo dai fatti del cliente. Serve anche per fare ordine
  tra troppe skill e per preparare un pacchetto da dare a un collega. Si attiva con frasi
  come "dammi il miglior prompt per", "costruiamo un prompt", "fallo come l'altra volta",
  "stesso formato che abbiamo usato per", "serve una skill per questo", "ha senso creare
  una skill o una cartella dedicata", "ho troppe skill", "quali skill mi mancano",
  "prepara un pacchetto di skill per".
license: CC-BY-4.0
---

# Da richiesta a skill

> **In una riga:** un prompt chiesto per la terza volta diventa una skill, e dalla seconda se ne tiene il conto.

## Quando usarla

Il segnale più frequente è una frase: "dammi il miglior prompt per". Chi la scrive spesso sta rifacendo un lavoro già fatto, per un altro cliente o un mese prima, e sta per pagare di nuovo il tempo di spiegarlo. L'altro segnale è "fallo come l'altra volta": il formato esiste già, ma vive in un documento vecchio insieme ai fatti di un cliente.

La skill fa tre cose:

1. Intercetta le richieste di prompt e controlla se il lavoro è già coperto.
2. Tiene il registro delle richieste che tornano.
3. Quando una richiesta ha i requisiti, scrive la skill.

## Cosa chiedere prima di partire

Davanti a una richiesta di prompt, niente: si controlla e si risponde. Quando si decide di scrivere una skill servono quattro cose.

1. Due o tre risultati passati dello stesso lavoro, anche imperfetti.
2. Cosa in quei risultati l'utente ha dovuto correggere a mano.
3. Chi la userà: solo l'utente, un collaboratore, persone esterne.
4. Quali fonti e strumenti sono sempre disponibili a chi la usa, e quali no.

## I passi

### 1. Davanti a una richiesta di prompt

Guarda l'elenco delle skill installate e `sistema/RICHIESTE.md` (se manca, crealo dal modello).

| Situazione | Cosa fare |
|---|---|
| Il lavoro è coperto da una skill | Dillo in una riga e usa la skill, con il contesto del cliente |
| Non è coperto, prima volta | Scrivi il prompt e aggiungi una riga al registro |
| Non è coperto, seconda volta | Scrivi il prompt, porta il contatore a due e segna la riga come candidata, con ciò che i due prompt hanno in comune |
| Non è coperto, terza volta | Proponi la skill al posto del terzo prompt |
| Il prompt serve a un altro strumento o a un'altra persona | Scrivilo e basta |

### 2. Il test: merita una skill

Quattro condizioni. Servono tutte.

| Condizione | Come si verifica |
|---|---|
| Si ripete | Almeno tre volte, oppure ha una cadenza fissa |
| Ha gli stessi passi | Le due o tre esecuzioni passate seguono la stessa sequenza |
| Ha un formato riconoscibile | I risultati passati si somigliano nella struttura |
| Il metodo si separa dal caso | Tolti i fatti del cliente, resta qualcosa da scrivere |

Se il lavoro si ripete solo per un cliente e meno di tre volte, non serve una skill: basta una nota nella scheda di quel cliente con il formato da seguire. Lo stesso vale per la domanda "serve una cartella o uno spazio dedicato": lo spazio si apre quando il tema ha materiale suo e richieste che tornano, non per ogni conversazione lunga.

Una prova rapida per capire se il metodo è separato dal caso: lo daresti a un altro progetto senza modifiche.

### 3. Estrarre il metodo

1. Metti uno accanto all'altro i risultati passati.
2. Segna ciò che è uguale in tutti: passi, sezioni, criteri di qualità, domande fatte all'inizio. Questo è il metodo.
3. Segna ciò che cambia: nomi, numeri, settore, tono. Questo è il caso, e resta fuori dalla skill.
4. Recupera le correzioni fatte a mano dall'utente: diventano la sezione degli errori da evitare.

Quando la richiesta è "stesso formato usato per un altro cliente", il risultato di questo passo è un modello vuoto. Il documento dell'altro cliente non si copia e non si cita.

### 4. Scrivere la skill

Una cartella con il nome in minuscolo e trattini, e dentro `SKILL.md` dal modello in fondo. Sei parti:

1. Intestazione con nome e descrizione. La descrizione contiene le frasi che l'utente dice davvero quando chiede quel lavoro, prese dalle richieste passate.
2. Quando usarla, e quando no.
3. Cosa chiedere prima di partire, in un solo messaggio.
4. I passi, nell'ordine in cui si fanno.
5. I modelli dei file che la skill crea.
6. Gli errori da evitare.

La skill legge il contesto del cliente dalla sua scheda e non contiene fatti di clienti. Non dipende da file, strumenti o accessi che chi la usa potrebbe non avere: se le serve un file, lo crea da un modello che porta con sé.

### 5. Provarla

Usala una volta su un caso vero e una volta su un caso inventato. Le prime correzioni dell'utente si scrivono subito nella skill, non nella risposta. Aggiorna la riga del registro con lo stato `skill` e il nome.

### 6. Fare ordine tra troppe skill

A "ho troppe skill" o "quali skill mi mancano" rispondi con una tabella: nome, a cosa serve in una riga, ultima volta usata, sovrapposizioni. Poi tre proposte al massimo:

- unire due skill che si attivano con le stesse frasi;
- ritirare quelle non usate da due mesi, spostandole in una cartella di archivio;
- scrivere quelle che il registro indica come candidate.

Una copia della stessa skill per ogni cliente è quasi sempre un errore: il metodo sta in una skill sola e le differenze stanno nelle schede dei clienti.

### 7. Quando la skill esce dalla tua cartella

Per un collega, per il team di un cliente o per il pubblico, prima della consegna:

1. Togli nomi di clienti, persone e prodotti, numeri veri, date ed episodi riconoscibili.
2. Sostituisci gli esempi con esempi inventati e dichiarali tali.
3. Togli percorsi, indirizzi e riferimenti a strumenti che il destinatario non ha.
4. Aggiungi un file `PARTI_DA_QUI.md`: come si installa, le prime tre richieste da provare, cosa la skill non fa.
5. Rileggi ogni file per intero. Una ricerca per nome trova i nomi e non trova i fatti: un episodio si riconosce anche senza il nome di chi lo ha vissuto.

## Modelli

### `sistema/RICHIESTE.md`

```markdown
# Registro delle richieste che tornano

| Tema | Prima volta | Ultima volta | Volte | Cosa hanno in comune | Stato |
|---|---|---|---|---|---|
| | AAAA-MM-GG | AAAA-MM-GG | 1 | | prompt / candidata / skill: <nome> / nota nella scheda |
```

Nel registro i temi si scrivono senza il nome del cliente: "confronto dei preventivi dei fornitori", senza dire per chi.

### Scheletro di `SKILL.md`

```markdown
---
name: <nome-in-minuscolo>
description: >
  <Cosa fa in una frase. Cosa produce. Si attiva con frasi come "...", "...", "...".>
---

# <Titolo>

> **In una riga:** <il risultato per chi la usa>

## Quando usarla
## Cosa chiedere prima di partire
## I passi
## Modelli
## Errori da evitare
```

## Esempio

Esempio inventato: richieste e clienti non esistono.

```
Utente: dammi il miglior prompt per confrontare i preventivi dei tre fornitori del cliente B
Claude: È la terza volta che torna questo lavoro (10/02 per il cliente A, 03/03 per il
cliente B). Le due versioni precedenti hanno gli stessi cinque passi e la stessa tabella
finale. Ti propongo di farne una skill, "confronto-preventivi", che legge il
contesto dalla scheda del cliente. Mi servono i due risultati passati e le correzioni che
hai fatto a mano. Se preferisci, oggi scrivo comunque il prompt e la skill la facciamo dopo.
```

## Errori da evitare

- Scrivere una skill alla prima richiesta. Non si sa ancora cosa è metodo e cosa è caso.
- Scrivere il terzo prompt usa e getta sullo stesso tema.
- Rispondere a "dammi il miglior prompt" con un prompt quando esiste già una skill che fa quel lavoro.
- Mettere nella skill i fatti del cliente da cui è nata.
- Scrivere descrizioni generiche. Senza le frasi vere dell'utente la skill non si attiva quando serve.
- Costruire una skill che funziona solo con uno strumento o un accesso che domani potrebbe mancare.
- Creare una skill per cliente quando basta una skill e una scheda per cliente.
- Consegnare una skill a terzi dopo aver cercato solo i nomi.

## Se non puoi scrivere file

Il registro si tiene in un blocco che l'utente salva. La skill nuova si produce come testo di `SKILL.md` da copiare in una cartella con lo stesso nome.
