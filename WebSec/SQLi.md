Consiglio di non usare sqlmap, prima cercate di capire cosa avviene

# SQLi
L'SQL injection è una vulnerabilità di sicurezza che si verifica quando un'applicazione web non sanifica correttamente l'input dell'utente prima di utilizzarlo in una query SQL. Questo consente di inserire codice SQL nelle query per manipolare il database o ottenere informazioni sensibili.
ESEMPI DI CODICE 
Di seguito troviamo, in vari linguaggi, degli esempi di codice vulnerabili:
import sqlite3

```
def get_user_data(username):
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    query = "SELECT * FROM users WHERE username = '" + username + "'"
    cursor.execute(query)
    user_data = cursor.fetchone()
    conn.close()
    return user_data
```

La parte vulnerabile di questa query è ``` + username + ```, l'input deve essere sempre parametrizzato, mai passato direttamente nella query. 
```
<?php
$mysqli = new mysqli("localhost", "username", "password", "database");

$username = $_GET['username'];
$query = "SELECT * FROM users WHERE username = '$username'";
$result = $mysqli->query($query);
$user_data = $result->fetch_assoc();
?>
Query che non ha presente SQLi(python):
def get_user_data_safe(username):
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    query = "SELECT * FROM users WHERE username = ?"
    cursor.execute(query, (username,))
    user_data = cursor.fetchone()
    conn.close()
    return user_data
```

Potete notare ``` " ? " ``` e il fatto che sia presente ``` cursor.execute(query, (username,))``` questo indica di trattare la variabile username come testo, rendendo esplicito la sintassi SQL al database. Inserire parole chiave nella variabile username non avrà alcun effetto perchè verranno trattati come dei dati. Di seguito la soluzione per PHP: 
```
$stmt = $mysqli->prepare("SELECT * FROM users WHERE username = ?");
$stmt->bind_param("s", $username);
$stmt->execute();
$result = $stmt->get_result();
$user_data = $result->fetch_assoc();
```

# Exploit
 Potete trovare exploit SQL ovunque, generalmente basta essere a conoscenza della tabella ```information_schema ``` (una tabella che permette di ottenere informazioni sul databse tra cui il nome delle tabelle e il nome delle colonne) e saper costruire delle query SQL. Per trovare delle SQL injection si può inserire il carattere ``` ' ``` che romperà la query nel caso in cui ci sia una injection. Questo perchè la query costruita nel backend terminerà in questo modo: 
```
Query...... Where password = '''
```
Il nostro apostrofo chiude la query, generando un errore per via dell'ultimo apostrofo presente che è quello che racchiude i nostri dati
Ricordate che: L' apostrofo finale è sempre presente, potete commentarlo e costruire la vostra query gestendo la chiusura di essa, o sfruttarlo, generalmente è meglio commentarlo per non scordarsi di esso. I commenti standard (possono dipendere dal tipo di Database) sono ``` # e -- ```(-- genera un errore se non è presente uno spazio subito dopo). È buona prassi eseguire una SQLi di questo tipo:
```
QUERY PAYLOAD -- (commenta il resto)
```
# Payload 
Alcuni payload di esempio sono:
```
' OR '1'='1'
https://insecure-website.com/products?category=Gifts'-- (il payload è 
Gifts'-- )
```
per poter accedere a tutti i regali, tramite la query risultante: 
```
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
O per esempio: 
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```
# UNION
Union è un costrutto che permette di eseguire più query completamente. Nel caso in cui avessimo SQLi, ma su una query che non ci restituisce niente di utile, possiamo usarlo per creare una nuova query che esegua quello che vogliamo: 
```
' UNION SELECT username, password FROM users--
```
L' unico problema della UNION è che il numero di colonne stampate dalla ``` UNION SELECT ```deve equivalere a quello della SELECT precedente, possiamo ovviare a questo problema stampando numeri casuali, o usare operatori come ``` CONCAT() ```. 
Ottenere Informazioni
Possiamo ottenere informazioni sul databse in svariati modi, per esempio facendoci stampare la versione relativo ad esso. Questo può servirci per sapere su che database lavoriamo, in quanto ogni tipo di database avrà sintassi differenti (in base ai comandi) e quindi quando non avremo un errore sapremo su che database lavoriamo. Inoltre ci è molto utile la tabella information_schema
da cui possiamo ottenere le tabelle: 
```
SELECT * FROM information_schema.tables
```
le colonne:
```
SELECT * FROM information_schema.columns e ovviamente anche le colonne di una certa tabella.
```
Trovate le tecniche per esaminare un database in : 

[PortSwigger - Esaminare il Database](https://portswigger.net/web-security/sql-injection/examining-the-database)


Di seguito trovate anche un cheat-sheet per le SQLi: 
[PortSwigger - SQLi cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)

# Blind
Non sempre (quasi mai) il risultato delle query verrà stampato per intero. In questo caso possiamo usare l' operatore ```LIKE``` (o equivalenti) , assieme ad una ```SLEEP``` per  avere un oracolo da cui capire se l' informazione che stiamo cercando è presente o meno nel database
