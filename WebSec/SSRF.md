# Server Side Request Forgery

Vulnerabilità di sicurezza che si verifica quando un'applicazione Web permette a un utente di influenzare le richieste fatte dal server a sistemi esterni. 
Questo significa che un aggressore può forzare il server a fare richieste non autorizzate verso risorse a cui non dovrebbe avere accesso, come server interni, servizi cloud o risorse locali.

# Payload
Tipicamente gli attacchi si basano su richieste ad endpoint che permettono di accedere al server stesso, come: 

```
127.0.0.1  , 0.0.0.0 , localhost e rappresentazioni alternative
```
I WAF solitamente bloccano queste richieste, ma possono esserci delle possibilità di bypassare i WAF con determinati playload

[SSRF WAF Bypass](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Request%20Forgery/README.md)

# Open Redirect

Quando non è possibile bypassare il controllo sull'indirizzo inserito potrebbe essere possibile effettuare un redirect a questi indirizzi.
Non è detto che funzioni, ma potete provarci creando un vostro sito (ngrok o simili) o con siti che permettono di creare link a cui fare redirect come : 

[Bitly](https://app.bitly.com)

# Errori di Parsing
Possono esserci degli errori tra le funzioni che effettuano la conversione dei link in indirizzi (o che li validano) ed il metodo che effettua le richieste
Per scoprirne di più visitate: 

[Abusing Url Parser](https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf)

Esistono tecniche più sofisticate, ma non vengono trattate alla cyberchallenge. Per scoprirle visitate: 

[DNS Rebinding](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/DNS%20Rebinding)
