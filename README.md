# MIDI graph sequencer

WIP. Usable but probably buggy.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back on Web Audio if that fails (just using a sine wave as a preview).

The sequencer is spatially based (non-linear) by default, but areas can become temporally based (linear) by the use of link ```phase``` and/or note ```hold```.

https://op12no2.github.io/graphseq/sequencer.html  

### Description

This is a bit flowery, but it's how I think about it and exactly how it's implemented in fact.  

When you click Play ```agents``` are born at ```root``` notes. Think of agents as artists _performing_ the graph. Root notes have an outline. Double-click notes to toggle on/off.

When an agent reaches a note (including the above context), the first thing it does is gate the note on at the specified ```pitch``` and ```velocity``` using the appropriate MIDI ```channel```. It does not do this if the note's ```monophonic``` checkbox is ticked and there already a note gated at the same pitch.

Then it starts figuring out which output link(s) to follow. 

First of all it collects output links into groups based on link ```group```.

Then for each link in each group it applies the link ```probability``` to whittle things down a little. Some groups may disappear in the process. In fact all groups may disappear.

Next it picks one link in each group (if any) based on link ```weight``` and discards the other contenders. 

Then it self-replicates making a replicant for _the_ link in each group (if any) and after optionally waiting around a while based on note ```hold```, pushes the replicants into the links at a location based on link ```phase``` and waves goodbye.

Finally it kills itself. An agent never performs more than one note. Sad.

In the background, helper agents are monitoring the notes playing, gating them off as needed based on a note's ```duration```.

### Discussion

I have deliberately resisted adding capabilities for notes to fire chords or random notes etc. It can all be done with the existing feature set and additionally you can then connect bits of the chord back into the graph with a low probability.  

To model a chord, create a note C0 with velocity 0 and link satellite notes C1 to Cn. Adjust the links to have a phase of 100 and unique group numbers. It doesn't matter where they are geographically because the phase is 100. Now when C0 fires, C1 to Cn will also fire at the same time; well, one tick later (a few ms). Similarly, to make one of C1 to Cn fire randomly, set all the links to the same group and one will be picked. Adjust weights to make some fire more often than others. Or for just some to fire, adjust the probabilities down so a few never get a chance to be chosen. It takes a while to get used to it, but it's fun. In the future I'll add shortcuts to paste common graph segments from a library, rather then pile up note features. Having said that the next tweak is to add note, link and agent ```rules``` which can not only modify properties but create and delete notes/links/rules. One-off rules can create useful satellite notes that are used thereafter etc. You can get similar results by linking C1 to Cn serially - because phase is 100 - but it also gives you the ability to apply probabilities cumulatively. In reality each note in a phase=100 sequence is gated at successive ticks, which is arguably less clinical anyway. Create broken chords by adjusting link phase.   

### Acknowledgements

- https://midinous.com/ - inspiration
- https://www.youtube.com/@tachesteaches - inspiration
- https://claude.ai - inspiration and patience
