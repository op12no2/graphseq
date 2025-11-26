# MIDI graph sequencer

WIP. Usable but probably buggy.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back on Web Audio if that fails (just using a sine wave as a preview).

The sequencer is spatially based (non-linear) by default, but areas can become temporally based (linear) by the use of link ```phase``` and/or note ```hold```.

https://op12no2.github.io/graphseq/sequencer.html  

### Description


### Tips 

- Don't try and predict/design - create a pretty pattern, tweak some note/link settings and see what happens :)
- Start simple.
- Watch out for feedback loops!

### Acknowledgements

- https://midinous.com/ - inspiration
- https://www.youtube.com/@tachesteaches  - inspiration
- https://claude.ai - patiently performing endless refactors
