# Sistema del consulente

Sette skill per Claude che servono a organizzare il lavoro di chi segue più clienti insieme. Vengono dal modo in cui lavoro come Fractional CMO: uno spazio per cliente fatto sempre allo stesso modo, uno stato che si aggiorna dopo ogni call, le correzioni che diventano regole, una mappa di cosa Claude può chiudere da solo, un'apertura della giornata e un controllo a fine settimana.

Le ho ricavate dalle richieste che faccio davvero, contando quelle che tornano. Sono il metodo, senza i casi: gli esempi che trovi dentro sono inventati e lo dicono.

## Per chi è

Per consulenti, freelance e manager a tempo parziale che lavorano con più aziende e usano Claude tutti i giorni. Le skill risolvono due problemi che conosce chiunque lavori così: il contesto da rispiegare a ogni conversazione e le promesse fatte in call che si perdono. Un terzo arriva con l'uso, ed è lo stesso errore corretto più volte.

Bastano Claude e una cartella di lavoro, senza saper programmare.

## Cosa c'è

| Skill | A cosa serve |
|---|---|
| `spazio-cliente` | Apre lo spazio di un cliente nuovo: cartella, scheda a dodici voci che dice dove vive ogni pezzo del sapere su quel cliente, file dei fatti con data e fonte, un solo elenco dei clienti. Allinea anche un cliente che ha già materiale sparso |
| `stato-ingaggio` | Tiene lo stato dell'ingaggio: dove siamo, cosa è aperto, promesse fatte e cose attese dagli altri. Si aggiorna dopo ogni call e prepara la successiva |
| `correzione-in-regola` | Trasforma una correzione in una regola scritta. Tre tipi: stile (con una lista nera di partenza delle frasi che suonano scritte da una macchina), fatti, comportamento. Un errore corretto due volte a mano diventa una regola |
| `chi-approva-cosa` | La mappa dell'autonomia per tipo di output: cosa Claude chiude da solo, cosa va in bozza, cosa richiede sempre un sì. Tiene la coda delle bozze in attesa |
| `piano-del-giorno` | Apre la giornata con una domanda sola su ciò che è scaduto o fermo, propone tre priorità, chiude con un impegno per il giorno dopo |
| `controllo-settimanale` | Nove controlli sulle incoerenze della cartella, tre interventi scelti, verifica la volta dopo. Una volta al mese un controllo di salute con otto misure |
| `da-richiesta-a-skill` | Decide quando una richiesta che torna merita una skill, e la scrive separando il metodo dai fatti del cliente |

## Come stanno insieme

Le skill scrivono e leggono file di testo in due cartelle. Ogni skill crea i file che le servono da un modello che porta con sé, quindi funzionano anche una alla volta.

```
clienti/
  ELENCO.md              l'unico elenco dei clienti
  <codice>/
    SCHEDA.md            l'indice a dodici voci
    SAPERE.md            i fatti, con data, fonte ed etichetta
    STATO.md             dove siamo e cosa è aperto
    PROMESSE.md          impegni nei due sensi
    CALL.md              una voce per call
    ricevuti/  bozze/  archivio/
sistema/
  STILE.md               la lista nera di stile
  CORREZIONI.md          registro delle correzioni e coda da verificare
  AUTONOMIA.md           chi approva cosa
  IN_ATTESA.md           bozze che aspettano un sì
  GIORNATE.md            aperture e chiusure
  CONTROLLI.md           esito dei controlli
  RICHIESTE.md           richieste che tornano
```

Quattro principi tengono insieme il tutto:

1. Un fatto, una casa. Un dato si scrive in un posto solo e il resto lo cita.
2. Ogni numero ha una data, una fonte e un'etichetta che dice se è stato visto, detto, calcolato o ipotizzato.
3. Le regole che durano stanno nel file di istruzioni, lo stato che cambia ogni settimana sta nei file di stato.
4. Niente esce dalla cartella senza un sì esplicito.

## In che ordine adottarle

Una alla volta, lasciando passare almeno una settimana tra l'una e l'altra.

1. `spazio-cliente`, sul cliente su cui lavori di più. Per gli altri basta l'allineamento, che scrive la scheda senza spostare nulla.
2. `stato-ingaggio`, da usare dopo ogni call per due settimane.
3. `correzione-in-regola`, a partire dalla lista nera di stile. È la parte che si nota prima.
4. `chi-approva-cosa`, quando cominci a far produrre a Claude documenti che escono verso i clienti.
5. `piano-del-giorno`, quando almeno tre clienti hanno lo stato aggiornato. Prima non ha niente da leggere.
6. `controllo-settimanale`, dopo un mese di uso.
7. `da-richiesta-a-skill`, quando ti accorgi di chiedere lo stesso prompt per la seconda volta.

## Prerequisiti

- Claude con le skill attive: Claude Code oppure claude.ai.
- Una cartella di lavoro che Claude possa leggere e scrivere. In una conversazione senza accesso ai file le skill funzionano lo stesso in forma ridotta: producono il contenuto dei file in blocchi da salvare a mano, e ogni skill spiega come.
- Non servono script, connettori o attività programmate. Chi ha modo di programmare attività ricorrenti può agganciare l'apertura della giornata e il controllo settimanale.
- Le skill sono scritte in italiano e producono file in italiano.

Alcune skill propongono di aggiungere due o tre righe al file di istruzioni del progetto (`CLAUDE.md` in Claude Code, le istruzioni del progetto su claude.ai), perché la lista di stile e la mappa dell'autonomia vengano lette a ogni conversazione. Le righe sono scritte nella skill e si aggiungono solo con il tuo sì.

## Come si installa

Copia la cartella della skill che ti serve (per esempio `skills/spazio-cliente`) dentro `.claude/skills/` del tuo progetto. In alternativa comprimi la cartella e caricala come skill su claude.ai. Ogni skill dice nella descrizione quando attivarsi, quindi dopo basta chiedere: "nuovo cliente", "aggiorna lo stato dopo la call", "piano di oggi".

`correzione-in-regola` ha una sottocartella `references/` con la lista nera di partenza: va copiata insieme al suo `SKILL.md`.

## Cosa non fanno

Lavorano su quello che c'è nella cartella e su quello che incolli nella conversazione: posta, calendario e CRM restano fuori, e niente viene inviato o pubblicato. I metodi di marketing e di vendita stanno in un altro repository, quello delle skill di strategia e go-to-market.

## Licenza

CC BY 4.0. Puoi usarle, modificarle e ridistribuirle, anche per lavoro, citando l'autore.

Lorenzo Asuni
