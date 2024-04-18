# PwnDbg

Ricerca una striga (di solito la shell) per ottenerne l'indirizzo:

```
 search -t string "/bin/sh" 
```

# Leak
I leak, ottenuti in qualsiasi modo, vanno eseguiti nel seguente modo:

```
base = leak() - leak_off
gadget1 = base + gadget1_off
gadget2 = base + gadget2_off
ecc....
```
