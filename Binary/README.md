# PwnCollege
Permette di esercitarsi su software security, da livelli più bassi della CyberChallenge fino a superarla (es: Kernel pwn) 

Inoltre trovate video di spiegazione ed introduzione alle vulnerabilità:

[PwnCollege](www.pwn.college) 

# Repository e Paper
Esistono infinite repository e paper per l'exploit in binary security, fare molte pwn è l'unica cosa che vi migliorerà. 

Una Repo che ho trovato interessante è: 

[Binary Sec Repository](https://ir0nstone.gitbook.io/notes) 

Sono presente anche Heap e Kernel, ma la CC si ferma al pwn dello Stack(32 e 64 bit)(X86 equivale a dire 64 bit)

Vi linko anche: 

[CTF 101](https://ctf101.org/)

Non tratta solo pwn, vi consiglio di guardare reverse e binary exploitation. 

Conoscere determinate funzione assembly è molto consigliato, trovate un crash course qui (niente di pesante ne di programmazione) :

[Assembly Crash Course](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://medium.com/reverse-engineering-for-dummies/a-crash-course-in-assembly-language-695b07995b4d&ved=2ahUKEwiqvt_Q98iFAxWj3gIHHSTaB8AQFnoECBMQAQ&usg=AOvVaw33Q7YbBMyZzQGxU5SjybNr)

Dovete necessariamente conoscere il funzionamento dello Stack (64 bit si basa su 32 ma con i registri)

Qui trovate un video che spiega il funzionamento dello stack:

[Stack](https://www.youtube.com/watch?v=5iQkR69H_1M)

# Debugger

Vi consiglio di scaricare:

[GDB Download](https://sourceware.org/gdb/download/)

Tassivamente con l'estensione:

[PwnDBG](https://github.com/pwndbg/pwndbg)

[GDB Comandi Utili](https://docencia.ac.upc.edu/FIB/grau/CASO/lab2014/gdb-debug.pdf)

# Lista delle syscall 

[64 bit](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/)

[32 bit](https://x86.syscall.sh/)

[Tutte le syscall](https://syscalls.w3challs.com/)

# Sito che indica la versione della libc dato un leak

[Libc Database](https://libc.rip/)
