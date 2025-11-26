# MIDI graph sequencer

WIP. Usable but probably buggy.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back on Web Audio if that fails (just using a sine wave as a preview).

The sequencer is spatially based (non-linear) by default, but areas can become temporally based (linear) by the use of link ```phase``` and/or note ```hold```.

https://op12no2.github.io/graphseq/sequencer.html  

### Description

This is a bit flowery, but it's how I think about it and exactly how it's implemented in fact.  

When you click Play ```agents``` are born at ```root``` notes. Think of agents as artists _performing_ the graph. Root notes have an outline. Double-click notes to toggle.

When an agent reaches a note (including the above context), the first thing it does is gate the note on at the specified ```pitch``` and ```velocity``` using the appropriate MIDI ```channel```. It does not do this if the note's ```monophonic``` checkbox is ticked and there already a note gated at the same pitch.

Then it starts figuring out which output link(s) to follow. 

First of all it collects output links into groups based on link ```group```.

Then for each link in each group it applies the link ```probability``` to whittle things down a little. Some groups may disappear in the process. In fact all groups may disappear.

Next it picks one link in each group (in any) based on link ```weight``` and discards the other contenders. 

Then it self-replicates making a replicant for _the_ link in each group (if any) and after optionally waiting a while based on note ```hold```, pushes the replicants into the links at a location based on link ```phase``` and waves goodbye.

Finally it kills itself. An agent never performs more than one note. Sad.

In the background, helper agents are monitoring the notes playing, gating them off as needed based on a note's ```duration```.

### Acknowledgements

- https://midinous.com/ - inspiration
- https://www.youtube.com/@tachesteaches - inspiration
- https://claude.ai - inspiration and patience
