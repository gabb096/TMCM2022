# Trasformare una Akay APC key25 in una drum machine utilizzando pure data

Questo progetto nasce come esame per il corso di "Tecnologie per il MIDI e la Computer Music". 
Lo scopo è quello di creare una patch pure data che sia in grado di rendere il controller MIDI "Akay APC key25" in una vera e propria drum machine che potesse essere utilizzata senza l'ausilio dello schermo del computer che ospita la patch, ma utilizzando come input visivo i vari tasti luminosi presenti sull'unità.

---

## La drum machine in breve
Il controller Akay è composto da:

* 40 bottoni rettangolari posizionati in una matrice 8x5;
* 14 bottoni rotondi ;
* 8 manopole;
* 6 bottoni rettangolari al di sotto delle manopole.
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
I primi quattro sono suoni percussivi, in ordine abbiamo Kick, Snare, HitHat e Ride e funzionano tutti allo stesso modo. Per inserire o togliere una nota ON/OFF basta premere su uno dei tasti dello step sequencer e il relativo led si illuminerà di rosso se se la nota è stata aggiunta o si spegne se la nota è stata eliminata.
Il quinto suono è un basso synth, di default premere su un bottone del sequencer inserisce una nota OFF, per inserire una nota ON+PITCH bisogna tenere premuto il corrispettivo tasto sulla tastiera e poi premere dove posizionare la nota.

Una volta selezionato il suono e inserita la sequenza possiamo crearne altre cambiando pattern, per farlo basta premere un dei tasti segnati come `pattern selector` nell'immagine. 
Ci sono 8 pattern per ogni suono.
Per sentire il pattern attualmente in modalità play pasta premere il tasto `PLAY/PAUSE`. Di default viene riprodotto il pattern #1 di ogni suono.
Quando la sequenza parte il passo in cui ci troviamo nello step sequencer viene illuminato di giallo.
Per sentire un nuovo pattern, selezionare prima il suono poi contemporaneamente il tasto `STOP ALL CLIPS` e il tasto relativo al pattern.
Per svuotare l'intero pattern premere il tasto `SUSTAIN`.

Quando un suono è selezionato possiamo modificare fino a 8 parametri per personalizzare il suono, tramite le manopole. 
Ogni suono ha parametri diversi, ma tutti hanno in comune il comando del volume posizionato sull'ultima manopola, (fila in basso tutto a destra).

Per tornare ai parametri di default premere `SHIFT`.

Infine la patch permette di registrare sul file `DrumMachineRec.wav` la propria esibizione. 
Per farlo basta premere una volta il tasto `REC` per far partire la registrazione per poi premerlo nuovamente quando si vuole interrompere la registrazione.


### Parametri dei Suoni

|Kick |Snare |HitHat |Ride |Basso |Effetti |
|:--  |:--   |:--    |:--  |:--   |:--     |
|Altezza |Accordatura |Attacco |Tonalità |Attacco |BPM |
|Tono |Altezza |Decadimento |Cutoff Passa Basso |Hold |Cutoff Passa Alto |
|Attacco |Decadimento |Cutoff Passa Alto |Cutoff Passa Alto |Decadimento |Cutoff Passa Basso |
|Decadimento |Rumore |Quantità Random |Decadimento |Wavefolding |Tastiera ON/OFF |
|Cutoff Passa Basso |Cutoff Passa Basso |Seme Random |Riverbero |Cutoff Passa Basso |Salta Step |
|Wavefolding |Saturazione | // | //  |Chorus |Ripeti Step |
|Rumore |//  | //  | //  |Riverbero |Saturazione |
|Volume |Volume |Volume |Volume |Volume |Volume Master|

## La patch

### main.pd
Questa è la patch principale che contiene tutte le altre.
Per prima cosa notiamo l'oggetto [softKeySelector], il cui compito è quello di restituire un numero da 0 a 5 in base a quale strumento è selezionato dall'utente :
 
 * 0 = Effetti
 * 1 = Gran cassa
 * 2 = Rullante
 * 3 = Piatto Hithat
 * 4 = Piatto Ride
 * 5 = Basso Synth

Questo numero viene passato ad ogni strumento. Quando lo strumento è selezionato si possono utilizzare i pomelli per modificarne i parametri.
Gli strumenti percussivi ricevono un bang ogni qual volta che devono sintetizzare il proprio suono. 
Il basso synth riceve invece il numero relativo alla nota da suonare seguendo il protocollo MIDI.
Tali bang e numeri vengono gestiti dall'oggetto [sequencer].

### sequencer.pd

Questa patch si occupa di tutta la meccanica della drum machine.
Il cuore del sequencer è l'oggetto [metro] che tramite la subpatch [pd counter] indica a quale passo della sequenza ci troviamo. 
Il numero del passo va nelle subpatch [pd seqTrig] e [pd sequencerLight].

##### pd seqTrig
Qui ci occupiamo di inviare all'outlet diretto agli strumenti l'informazione su quando sintetizzare il proprio suono. 
Di fatto legge per ogni strumento uno degli 8 array ad esso assogiato e quando arriviamo al penultimo passo della sequenza si occupa anche di cambiare il pattern da riprodurre se necessario.

##### pd sequencerLight
Questa subpatch si occcupa completamente dell'interfaccia con l'utente.
Ogni subpatch all'interno si occupa di una funzione specifica:

* **[pd instSelector]**
Come suggerisce il nome illumina o spenge i LED adibiti al selettore di strumento quando lo strumento viene selezionato.
* **[pd stepIndicator]**
Quando nessuno strumento è selezionato questa subpatch si occupa di illuminare lo step attuale della sequenza.
* **[pd sequenceInterface]**
Quando uno strumento è selezionato questa subpatch mostra il pattern selezionato accendendo i relativi LED. 
* **[pd seqNoteIn]** 
Si occupa di scrivere negli array e accandere/spegnere le note inserite dall'utente.