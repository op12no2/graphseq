# MIDI graph sequencer

WIP.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back on Web Audio if that fails (just using a sine wave as a preview).

https://op12no2.github.io/graphseq/sequencer.html  

One small square side is a 1/16 note. 

When Play is pressed ```agents``` are spotanuously created at ```root notes``` and then obey the rules below as if they had just encountered a note.

On reaching a note, agents replicate themselves if there are any connected ```Always Fire``` links - and the replicants hop into them - their starting position is the link ```phase``, so this is how you can play chords (and broken chords). The original agent then evaluates the weights on any remaining links and hops into one or dies there and then if there are none.

This is the default behaviour. The next step is to add rule sets that are evaluated and actioned; which will include note/link creation/modification and movement.

Buglets: link selection when 2 notes are interconnected.
