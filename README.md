# MIDI graph sequencer

WIP. Usable but probably buggy.

On start up the sequencer tries to connect to MIDI via loopMIDI or macOS virtual ports and falls back to Web Audio if that fails.

The sequencer is spatially based by default, but areas can become temporally based by the use of link ```phase``` and/or note ```hold```.

https://op12no2.github.io/graphseq/sequencer.html  

### Description

This is a bit flowery, but exactly how it's implemented.  

When you click Play ```agents``` are created at ```root``` notes. Think of agents as artists _performing_ the graph. Root notes have an outline. Double-click notes to toggle rootiness on/off.
 
When an agent reaches a note (including in the above context), the first thing it does is gate the note on at the specified ```pitch``` and ```velocity``` using the appropriate MIDI ```channel```. It does not do this if the note's ```monophonic``` checkbox is ticked and there already a note gated in the same ```graph``` (a note property).

Then it starts figuring out which output link(s) to follow:- 

1. FILTERING. Iterate the output links, independently-applying each link ```probability``` to get a list of candidates, which may be empty; only a probability of 1.0 ensures a link survives this step: if rand() < probability then add to candidate list.

2. GROUPING. Arrange the candidate links (if any) into groups based on link ```group```.

3. SELECTION. Select a _single_ link in each group (if any) based on link ```weight``` and discard the other candidates in that group. For example if there are two links in a group with weights 1 and 4 the latter will be selected 4 times more often.  

4. REPLICATION. The agent then self-replicates, making a replicant for _the_ link in each group (if any) and after optionally waiting around a while based on note ```hold```, pushes the replicants into the selected links at a location based on link ```phase``` and waves goodbye.

Finally the agent deletes itself; an agent never performs more than one note. 

In the background, helper agents are monitoring the notes playing, gating them off as needed based on a note's ```duration```.

### Discussion

I have deliberately resisted adding capabilities for notes to natively fire chords or random notes etc. It can all be done with the existing feature set and additionally you can then connect bits of the chord back into the graph with a low probability. 

To model a chord, create a note C0 with velocity 0 and link satellite notes C1 to Cn. Adjust the links to have a phase of 100 and unique groups (I'll add a helper to speed that up soon). It doesn't matter where they are geographically because the phase is 100. Now when C0 fires, C1 to Cn will also fire at the same time; well, one tick later (a few ms). Similarly, to make one of C1 to Cn fire randomly, set all the links to the same group and one will be picked. Adjust weights to make some get chosen more often than others. Adjust the probabilities down so a some never get a chance to be chosen. 

You can get similar results by linking C1 to Cn serially - because phase is 100 - and it also gives you the ability to apply probabilities cumulatively. In reality each note in a phase=100 sequence is gated at successive ticks, which is arguably less clinical anyway. Create broken chords by adjusting link phase. 

Watch out for feedback loops with agents self-replicating out of control as there are no birth control measures in place at the moment. I am finding it's almost impossisble to _design_ anything other than simple graphs, better to make a pretty pattern, tweak some settings and see what happens. Multiple disconnected graphs each with their own root note can be interesting when you arrange each around a different prime number. You can drag notes around and change note/link properties while the sequencer is playing. Deletion also seems to work, but don't be surprised if something very strange happens. There is no _new graph_ capability at the moment; just refresh the browser. Each small square is a 1/16 note (when link phase is 0). There is currently no auto-stop when/if all agents die. The plan is that note/link/agent rule sets will allow the graph to morph while it's being performed; i.e. link/note modfication, movement and creation/deletion. Click Esc to deselect and change the property bar back to a place where you can enter a name and description for your graph. Use the File menu to save it.

### Acknowledgements

- https://midinous.com/ - inspiration
- https://www.youtube.com/@tachesteaches - inspiration
- https://claude.ai - patience 
