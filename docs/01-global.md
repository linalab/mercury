# Global Settings (set)

## tempo

Change the global tempo in Beats Per Minute (BPM), counted in quarter-notes. Second argument sets a ramptime in milliseconds to gradually change the tempo over the provided amount of time (*!WARNING: experimental and may lag/glitch!*)

**arguments**
- {Number+} -> The BPM as a positive number
- {Number} -> The ramptime (optional/experimental)

```java
set tempo 128

set tempo 80 5000
```

## scale

Set the scale in a 12-TET system for which all the played notes will be mapped to. An optional second argument sets the tone-center (or root) for the scale. The default scale and root is `chromatic c`

**arguments**
- {Name} -> the scale name
- {Name} -> the root (optional, default=c)

```java
set scale major D#

set scale minor_harmonic Eb
```

Currently available scales are:
```
"chromatic" :            [0, 1, 2, 3, 4, 5, 6, 7, 8, 9,  10, 11],
"major" :                [0, 0, 2, 2, 4, 5, 5, 7, 7, 9,  9,  11],
"minor" :                [0, 0, 2, 3, 3, 5, 7, 7, 8, 8,  10, 10],
"minor_melodic" :        [0, 0, 2, 3, 3, 5, 7, 7, 9, 9,  11, 11],
"minor_harmonic" :	     [0, 0, 2, 3, 3, 5, 7, 7, 8, 8,  11, 11],
"dorian" :               [0, 0, 2, 3, 3, 5, 5, 7, 7, 9,  10, 10],
"phrygian" :             [0, 1, 1, 3, 3, 5, 7, 7, 8, 8,  10, 10],
"lydian" :               [0, 0, 2, 4, 4, 6, 6, 7, 7, 9,  11, 11],
"myxolydian" :           [0, 0, 2, 4, 4, 5, 5, 7, 7, 9,  10, 10],
"locrian" :              [0, 1, 1, 3, 3, 5, 6, 6, 8, 8,  10, 10],
"hungarian" :            [0, 0, 2, 3, 3, 6, 6, 7, 8, 8,  11, 11],
"gypsy" :                [0, 1, 1, 4, 4, 5, 5, 7, 8, 8,  11, 11],
"major_neapolitan" :     [0, 1, 1, 3, 3, 5, 7, 7, 8, 8,  11, 11],
"minor_neapolitan" :     [0, 1, 1, 3, 3, 5, 7, 7, 9, 9,  11, 11],
"hexatonic" :            [0, 0, 2, 2, 4, 4, 6, 6, 8, 8,  10, 10],
"hexatonic_blues" :      [0, 0, 2, 2, 4, 4, 6, 6, 7, 7,  10, 10],
"hexatonic_prometheus" : [0, 0, 2, 2, 4, 4, 6, 6, 9, 9,  10, 10],
"major_pentatonic" :     [0, 0, 2, 2, 4, 4, 7, 7, 7, 9,  9,  9],
"minor_pentatonic" :     [0, 0, 3, 3, 3, 5, 5, 7, 7, 10, 10, 10]
```

The naming convention and offsets for the roots are:
```
-6 gb Gb ges Ges
-5 g  G
-4 g# G# gis Gis
-4 ab Ab as  As
-3 a  A
-2 a# A# ais Ais
-2 bb Bb bes Bes
-1 b  B 
-1 cb Cb ces Ces
+0  b# B# bis Bis
+0  c  C
+1  c# C# cis Cis
+1  db Db des Des
+2  d  D
+3  d# D# dis Dis
+3  eb Eb es  Es
+4  e  E
+4  fb Fb fes Fes
+5  e# E# eis Eis
+6  f  F
```

## scalar

Scalar transposition, All the current notes are shifted up or down a certain amount of semitones but remaps the notes to the set scale. This is different from transposing the scales.

**arguments**
- {Int} -> scalar to shift notes by

```java
set scalar 2
```

## randomSeed

Set the random seed as integer for the psuedorandom number generators used in all functions across the environment. Setting the seed to a fixed integer will help make sure random values keep the same sequence every time you re-evaluate the code. A second optional argument resets the seed every n-bar, which can be useful for random arguments used outside list generation, such as `pan(random)` or `beat(0.5)`

