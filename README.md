# MIDI graph sequencer

WIP.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back on Web Audio if that fails (just using a sine wave as a preview).

https://op12no2.github.io/graphseq/sequencer.html  

One small square side is a 1/16 note. 

When Play is pressed ```agents``` are spotanuously created at ```root notes``` and then obey the rules below as if they had just encountered a note.

On reaching a note, the outgoing links are evaluated as follows:-

1. Apply the link's ```probability``` to get a list of links that have fired (maybe none).
2. For each collection of fired links defined by link ```group```, select one to use based on link ```weight```. 
3. Replicate the agent and squirt the replicants into these selected links based on link ```phase```.
4. Kill the original agent.

This is the default behaviour. The next step is to add rule sets that are evaluated and actioned; which will include self/neighbour note/link creation/modification and movement.



