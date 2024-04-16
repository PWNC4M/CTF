# Cross Site Request Forgery

Il CSRF, o Cross-Site Request Forgery, è una vulnerabilità che si verifica quando un utente autenticato involontariamente esegue azioni non autorizzate su un sito web. 

Questo accade perché un attaccante riesce a indurre l'utente a eseguire delle azioni senza il suo consenso, sfruttando la sessione autenticata dell'utente su un altro sito.

Ecco come funziona tipicamente un attacco CSRF:

    Autenticazione dell'utente: L'utente si autentica su un sito web legittimo, ottenendo una sessione valida.

    Costruzione del payload: L'attaccante prepara un payload, solitamente sotto forma di un link o un form nascosto, che eseguirà azioni non autorizzate sul sito web bersaglio.

    Inganno dell'utente: L'attaccante convince l'utente a fare clic su un link o a visitare una pagina che contiene il payload, nelle CTF è molto probabile che questo avvenga tramite XSS.

    Esecuzione dell'azione non autorizzata: Poiché l'utente è già autenticato sul sito web bersaglio, il browser invia automaticamente le richieste HTTP contenute nel payload. Queste richieste sembrano provenire dall'utente legittimo e possono eseguire azioni come cambiare la password, modificare le impostazioni dell'account o restituire la flag.

# Esempio di attacco

Ecco un esempio concreto di come un attacco CSRF potrebbe essere eseguito:

Supponiamo che Bob sia autenticato su un sito web di banca online. L'attaccante sa che Bob ha un account su questo sito. Crea quindi una pagina web (NGROK o simili) che contiene un modulo nascosto che trasferisce denaro dal conto di Bob al suo stesso conto, ad esempio:

```
<form action="http://www.bankingwebsite.com/transfer">
  <input type="hidden" name="toAccount" value="Eve">
  <input type="hidden" name="amount" value="1000">
  <input type="submit" value="Vai al link per il trasferimento">
</form>
```

Senza che Bob sia consapevole di ciò, il denaro viene trasferito dal suo conto a quello dell' attaccante. Non è che raro che questo avvenga tramite XSS, capita spesso che nelle challenge jeopardy bisogni effettuare un attacco CSRF+XSS

# CSRF Token
Per prevenire gli attacchi CSRF, è fondamentale implementare misure di sicurezza come l'utilizzo di token CSRF univoci per ogni richiesta.
Chi costruisce il payload non può (o non dovrebbe) conoscere questi token, se viene effettuata una richiesta ad un endpoint senza un CSRF token valido questa richiesta viene rifiutata.
