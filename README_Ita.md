# DA FINIRE
# Trasformare una Akay APC key25 in una drum machine utilizzando pure data

Questo progetto nasce come un esame per il corso di "Tecnologie per il MIDI e la Computer Music". 
Lo scopo è quello di creare una patch pure data che fosse in grado di rendere il controller MIDI "Akay APC key25" in una vera e propria drum machine che potesse essere utilizzata senza l'ausilio dello schermo del computer che ospita la patch, ma utilizzando come input visivo i vari tasti luminosi presenti sull'unità.

---

## La drum machine in breve
Il controller Akay è composto da:

* 40 bottoni rettangolari posizionati in una matrice 8x5;
* 14 bottoni rotondi ;
* 8 manopole;
* 6 bottoni rettangolari al di sotto dei pomelli.
* Una tastiera da 25 tasti.

Tutti questi controlli tramite la patch pure data diventano:

* Uno step sequencer da 32 passi, ottenuto dalle prime 4 righe della matrice di bottoni rettangolari.
* Una riga dove poter suonare i singoli strumenti;
* Selettore di pattern;
* Selettore di strumenti;
* Modificatori per modificare i singoli strumenti;
* Comandi generali.

![](img/ApcKey25Label.jpg) 

## Come utilizzarla
Collegare la tastiera al computer, aprire la patch "main.pd" e selezionare il comando "dsp on" su pure data.

Ora è tutto pronto per suonare.

Selezionare uno degli strumenti tramite i tasti segnati come `Instrument Selector` nell'imagine precedente. 
I primi tre sono suoni percussivi, in ordine abbiamo Kick, Snare, HitHat, il quarto è un `?? ??` e funzionano tutti allo stesso modo. Per inserire o togliere una nota ON/OFF basta premere su uno dei tasti dello step sequencer e il relativo led indicherà se la nota è stata aggiunta o eliminata.
Il quinto suono è un basso synth, di default premere su un bottone del sequencer inserisce una nota OFF, per inserire una nota ON+PITCH bisogna tenere premuto il corrispettivo tasto sulla tastiera.

Una volta selezionato il suono e inserita la sequenza possiamo crearne altre cambiando pattern, per farlo basta un dei tasti segnati come `pattern selector` nell'immagine. 
Ci sono 8 pattern per ogni suono.
Per sentire il pattern attualmente in modalità play pasta premere il tasto `PLAY/PAUSE`. Di default viene riprodotto il pattern #1 di ogni suono.
Se nessuno strumento è selezionato vedremo nell'area dedicata al sequencer un led che indica a quale step ci troviamo.
Per sentire un nuovo pattern, selezionare prima il suono poi contemporaneamente il tasto `STOP ALL CLIPS` e il tasto relativo al pattern.
Per eliminare l'intero pattern premere il tasto `SUSTAIN`.

Quando un suono è selezionato possiamo modificarne alcuni parametri tramite le 8 manopole. 
Ogni suono ha parametri diversi, ma tutti hanno in comune il comando del volume comandato dall'ultima manopola, posizionata nella fila in basso tutto a destra.
Per tornare ai parametri di default premere `SHIFT`.

## I suoni



## Gli effetti


## La patch

### main.pd

### sequencer.pd