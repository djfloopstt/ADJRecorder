#Ableton DJ Recorder

##Pitch
The idea behind this project is to replace the mixtape feature of "The Bridge" for Ableton Live and Serato Scratch Live. The original idea behind "The Bridge" was to directly link Ableton to Serato to allow triggering of Ableton events inside of Serato, audio routing directly though Ableton from Serato to get access to all of the Ableton effects, and finally: the mixtape recording functionality.  This feature would record all of your movements as automations in an Ableton set, to be tweaked or fixed later.  "The Bridge" unfortunately does not work without special Rane hardware, the now obsolete Serato Scratch Live, and the full version of Ableton Live.  This project aims to replace that functionality to work with the newest version of Serato DJ, no extra hardware, and ideally allow Ableton Lite users to use the tool as well (I don't have the full Ableton lol).  Eventual goals of the project are to support other DAW's as well as other DJ softwares.

##Design Ideas
The idea is to intercept all of the MIDI messages going in between your DJ Controller and Serato then send them via a virtual MIDI port to both Serato and Ableton or simply saving out the resulting MIDI and sound data into an als project (eventual goal).


##Libraries planned to use
RtMidi - standard cross platform MIDI api
virtualMIDI - virtual MIDI port support on windows
