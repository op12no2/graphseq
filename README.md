# MIDI graph sequencer

Try it here:-

https://op12no2.github.io/graphseq/sequencer.html  

### MIDI

On page load the sequencer uses Web Audio which is fine for exploring and playing with the examples. When you click the red MIDI button, it will try and connect to loopMIDI on Windows and IAC on macOS; both of which can then be connected to your DAW.

### Examples

[Example 1](https://op12no2.github.io/graphseq/sequencer.html?load=https://raw.githubusercontent.com/op12no2/graphseq/refs/heads/main/example_1.json)

### Keyboard assignments (PC-speak)

Double-click grid: create a new note using the properties from the last selected note (if any).

Double-click note: toggle root note status on/off.

Ctrl+drag from note to note: create a new link between the notes using the properties from the last selected link (if any). 

Ctrl+drag from note to to grid: create a new note and a new link as above. 

Alt+drag: zoom the grid.

Shift+drag: pan the grid.

←/→: cycle selection to next note or link (whichever is currenty selected)

Tab: toggle between selections note or links when using ←/→.

Delete: remove selected note/link.

Esc: display sequence properties.

### Acknowledgements

- https://midinous.com/ - inspiration
- https://www.youtube.com/@tachesteaches - inspiration
- https://claude.ai - patience 
