Conway's Game Of Life, for the R4 Uno WIFI board.

   DO NOT CONNECT A LOUDSPEAKER TO AN ARDUINO R4 - YOU WILL DAMAGE THE ARDUINO
   You need to use an amplifier.

This code plays the game, and on each generation it scans the LED patterns and turns them into music notes in the scale of C major on the analogue output pin A0. The serial monitor should be set to a baud rate of 115200 baud from the drop down menu. Use or remove comments // for lines that start with a Serial.Print to control what feedback you see in the serial monitor window.

Unlike other R4 sound examples that use the analogWave.h library, this code does things correctly by using a fractional increment through a look up table and this permits the sample rate to be anything you want. Here it is set to CD quality of 44100 samples per second, something you can't do with the analogWave.h library.

The pin A0 should be connected to a capacitor with the other end connected to an audio jack socket. This can then be plugged into an amplifier so you can hear the notes played.
See Fig1 for the circuit of this.

The first 6 LEDs in the X axis cover 6 octaves and the next 6 positions repeat this pattern, see Fig 2.

The waveform used to generate the notes is defined at line 35 of the main code. Basically you specify the fundamental to 5th harmonic, in the proportion you want them mixing in the call to the generateTable function. This is like defining the stops on a Church Organ and the sound is something similar. This is because this is a static sound, that means that nothing changes during the note being sounded. Typically a sound might change its amplitude, by using some sort of envelope generator, and a real sound would also change the mix of harmonics as the tone progresses. These are all possible, but that is for another project.

As the notes play for fixed durations, there would normally be a click heard when a note stops. However, here I have implemented a function to restore the DC bias level when a note stops, which eliminates clicks. See Fig 3, 4, & 5 for oscilloscope traces.

The code uses MIDI numbers to represent notes, but uses nothing else about MIDI.

Things you can play about with in the Sound.h tab:-
The length of the note and the space between nots is set in lines 12 & 13 of the 
The Musical scale of the output is defined in line 5.
The volume of the sound output is defined in line 3, make this less than 1.0 to make it smaller, to say match the input requirement of your amplifier. Greater than 1.0 will cause distortion, but you might like the effect.

Things you can play about with in the Matrix.h tab:-
The daly between generational turns in line 6.
You can add extra patterns or modify existing ones. Line 13 states how many and the names should be listed in the pattern names function at line 36. As well as a defining start pattern matrix after line 100.
Line 34 defines the first pattern to use after reset.
Line 16 defines how many patterns without change will cause the next pattern to be played.
Line 10 defines the maximum number of generations before a reset. Without this then a pattern that finishes in a blinking pattern would never end. For example the "Die hard" pattern ends in a four stage blinking pattern, that eventually ends by exceeding the maximum number of generations. Conway's game assumed an infinite grid, where as this version assumed hard edges with no counting of neighbours outside the matrix. Other implementations take a wrap round approach. where say a check on right most cell results the left most cell being checked.  

Things you can play about with in the main tab:-
The for loops in lines 47 & 48 can be swapped over to change the order the notes are output from the pattern. As written notes are produced down in the Y direction and then the next octave in the X direction is scanned.

You are encouraged to extend this work and perhaps share any changes on the Arduino Forum.
     