**arguments**
- {Int+} -> the seed for the psudeorandom number generators (default=0)
- {Number} -> reset time in n-bars, or divisions (optional, default=null)

```java
set randomSeed 31415
set randomSeed 1618 2
```

## volume

Set the global volume in floating-point amplitude for all instruments across the entire environment. Additional ramptime in milliseconds can be provided to create fade-in/fade-out or smooth transitions to for dynamics.

**arguments**
- {Float} -> attenuate the total volume of all instruments (default=1)
- {Int+} -> ramptime in milliseconds or divisions (optional, default=0)

```java
set volume 0.5 5000
set volume 0.4 2/1
```

## highPass

Set the global highPass filter cutoff in Hz for all instruments across the entire environment. Additional ramptime in milliseconds can be provided to create smooth transitions from one value to another.

Alias: `hipass`

**arguments**
- {Float+} -> cutoff frequenzy in Hertz
- {Int+} -> ramptime in milliseconds or division (optional, default=1)

```java
set highPass 900 5000
set highPass 800 2/1
```

## lowPass

Set the global low-pass filter cutoff in Hz for all instruments across the entire environment. Additional ramptime in milliseconds can be provided to create smooth transitions from one value to another.

Alias: `lopass`

**arguments**
- {Float+} -> cutoff frequenzy in Hertz
- {Int+} -> ramptime in milliseconds or division (optional, default=1)

```java
set lowPass 900 5000
set lowPass 800 2/1
```

## beatRepeat

A beatrepeating effect (sometimes called stutter) that continuously repeats a section of the entire sound that was last played. The repating interval is determined in divisions (`1/4`, `3/16`, etc). It immediately starts repeating at the moment of evaluating the code, so timing is key!

Alias: `stutter`

**arguments**
- {Division} -> beatrepeat time interval in division

```java
set beatRepeat 1/4
```

## osc

Set the ip-address, in-port and out-port number for the network to transmit OSC-messages over using UDP. Default settings are 8000 (in-port), 9000 (out-port), localhost (127.0.0.1) (ip).

**arguments**
- {Int+} -> receiving port (default=8000)
- {Int+} -> sending port (default=9000)
- {Name} -> ip-address in the form of xxx.xxx.xxx.xxx or localhost (default=localhost)

```java
set osc default

set osc 8000 9000 127.0.0.1

set osc ip 127.0.0.1
set osc in 8000
set osc out 9000
```

## midi and midiClock

With the midi object you can get the available devices (ports) that you can use to send midi notes to with a `new midi` instrument.

```java
set midi getPorts
// prints the available ports to the console

new midi "AU DLS Synth 1" note(7 0) duration(250) time(1/4) gain(0.8)
```

>More on the midi instrument under [instruments](./02-instrument.md)

Output midiClock sync messages to sync an external device to the tempo of Mercury. The device name can have spaces. Use the `getports` argument to automatically open the console and view the different portnames. Use the `off` message or `silence` or `alt + .` to stop the syncing and send a stop message.

**arguments**
- {Name} -> getPorts, the midi portname or off (default=off)

```java
set midiClock getPorts
// returns the port names in console and automatically opens the console

set midiClock midiPortName
// turn the clock on and 
// outputs clock-sync to midiport of that name

set midiClock off
// turn the clock off (default)
```

## click

Enable a clicktrack/metronome sound to allow you to easily play along with the music. You can adjust the interval for the low pitch separately from the interval of the accent. The accent sounds an octave higher. You can also adjust the channel output for the click so you can hear it separately from the main output. Reset the settings with `default`.

**arguments**
- {Name} -> `on`, `off` or `default` (default=off)

```java
set click on
// turn the click on/off (default=off)

set click freq 1000
// set the base frequency for the click (default=900)

set click length 0.9
// adjust the length of the tone (default=0.65)

set click time 1/8
// set the base interval for the low pitch (default=1/4)

set click accent 1/2
// set the accent interval for the high pitch (default=1/1)

set click gain 0.8
// adjust the volume of the click sound (default=0.75)

set click out 3 4
// set the output channel(s) for the click, can be mono or stereo (default=1 2)

set click default
// reset all attributes to the default settings
```
