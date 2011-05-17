audiolib.js
===========

audiolib.js is a powerful audio tools library for javascript.

Amongst other things, it provides AudioDevice class which has a consistent callback API that supports both Firefox4's Audio Data API and Chrome 10's Web Audio API.

Usage
-----
var dev = new AudioDevice(sampleRate, channelCount, function(sampleBuffer){
	// Fill the buffer here.
});

```javascript
// Effects

var del = new audioLib.Delay(sampleRate, delay, feedback);

var flt = new audioLib.IIRFilter(sampleRate, cutoffFreq, resonance);

var flt = new audioLib.LP12Filter(sampleRate, cutoffFreq, resonance);

var flt = new audioLib.LowPassFilter(sampleRate, cutoffFreq, resonance);

var dist = new audioLib.Distortion(sampleRate);

// to feed a new input sample
effect.pushSample(sample);
// to get the output
sample = effect.getMix();

// Synthesis

var osc = new audioLib.Oscillator(sampleRate, frequency);

// to generate a new sample
osc.generate(fm1, fm2, ..., fmX);
// to get the output
osc.getMix();

// Envelopes

var adsr = new audioLib.ADSREnvelope(sampleRate, attack, decay, sustain, release);

// to trigger the gate
adsr.triggerGate(isOpen);
// to update the value ** Do this on every sample fetch for this to work properly. also returns the current value
adsr.generate();
// Get the value
adsr.value; // 0.0 - 1.0, unless you put something more as sustain

var stepSeq = new audioLib.StepSequencer(sampleRate, stepLength, stepArray, attack);

// To start the sequence over
stepSeq.triggerGate();
// to update the value ** Do this on every sample fetch for this to work properly. also returns the current value
stepSeq.generate();
// Get the value
stepSeq.value; // 0.0 - 1.0

//Recording

var rec = dev.record();

// To stop
rec.stop();
// To export wav
var audioElement = new Audio(
	'data:audio/wav;base64,' +
	btoa( rec.toWav() ) // presuming btoa is supported
);

```

Demos
-----

(if you have your own, please fork & add | msg me)
 * http://niiden.com/orbisyn/


Licensed under MIT license.
