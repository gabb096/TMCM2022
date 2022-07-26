# STILL IN PROGRESS


## Turning the Akay APC key25 into a drum machine using pure data.

This project originated as an exam for the "Technology for Midi and Computer Music" course.
The purpose was to create a pure data patch, which was able to make the APC Key25 MIDI controller a real Drum Machine, which could operate without the aid of the screen, taking advantage of the multitude of buttons on the unit.

### The sounds

Using the `SOFT KEYS` in the `SCENE LAUNCH` section you can select one of 5 different sounds such as:

* Kick drum:
* Snare drum;
* Hit-Hat;
* Still thinking...
* Bass.

Each one is synthesized from scratch (no sample is used) and has up to 8 parameters to tweak it.

You can play each one of the sound at any time. 
The drums are located in the bottom row of the matrix, in order from left to right we have Kick, Snare, Hit-Hat, empty-for-now, and then they repeat in the same order.
You can play the bass with the keyboard.

While one of the sounds is selected via the `SOFT KEYS`, we can use the first 4 rows of the button array to input the sound in the sequencer:
By pressing one of the matrix buttons we enter the position in the sequence.
By pressing one of the round button on the bottom of the matrix we can select the volume of the single note.

### The sequencer