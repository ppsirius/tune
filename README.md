# TuneJS

**Authors:** Andrew Bernstein & Ben Taylor

**Overview:** Tune.js is a web audio tuning library of microtonal and just intonation scales. Tune.js supports over 3,000 historical tunings and temperaments, ported from Microtuner TIDoc files [compiled and documented by Victor Cerullo from 2003-2010](http://www.venetica.net/Sites/16tone/mtx_file_specs.htm).

**List of Tunings:** [Tuning Archive](http://abbernie.github.io/tune/scales.html)

**Demo:** [Microtonal Piano](http://abbernie.github.io/tune/)

### How to Tune.js, a Quick Start Guide

Download tune.js and include it in a script tag at the top of your page.

```html
<head>
	<script src="tune.js"></script>
</head>
```

Create a Tune.js instance.

```js
var tune = new Tune();
```

Load your scale of choice with the ```loadScale('scale-name') ``` method.

```js
tune.loadScale('mean19');
```

Pass MIDI note numbers to the ```note() ``` method. By default, ```note(midi-note-#) ``` returns the corresponding frequency in Hertz. You can use ```note() ``` to set the frequency of an oscillator.

```js
osc.frequency.value = tune.note(60);
```


### Properties

#### Tune.mode

Set the output mode of `tune.note()`. Choose between 

- **frequency**: `tune.note()` will return a hertz value, e.g. 392.43834 for a pure G4 over C4
- **ratio**: `tune.note()` will return a ratio value, e.g. 1.5 for a pure G over C
- **MIDI**: `tune.note()` will return an adjusted MIDI pitch, e.g. 67.0195 for a pure G4 over C4

```js
// Set the output mode to 'ratio', e.g. the ratio 3/2 will output 1.5
tune.mode.output = 'ratio';
```

The default output mode is 'frequency'. Currently the only available input mode is 'MIDI'. 

#### Tune.key

Returns the current key of a Tune instance. To set the key of a Tune instance use the ```setKey()``` method. The default key is set to 60 (middle C).

```js
var myKey = tune.key;
```

#### Tune.scale

Read only. An array containing the ratio values of the current scale loaded with the ```loadScale()``` method.

```js
// Returns the length of the current scale
var scaleLength = tune.scale.length;
```



### Methods

#### Tune.note(midi-note-#)

Returns a microtonally tuned note value for any MIDI integer input. By default, `Tune.note` returns a frequency value in hertz.

```js
// If the key we are in is C4 (60), this will return the frequency for 7th scale degree of our scale
var note = tune.note(67);
```

Depending on `Tune.mode`, the `Tune.note` method may return a frequency value in hertz (default, e.g. 392.43834 for a pure G4 over C4), a ratio value as a float (e.g. 1.5 for a pure G over C), or a MIDI float value (e.g. 67.0195 for a pure G4 over C4). See `Tune.mode`.

#### Tune.setKey(midi-note-#)

Sets the key and base frequency of a scale with the ```setKey(midi-note-#) ``` method.

```js
//sets the base (tonic) frequency to G4 or 392Hz
tune.setKey(67);
```

#### Tune.chord([array-of-midi-note-#s])

Returns an array of note values. Like `Tune.note()`, `Tune.chord()` returns values according to the current output mode (`Tune.mode`). 

```js
// returns a three note chord with the specified scale degrees
var myMicrotonalChord = [60,67,71];
tune.chord(myMicrotonalChord);
```

#### Tune.search("string")

Searches through the scale archive for scales that match the query.

```js
//returns an array of scale names that contain the word "partch"
tune.search("partch");
```

### Example Tunings

| Name | Description |
|------|-------------|
| ji_12 | Basic just instonation with 7-limit tritone |
| harm30 | First 30 harmonics and subharmonics |
| pyth_31 | 31-tone Pythagorean scale |
| ptolemy | Intense Diatonic Syntonon, also Zarlino's scale |
| couperin | Couperin modified meantone |
| helmholtz_pure | Helmholtz's two-keyboard harmonium tuning untempered |
| partch_43 | Harry Partch's 43-tone pure scale |
| johnston_81 | Ben Johnston's 81-note 5-limit scale of Sonata for Microtonal Piano |
| young-lm_piano | LaMonte Young's Well-Tempered Piano |
| xenakis_chrom | Xenakis's Byzantine Liturgical mode, 5 + 19 + 6 parts |
| slendro | Observed Javanese Slendro scale, Helmholtz/Ellis p. 518, nr.94 |
| harrison_5 | From Lou Harrison, a pelog style pentatonic |
| malkauns | Mode of Indian Raga Malkauns, inverse of prime_5 |

![BigP](http://www.mathopenref.com/images/bioimages/pythagoras1.jpg)
![BigZ](https://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Gioseffo_Zarlino.jpg/200px-Gioseffo_Zarlino.jpg)
![Partch](http://www.pas.org/images/default-source/hall-of-fame-photos/hpartch.jpg?sfvrsn=0)
